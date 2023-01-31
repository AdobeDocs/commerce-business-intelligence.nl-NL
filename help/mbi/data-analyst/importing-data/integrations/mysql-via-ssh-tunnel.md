---
title: MySQL verbinden via SSH-tunnel
description: Leer hoe te om MySQL via de Tunnel van SSH te verbinden.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Verbinden `MySQL` via `SSH Tunnel`

* [De [!DNL MBI] openbare sleutel](#retrieve)
* [Toegang tot de [!DNL MBI] IP-adres](#allowlist)
* [Een Linux-gebruiker maken voor [!DNL MBI]](#linux)
* [Een MySQL-gebruiker maken voor [!DNL MBI]](#mysql)
* [Voer de verbinding en gebruikersgegevens in [!DNL MBI]](#finish)

## GA NAAR

* `MySQL via SSH tunnel`
* [` MySQL`](../integrations/mysql-via-a-direct-connection.md)
* [` MySQL`](../integrations/mysql-via-cpanel.md)

Als u verbinding wilt maken met uw `MySQL` database naar [!DNL MBI] via een `SSH tunnel`, zult u (of uw team, als u geen technicus bent) een paar dingen moeten doen:

1. De [!DNL MBI] `public key`
1. Toegang tot de [!DNL MBI] `IP address`
1. Een `Linux` gebruiker voor [!DNL MBI]
1. Een `MySQL` gebruiker voor [!DNL MBI]
1. Voer de verbinding en gebruikersgegevens in [!DNL MBI]

Het is niet zo ingewikkeld als het zou kunnen klinken. Laten we beginnen.

## De [!DNL MBI] openbare sleutel {#retrieve}

De `public key` wordt gebruikt om de [!DNL MBI] `Linux` gebruiker. In de volgende sectie wordt de gebruiker gemaakt en wordt de sleutel geïmporteerd.

1. Ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]**.
1. Klik op de knop `MySQL` pictogram.
1. Na de `MySQL credentials` pagina wordt geopend, stelt u de `Encrypted` schakelen naar `Yes`. Hiermee wordt het SSH-instellingsformulier weergegeven.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Als u een beetje verloren bent, is hier hoe te door te navigeren [!DNL MBI] om de sleutel op te halen:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Toegang tot de [!DNL MBI] IP-adres {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf onze IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151` maar ze staan ook op de `MySQL credentials` pagina. De blauwe doos in het bovenstaande GIF bekijken? Dat is het!

## Een `Linux` gebruiker voor [!DNL MBI] {#linux}

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt [deze gebruiker beperken](../../../administrator/account-management/restrict-db-access.md) op elke gewenste manier, zolang het recht behoudt om verbinding te maken met het `MySQL` server.

1. Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als hoofdmap uit op uw `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Onthoud de `public key` hebben we in de eerste sectie opgehaald? Om ervoor te zorgen dat de gebruiker toegang heeft tot de database, moeten we de sleutel importeren in `authorized\_keys`.

   Kopieer de hele sleutel naar de `authorized\_keys` bestand als volgt:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Als u de gebruiker wilt maken, wijzigt u de machtigingen voor de `/home/rjmetric` map om toegang toe te staan via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Als de `sshd\_config` bestand dat aan de server is gekoppeld, is niet ingesteld op de standaardoptie. Alleen bepaalde gebruikers hebben toegang tot de server. Hierdoor wordt een verbinding met [!DNL MBI]. In deze gevallen is het nodig om een opdracht als `AllowUsers` de `rjmetric` gebruikerstoegang tot de server.

## Een `MySQL` gebruiker voor [!DNL MBI] {#mysql}

Uw organisatie kan een verschillend proces vereisen, maar de eenvoudigste manier om deze gebruiker tot stand te brengen is de volgende vraag uit te voeren wanneer het programma wordt geopend in `MySQL` als gebruiker met het recht om rechten te verlenen:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Vervangen `secure password here` met een beveiligd wachtwoord, dat anders kan zijn dan het `SSH` wachtwoord.

Om deze gebruiker tot gegevens in specifieke gegevensbestanden, lijsten, of kolommen te beperken, kunt u vragen in plaats daarvan in werking stellen GRANT die slechts toegang tot de gegevens toestaan u toelaat.

## De verbinding en gebruikersgegevens invoeren in [!DNL MBI] {#finish}

Om dingen te verpakken, moeten wij de verbinding en gebruikersinformatie ingaan in [!DNL MBI]. Heb je de `MySQL credentials` pagina geopend? Indien niet, ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** en vervolgens het MySQL-pictogram. vergeet niet om de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de sectie Databaseverbinding:

* `Username`: De gebruikersnaam voor de [!DNL MBI] MySQL-gebruiker
* `Password`: Het wachtwoord voor de [!DNL MBI] MySQL-gebruiker
* `Port`: De poort van MySQL op uw server (standaard 3306)
* `Host` Standaard is dit localhost. In het algemeen zal het de bind-adrewaarde voor uw server MySQL zijn, die door gebrek is `127.0.0.1 (localhost)`, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1`) of het openbare IP-adres van uw server.

   U vindt de waarde in uw `my.cnf` bestand (meestal te vinden op `/etc/my.cnf`) onder de regel die leest `\[mysqld\]`. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

In de `SSH Connection` sectie:

* `Remote Address`: Het IP-adres of de hostnaam van de server [!DNL MBI] wordt
* `Username`: De gebruikersnaam voor de [!DNL MBI] SSH-gebruiker (Linux)
* `SSH Port`: SSH-poort op uw server (standaard 22)

Dat is het! Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Verwante:

* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151)
