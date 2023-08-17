---
title: Verbinden [!DNL MongoDB] via SSH-tunnel
description: Leer hoe u verbinding maakt [!DNL MongoDB] via SSH-tunnel.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Verbinden [!DNL MongoDB] via SSH-tunnel

Als u verbinding wilt maken met uw [!DNL MongoDB] database naar [!DNL Commerce Intelligence] via een SSH-tunnel moet u een aantal dingen doen:

1. [De [!DNL Commerce Intelligence] openbare sleutel](#retrieve)
1. [Toegang tot de [!DNL Commerce Intelligence] IP-adres](#allowlist)
1. [Een Linux-gebruiker maken voor de handelsinlichtingendienst](#linux)
1. [Een [!DNL MongoDB] gebruiker for Commerce Intelligence](#mongodb)
1. [Voer de verbinding en gebruikersgegevens in [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>Vanwege de technische aard van deze installatie, raadt de Adobe u aan om een lus uit te voeren in een ontwikkelaar om u te helpen als u dit nog niet eerder hebt gedaan.

## De [!DNL Commerce Intelligence] openbare sleutel {#retrieve}

De `public key` wordt gebruikt om de [!DNL Commerce Intelligence] `Linux` gebruiker. In de volgende sectie wordt u door het maken van de gebruiker geleid en worden de sleutels geïmporteerd.

1. Ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]**.
1. Klik op de knop [!DNL MONGODB] pictogram.
1. Na de [!DNL MongoDB] aanmeldingspagina wordt geopend, de `Encrypted` schakelen naar `Yes`. Dit toont de de opstellingsvorm van SSH.
1. De `public key` onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Als u een beetje verloren bent, is hier hoe te door te navigeren [!DNL Commerce Intelligence] om de sleutel op te halen:

![Het terugwinnen van de openbare sleutel RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Toegang tot de [!DNL Commerce Intelligence] IP-adres {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151`, maar het is ook [!DNL MongoDB] pagina met referenties:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Een `Linux` gebruiker voor [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Als de `sshd_config` het bestand dat aan de server is gekoppeld, is niet ingesteld op de standaardoptie. Alleen bepaalde gebruikers hebben toegang tot de server. Hierdoor wordt een verbinding met [!DNL Commerce Intelligence]. In deze gevallen is het nodig om een opdracht als `AllowUsers` de `rjmetric` toegang tot de server.

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt deze gebruiker op elke gewenste manier beperken zolang deze het recht behoudt om verbinding te maken met de [!DNL MongoDB] server.

Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als basis uit op uw `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

De `public key` bent u opgehaald in de eerste sectie? Om ervoor te zorgen dat de gebruiker toegang heeft tot de database, moet u de sleutel importeren in `authorized_keys`. Kopieer de hele sleutel naar de `authorized_keys` bestand als volgt:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Om te beëindigen creërend de gebruiker, verander de toestemmingen op de /home/rjmetrische folder om toegang via SSH toe te staan:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Een [!DNL Commerce Intelligence] [!DNL MongoDB] user {#mongodb}

[!DNL MongoDB] servers hebben twee uitvoeringsmodi - [met de optie &quot; auth &quot;](#auth) `(mongod -- auth)` en één zonder [is de standaardwaarde](#default). De stappen voor het maken van [!DNL MongoDB] de gebruiker varieert afhankelijk van de modus die de server gebruikt. Controleer de modus voordat u verdergaat.

### Als uw server de `Auth` Optie: {#auth}

Wanneer u verbinding maakt met meerdere databases, kunt u de gebruiker toevoegen door u aan te melden [!DNL MongoDB] als een beheerder gebruiker en het uitvoeren van de volgende bevelen.

>[!NOTE]
>
>Om alle beschikbare gegevensbestanden te zien, [!DNL Commerce Intelligence] gebruiker vereist de rechten om te kunnen worden uitgevoerd `listDatabases.`

Deze opdracht verleent de [!DNL Commerce Intelligence] gebruikerstoegang `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Gebruik deze opdracht om het [!DNL Commerce Intelligence] gebruikerstoegang `to a single database`:

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

Als uw server dit niet gebruikt `auth` modus, uw [!DNL MongoDB] is zelfs zonder gebruikersnaam en wachtwoord toegankelijk. U dient echter de `mongodb.conf` file `(/etc/mongodb.conf)` heeft de volgende regels. Als dat niet het geval is, start u de server opnieuw nadat u deze hebt toegevoegd.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Om uw [!DNL MongoDB] de server aan een verschillend adres, pas de gegevensbestand hostname in de volgende stap dienovereenkomstig aan.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]. Heb je de [!DNL MongoDB] aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Data > Connections]** en klik op **[!UICONTROL Add New Data Source]** en vervolgens de [!DNL MongoDB] pictogram. Vergeet niet de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Host`: `127.0.0.1`
* `Username`: De [!DNL Commerce Intelligence] [!DNL MongoDB] username (moet `rjmetric`)
* `Password`: De [!DNL Commerce Intelligence] [!DNL MongoDB] password
* `Port`: MongoDB-poort op uw server (`27017` standaard)
* `Database Name` (Optioneel): als u slechts toegang tot één database hebt toegestaan, geeft u hier de naam van die database op.

Onder de `SSH Connection` sectie:

* `Remote Address`: Het IP-adres of de hostnaam van de server waarin u SSH wilt plaatsen
* `Username`: De [!DNL Commerce Intelligence] Linux (SSH)-gebruikersnaam (moet ook Jometrisch zijn)
* `SSH Port`: De SSH-poort op uw server (standaard ingesteld op 22)

Klik op **[!UICONTROL Save Test]** om de installatie te voltooien.

### Verwante

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
