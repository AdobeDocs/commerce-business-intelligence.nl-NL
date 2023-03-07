---
title: Connect PostgreSQL via SSH Tunnel
description: Leer hoe u uw PostSQL-database kunt verbinden met [!DNL MBI] via een SSH-tunnel.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Verbinden `PostgreSQL` via `SSH` Tunnel

Als u verbinding wilt maken met uw `PostgreSQL` database naar [!DNL MBI] via een `SSH tunnel`, moet u (of uw team, als u geen technicus bent) een paar dingen doen:

1. [De [!DNL MBI] openbare sleutel](#retrieve)
1. [Toegang tot de [!DNL MBI] IP-adres](#allowlist)
1. [Een Linux maken](#linux)
1. [Een gebruiker van Postbus maken voor [!DNL MBI] ](#postgres)
1. [Voer de verbinding en gebruikersgegevens in MBI in](#finish)

Het is niet zo ingewikkeld als het zou kunnen klinken. Aan de slag.

## De [!DNL MBI] `public key` {#retrieve}

De `public key` wordt gebruikt om de [!DNL MBI] Linux®-gebruiker. In de volgende sectie maakt u de gebruiker en importeert u de sleutel.

1. Ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add a Data Source]**.
1. Klik op de knop `PostgreSQL` pictogram.
1. Na de `PostgreSQL credentials` pagina wordt geopend, stelt u de `Encrypted` schakelen naar `Yes`. Hierdoor wordt het dialoogvenster `SSH` instellingsformulier.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Als u een beetje verloren bent, is dit hoe te door te navigeren [!DNL MBI] om de sleutel op te halen:

![Het terugwinnen van de openbare sleutel RJMetrics](../../../assets/get-mbi-public-key.gif)

## Toegang tot de [!DNL MBI] IP-adres {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adres toe te staan. Het is `54.88.76.97/32`, maar het is ook `PostgreSQL` aanmeldingspagina. De blauwe doos in het bovenstaande GIF bekijken? Dat is het!

## Een `Linux` gebruiker voor [!DNL MBI] {#linux}

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt [deze gebruiker beperken](../../../administrator/account-management/restrict-db-access.md) op elke gewenste manier, zolang het recht behouden blijft om verbinding te maken met de PostgreSQL-server.

1. Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als hoofdmap uit op uw `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Onthoud de `public key` bent u opgehaald in de eerste sectie? Om ervoor te zorgen dat de gebruiker toegang heeft tot de database, moet u de sleutel importeren in `authorized\_keys`.

   Kopieer de hele sleutel naar de `authorized\_keys` bestand als volgt:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Als u de gebruiker wilt maken, wijzigt u de machtigingen voor de `/home/rjmetric` map om toegang toe te staan via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Als de `sshd\_config` het bestand dat aan de server is gekoppeld, is niet ingesteld op de standaardoptie. Alleen bepaalde gebruikers hebben toegang tot de server. Hierdoor wordt een verbinding met [!DNL MBI]. In deze gevallen is het nodig om een opdracht als `AllowUsers` om de rjmetrische gebruiker toegang tot de server toe te staan.

## Een [!DNL MBI] Postbus-gebruiker {#postgres}

Uw organisatie kan een verschillend proces vereisen, maar de eenvoudigste manier om deze gebruiker tot stand te brengen is de volgende vraag uit te voeren wanneer het programma geopend in Postgres als gebruiker met het recht om voorrechten te verlenen. De gebruiker zou ook het schema moeten bezitten dat [!DNL MBI] toegang wordt verleend tot.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Vervangen `secure password` met uw eigen beveiligde wachtwoord, dat anders kan zijn dan het SSH-wachtwoord. Ook, zorg ervoor u vervangt `database name` en `schema name` met de juiste namen in uw database.

Als u veelvoudige gegevensbestanden of schema&#39;s wilt verbinden, herhaal dit proces zonodig.

## De verbinding en gebruikersgegevens invoeren in [!DNL MBI] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL MBI]. Hebt u de aanmeldingspagina van PostgreSQL geopend? Indien niet, ga naar **[!UICONTROL Manage Data > Connections]** en klik op **[!UICONTROL Add a Data Source]** en vervolgens het PostgreSQL-pictogram. Vergeet niet de instelling van de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de sectie Databaseverbinding:

* `Username`: De RJMetrics Postgres-gebruikersnaam (moet rjmetrisch zijn)
* `Password`: Het wachtwoord voor RJMetrics Postgres
* `Port`: PostSQL-poort op uw server (standaard 5432)
* `Host`: 127.0.0.1

Onder `SSH Connection`:

* `Remote Address`: Het IP adres of hostname van de server u in zult SSH
* `Username`: Uw SSH login naam (zou rjmetrisch moeten zijn)
* `SSH Port`: SSH-poort op uw server (standaard 22)

Dat is het! Als u klaar bent, klikt u op **Opslaan en testen** om de installatie te voltooien.

### Verwante

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
