---
title: Connect PostgreSQL via SSH Tunnel
description: Leer hoe u uw PostgreSQL-database via een SSH-tunnel met Commerce Intelligence kunt verbinden.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Verbinden [!DNL PostgreSQL] via [!DNL SSH Tunnel]

Als u de [!DNL PostgreSQL] -database wilt verbinden met [!DNL Commerce Intelligence] via een `SSH tunnel` , moet u een aantal dingen doen:

1. [Wint  [!DNL Commerce Intelligence]  openbare sleutel terug](#retrieve)
1. [Toestaan toegang tot het  [!DNL Commerce Intelligence]  IP adres](#allowlist)
1. [Creeer a [!DNL Linux]  gebruiker voor  [!DNL Commerce Intelligence]](#linux)
1. [Creeer a [!DNL PostgreSQL]  gebruiker voor  [!DNL Commerce Intelligence]](#postgres)
1. [Ga de verbinding en gebruikersinformatie in  [!DNL Commerce Intelligence]](#finish)

## De [!DNL Commerce Intelligence] [!DNL public key] ophalen {#retrieve}

`public key` wordt gebruikt om de gebruiker [!DNL Commerce Intelligence] [!DNL Linux] te autoriseren. Nu gaat u de gebruiker maken en de sleutel importeren.

1. Ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add a Data Source]** .
1. Klik op het pictogram [!DNL PostgreSQL] .
1. Nadat de pagina `PostgreSQL credentials` is geopend, stelt u de `Encrypted` toggle in op `Yes` . Hierdoor wordt het instellingsformulier van `SSH` weergegeven.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Hieronder ziet u hoe u door [!DNL Commerce Intelligence] kunt navigeren om de toets op te halen:

![&#x200B; het terugwinnen van de openbare sleutel RJMetrics &#x200B;](../../../assets/get-mbi-public-key.gif)

## Toegang tot het IP-adres van [!DNL Commerce Intelligence] toestaan {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adres toe te staan. Het is `54.88.76.97/32` , maar het staat ook op de pagina met referenties van `PostgreSQL` . Zie de blauwe doos in de GIF hierboven.

## Een [!DNL Linux] gebruiker voor [!DNL Commerce Intelligence] maken {#linux}

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt [&#x200B; deze gebruiker &#x200B;](../../../administrator/account-management/restrict-db-access.md) om het even welke manier beperken u houdt, zolang het het recht behoudt om met de [!DNL PostgreSQL] server te verbinden.

1. Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als hoofdmap op de [!DNL Linux] -server uit:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Weet u nog welke `public key` u in de eerste sectie hebt opgehaald? Om ervoor te zorgen dat de gebruiker toegang heeft tot de database, moet u de sleutel importeren in `authorized\_keys` .

   Kopieer de volledige sleutel als volgt naar het `authorized\_keys` -bestand:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Als u de gebruiker wilt maken, wijzigt u de machtigingen voor de map `/home/rjmetric` zodat toegang wordt verleend via `SSH` :

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Als het `sshd\_config` -bestand dat aan de server is gekoppeld niet is ingesteld op de standaardoptie, hebben alleen bepaalde gebruikers toegang tot de server. Hierdoor wordt een geslaagde verbinding met [!DNL Commerce Intelligence] voorkomen. In deze gevallen is het nodig om een opdracht als `AllowUsers` uit te voeren om de Sprite-gebruiker toegang tot de server te verlenen.

## Een [!DNL Commerce Intelligence] [!DNL Postgres] -gebruiker maken {#postgres}

Uw organisatie kan een verschillend proces vereisen, maar de eenvoudigste manier om deze gebruiker tot stand te brengen is de volgende vraag uit te voeren wanneer het programma geopend in Postgres als gebruiker met het recht om voorrechten te verlenen. De gebruiker moet ook eigenaar zijn van het schema waartoe [!DNL Commerce Intelligence] toegang krijgt.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Vervang `secure password` door uw eigen beveiligingswachtwoord, dat anders kan zijn dan het SSH-wachtwoord. Vervang `database name` en `schema name` ook door de juiste namen in de database.

Als u veelvoudige gegevensbestanden of schema&#39;s wilt verbinden, herhaal dit proces zonodig.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] . Hebt u de aanmeldingspagina van [!DNL PostgreSQL] geopend? Als dat niet het geval is, gaat u naar **[!UICONTROL Manage Data > Connections]** en klikt u op **[!UICONTROL Add a Data Source]** , gevolgd door het pictogram [!DNL PostgreSQL] . Vergeet niet de `Encrypted` -schakeloptie in te stellen op `Yes` .

Voer de volgende gegevens op deze pagina in, te beginnen met de sectie `Database Connection` :

* `Username`: De RJMetrics Postgres-gebruikersnaam (moet rjmetrisch zijn)
* `Password`: Het wachtwoord voor RJMetrics Postgres
* `Port`: PostSQL-poort op uw server (standaard 5432)
* `Host`: 127.0.0.1

Onder `SSH Connection` :

* `Remote Address`: Het IP-adres of de hostnaam van de server waarnaar u verzendt
* `Username`: uw SSH-aanmeldnaam (moet rjmetrisch zijn)
* `SSH Port`: SSH-poort op uw server (standaard 22)

Wanneer u wordt gebeëindigd, klik **sparen &amp; Test** om de opstelling te voltooien.

### Verwante

* [&#x200B; Reauthenticating integrations &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
