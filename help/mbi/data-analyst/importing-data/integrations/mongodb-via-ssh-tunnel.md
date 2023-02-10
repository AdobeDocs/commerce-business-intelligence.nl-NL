---
title: Verbinden [!DNL MongoDB] via SSH-tunnel
description: Leer hoe u verbinding maakt [!DNL MongoDB] via SSH-tunnel.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Verbinden [!DNL MongoDB] via SSH-tunnel


Als u verbinding wilt maken met uw [!DNL MongoDB] database naar [!DNL MBI] via een tunnel SSH, zult u (of uw team, als u geen technicus bent) een paar dingen moeten doen:

1. [De [!DNL MBI] openbare sleutel](#retrieve)
1. [Toegang tot de [!DNL MBI] IP-adres](#allowlist)
1. [Een Linux-gebruiker voor MBI maken](#linux)
1. [Een [!DNL MongoDB] gebruiker voor MBI](#mongodb)
1. [Voer de verbinding en gebruikersgegevens in [!DNL MBI]](#finish)

>[!NOTE]
>
>Gezien de technische aard van deze opstelling, adviseren wij u in een ontwikkelaar te herhalen om uit te helpen als u dit niet eerder hebt gedaan.

## De [!DNL MBI] openbare sleutel {#retrieve}

De `public key` wordt gebruikt om de [!DNL MBI] `Linux` gebruiker. In de volgende sectie maken we de gebruiker en importeren we de sleutel.

1. Ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]**.
1. Klik op de knop [!DNL MONGODB] pictogram.
1. Na de [!DNL MongoDB] aanmeldingspagina wordt geopend, wijzigt u de `Encrypted` schakelen naar `Yes`. Hiermee wordt het SSH-instellingsformulier weergegeven.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Als u een beetje verloren bent, is hier hoe te door te navigeren [!DNL MBI] om de sleutel op te halen:

![Het terugwinnen van de openbare sleutel RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Toegang tot de [!DNL MBI] IP-adres {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf onze IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151`, maar het is ook [!DNL MongoDB] aanmeldingspagina:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Een `Linux` gebruiker voor [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>Als de `sshd_config` bestand dat aan de server is gekoppeld, is niet ingesteld op de standaardoptie. Alleen bepaalde gebruikers hebben toegang tot de server. Hierdoor wordt een verbinding met [!DNL MBI]. In deze gevallen is het nodig om een opdracht als `AllowUsers` de `rjmetric` gebruikerstoegang tot de server.

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt deze gebruiker op elke gewenste manier beperken zolang deze het recht behoudt om verbinding te maken met de [!DNL MongoDB] server.

Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als hoofdmap uit op uw `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Onthoud de `public key` hebben we in de eerste sectie opgehaald? Om ervoor te zorgen dat de gebruiker toegang heeft tot de database, moeten we de sleutel importeren in `authorized_keys`. Kopieer de hele sleutel naar de `authorized_keys` bestand als volgt:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Om te beëindigen creërend de gebruiker, verander de toestemmingen op de /home/rjmetrische folder om toegang via SSH toe te staan:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Een [!DNL MBI] [!DNL MongoDB] user {#mongodb}

[!DNL MongoDB] servers hebben twee uitvoeringsmodi - [met de optie &quot; auth &quot;](#auth) `(mongod -- auth)` en één zonder [is de standaardinstelling](#default). De stappen voor het maken van een [!DNL MongoDB] De gebruiker zal een beetje afhankelijk van welke wijze variëren uw server gebruikt, zodat zeker om de wijze te verifiëren alvorens verder te gaan.

### Als uw server de `Auth` Optie: {#auth}

Wanneer u verbinding maakt met meerdere databases, kunt u de gebruiker toevoegen door u aan te melden [!DNL MongoDB] als een beheerder en de volgende opdrachten uitvoeren.

>[!NOTE]
>
>Om alle beschikbare gegevensbestanden te zien, [!DNL MBI] gebruiker vereist de rechten om te kunnen worden uitgevoerd `listDatabases.`

Deze opdracht geeft de [!DNL MBI] gebruikerstoegang `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Gebruik deze opdracht om het [!DNL MBI] gebruikerstoegang `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Hiermee wordt een reactie afgedrukt die er als volgt uitziet:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Als uw server de standaardoptie gebruikt {#default}

Als uw server dit niet gebruikt `auth` modus, uw [!DNL MongoDB] server is ook zonder gebruikersnaam en wachtwoord toegankelijk. U dient echter de `mongodb.conf` file `(/etc/mongodb.conf)` heeft de volgende regels. Als dat niet het geval is, start u de server opnieuw nadat u deze hebt toegevoegd.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Om uw [!DNL MongoDB] de server aan een verschillend adres, pas de gegevensbestand hostname in de volgende stap dienovereenkomstig aan.

## De verbinding en gebruikersgegevens invoeren in [!DNL MBI] {#finish}

Om dingen te verpakken, moeten wij de verbinding en gebruikersinformatie ingaan in [!DNL MBI]. Heb je de [!DNL MongoDB] aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Data > Connections]** en klik op **[!UICONTROL Add New Data Source]** en de [!DNL MongoDB] pictogram. Vergeet niet de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Host`: `127.0.0.1`
* `Username`: De [!DNL MBI] [!DNL MongoDB] username (moet `rjmetric`)
* `Password`: De [!DNL MBI] [!DNL MongoDB] password
* `Port`: De poort van MongoDB op uw server (`27017` standaard)
* `Database Name` (Optioneel): Als u slechts toegang tot één gegevensbestand hebt toegestaan, specificeer hier de naam van dat gegevensbestand.

Onder de `SSH Connection` sectie:

* `Remote Address`: Het IP adres of hostname van de server wij SSH in zullen
* `Username`: De [!DNL MBI] Linux (SSH)-gebruikersnaam (moet ook Jometrisch zijn)
* `SSH Port`: De haven van SSH op uw server (22 door gebrek)

Dat is het! Als u klaar bent, klikt u op **[!UICONTROL Save Test]** om de installatie te voltooien.

### Verwante

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
