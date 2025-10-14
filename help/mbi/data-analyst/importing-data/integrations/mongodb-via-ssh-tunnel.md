---
title: Verbind  [!DNL MongoDB]  via de tunnel van SSH
description: Leer hoe te om  [!DNL MongoDB]  via de tunnel van SSH te verbinden.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Verbinden [!DNL MongoDB] via SSH Tunnel

Als u de [!DNL MongoDB] -database via een SSH-tunnel wilt verbinden met [!DNL Commerce Intelligence] , moet u een aantal dingen doen:

1. [Wint  [!DNL Commerce Intelligence]  openbare sleutel terug](#retrieve)
1. [Toestaan toegang tot het  [!DNL Commerce Intelligence]  IP adres](#allowlist)
1. [Een Linux-gebruiker voor Commerce Intelligence maken](#linux)
1. [Creeer a [!DNL MongoDB]  gebruiker voor Commerce Intelligence](#mongodb)
1. [Ga de verbinding en gebruikersinformatie in  [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>Vanwege de technische aard van deze installatie, raadt Adobe u aan een lus uit te voeren in een ontwikkelaar om uit te zoeken of u dit nog niet eerder hebt gedaan.

## De openbare sleutel [!DNL Commerce Intelligence] ophalen {#retrieve}

`public key` wordt gebruikt om de gebruiker [!DNL Commerce Intelligence] `Linux` te autoriseren. In de volgende sectie wordt u door het maken van de gebruiker geleid en worden de sleutels geïmporteerd.

1. Ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** .
1. Klik op het pictogram [!DNL MONGODB] .
1. Nadat de aanmeldingspagina van [!DNL MongoDB] is geopend, wijzigt u de schakeloptie `Encrypted` in `Yes` . Dit toont de de opstellingsvorm van SSH.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Als u een beetje verloren bent, is hier hoe te door [!DNL Commerce Intelligence] te navigeren om de sleutel terug te winnen:

![&#x200B; het terugwinnen van de openbare sleutel RJMetrics &#x200B;](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Toegang tot het IP-adres van [!DNL Commerce Intelligence] toestaan {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151` , maar ze staan ook op de aanmeldingspagina van [!DNL MongoDB] :

![&#x200B; MBI_Allow_Access_IPs.png &#x200B;](../../../assets/MBI_allow_access_IPs.png)

## Een `Linux` gebruiker voor [!DNL Commerce Intelligence] maken {#linux}

>[!IMPORTANT]
>
>Als het `sshd_config` -bestand dat aan de server is gekoppeld niet is ingesteld op de standaardoptie, hebben alleen bepaalde gebruikers toegang tot de server. Hierdoor wordt een geslaagde verbinding met [!DNL Commerce Intelligence] voorkomen. In deze gevallen is het nodig een opdracht als `AllowUsers` uit te voeren om de `rjmetric` -gebruiker toegang te geven tot de server.

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt deze gebruiker op elke gewenste manier beperken zolang deze het recht behoudt om verbinding te maken met de [!DNL MongoDB] -server.

Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als hoofdmap op de `Linux` -server uit:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Weet u nog welke `public key` u in de eerste sectie hebt opgehaald? Om ervoor te zorgen dat de gebruiker toegang heeft tot de database, moet u de sleutel importeren in `authorized_keys` . Kopieer de volledige sleutel als volgt naar het `authorized_keys` -bestand:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Om te beëindigen creërend de gebruiker, verander de toestemmingen op de /home/rjmetrische folder om toegang via SSH toe te staan:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Een [!DNL Commerce Intelligence] [!DNL MongoDB] -gebruiker maken {#mongodb}

[!DNL MongoDB] de servers hebben twee looppaswijzen - [&#x200B; met de &quot;auth&quot;optie &#x200B;](#auth) `(mongod -- auth)` en zonder, [&#x200B; die het gebrek &#x200B;](#default) is. De stappen voor het maken van een [!DNL MongoDB] -gebruiker variëren afhankelijk van de modus die de server gebruikt. Controleer de modus voordat u verdergaat.

### Als de server de optie `Auth` gebruikt: {#auth}

Wanneer u verbinding maakt met meerdere databases, kunt u de gebruiker toevoegen door u aan te melden bij [!DNL MongoDB] als beheerder en de volgende opdrachten uit te voeren.

>[!NOTE]
>
>Om alle beschikbare databases te kunnen zien, vereist de [!DNL Commerce Intelligence] -gebruiker de rechten om `listDatabases.` uit te voeren

Met deze opdracht krijgt de [!DNL Commerce Intelligence] gebruiker toegang `to all databases` :

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Gebruik deze opdracht om de [!DNL Commerce Intelligence] gebruiker toegang te verlenen `to a single database` :

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

Als uw server de modus `auth` niet gebruikt, is uw [!DNL MongoDB] -server ook toegankelijk zonder gebruikersnaam en wachtwoord. U moet er echter voor zorgen dat het `mongodb.conf` bestand `(/etc/mongodb.conf)` de volgende regels heeft. Als dit niet het geval is, start u de server opnieuw nadat u deze hebt toegevoegd.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Als u de [!DNL MongoDB] -server aan een ander adres wilt binden, past u de hostnaam van de database in de volgende stap dienovereenkomstig aan.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] . Hebt u de aanmeldingspagina van [!DNL MongoDB] geopend? Als dat niet het geval is, gaat u naar **[!UICONTROL Data > Connections]** en klikt u op **[!UICONTROL Add New Data Source]** , gevolgd door het pictogram [!DNL MongoDB] . Vergeet niet de `Encrypted` -schakeloptie in `Yes` te wijzigen.

Voer de volgende gegevens op deze pagina in, te beginnen met de sectie `Database Connection` :

* `Host`: `127.0.0.1`
* `Username`: De gebruikersnaam [!DNL Commerce Intelligence] [!DNL MongoDB] (moet `rjmetric` zijn)
* `Password`: Het wachtwoord [!DNL Commerce Intelligence] [!DNL MongoDB]
* `Port`: MongoDB-poort op uw server (`27017` standaard)
* `Database Name` (Optioneel): als u slechts toegang tot één database hebt toegestaan, geeft u hier de naam van die database op.

Onder de sectie `SSH Connection` :

* `Remote Address`: Het IP-adres of de hostnaam van de server waarnaar u verzendt
* `Username`: De [!DNL Commerce Intelligence] Linux (SSH)-gebruikersnaam (moet rjmetrisch zijn)
* `SSH Port`: De SSH-poort op uw server (standaard 22)

Als u klaar bent, klikt u op **[!UICONTROL Save Test]** om de installatie te voltooien.

### Verwante

* [&#x200B; Reauthenticating integrations &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
