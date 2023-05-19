---
title: Verbinding maken [!DNL MySQL] via SSH-tunnel
description: Leer hoe u verbinding maakt [!DNL MySQL] via SSH-tunnel.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Verbinden [!DNL MySQL] via [!DNL SSH Tunnel]

* [De [!DNL Commerce Intelligence] openbare sleutel](#retrieve)
* [Toegang tot de [!DNL Commerce Intelligence] IP-adres](#allowlist)
* [Een Linux-gebruiker maken voor [!DNL Commerce Intelligence]](#linux)
* [Een [!DNL MySQL] gebruiker voor [!DNL Commerce Intelligence]](#mysql)
* [Voer de verbinding en gebruikersgegevens in [!DNL Commerce Intelligence]](#finish)

## GA NAAR

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Als u verbinding wilt maken met uw [!DNL MySQL] database naar [!DNL Commerce Intelligence] via een `SSH tunnel`, moet u een paar dingen doen:

1. De [!DNL Commerce Intelligence] `public key`
1. Toegang tot de [!DNL Commerce Intelligence] `IP address`
1. Een `Linux` gebruiker voor [!DNL Commerce Intelligence]
1. Een `MySQL` gebruiker voor [!DNL Commerce Intelligence]
1. Voer de verbinding en gebruikersgegevens in [!DNL Commerce Intelligence]


## De [!DNL Commerce Intelligence] openbare sleutel {#retrieve}

De `public key` wordt gebruikt om de [!DNL Commerce Intelligence] `Linux` gebruiker. In de volgende sectie maakt u de gebruiker en importeert u de sleutel.

1. Ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]**.
1. Klik op de knop `MySQL` pictogram.
1. Na de `MySQL credentials` pagina wordt geopend, stelt u de `Encrypted` schakelen naar `Yes`. Dit toont de de opstellingsvorm van SSH.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Hieronder wordt beschreven hoe u kunt navigeren [!DNL Commerce Intelligence] om de sleutel op te halen:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Toegang tot de [!DNL Commerce Intelligence] IP-adres {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151` maar ze staan ook op de agenda `MySQL credentials` pagina. Zie de blauwe doos in het bovenstaande GIF.

## Een [!DNL Linux] gebruiker voor [!DNL Commerce Intelligence] {#linux}

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt [deze gebruiker beperken](../../../administrator/account-management/restrict-db-access.md) op elke gewenste manier, zolang het recht behoudt om verbinding te maken met het `MySQL` server.

1. Als u de nieuwe gebruiker wilt toevoegen, voert u de volgende opdrachten als hoofdmap uit op uw [!DNL Linux] server:

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Als de `sshd\_config` het bestand dat aan de server is gekoppeld, is niet ingesteld op de standaardoptie. Alleen bepaalde gebruikers hebben toegang tot de server. Hierdoor wordt een verbinding met [!DNL Commerce Intelligence]. In deze gevallen is het nodig om een opdracht als `AllowUsers` de `rjmetric` gebruikerstoegang tot de server.

## Een [!DNL MySQL] gebruiker voor [!DNL Commerce Intelligence] {#mysql}

Uw organisatie kan een verschillend proces vereisen, maar de eenvoudigste manier om deze gebruiker tot stand te brengen is de volgende vraag uit te voeren wanneer het programma wordt geopend in [!DNL MySQL] als gebruiker met het recht om rechten te verlenen:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Vervangen `secure password here` met een beveiligd wachtwoord, dat kan verschillen van het `SSH` wachtwoord.

Om deze gebruiker tot gegevens in specifieke gegevensbestanden, lijsten, of kolommen te beperken, kunt u vragen in plaats daarvan in werking stellen GRANT die slechts toegang tot de gegevens toestaan u toelaat.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]. Heb je de `MySQL credentials` pagina geopend? Indien niet, ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** en de [!DNL MySQL] pictogram. Vergeet niet de instelling van de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: Het wachtwoord voor de [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: [!DNL MySQL] poort op de server (standaard 3306)
* `Host` Standaard is dit localhost. In het algemeen is het de bind-adrewaarde voor uw [!DNL MySQL] server, die standaard `127.0.0.1 (localhost)`, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1`) of het openbare IP-adres van uw server.

   U vindt de waarde in uw `my.cnf` bestand (bevindt zich in `/etc/my.cnf`) onder de regel die leest `\[mysqld\]`. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

In de `SSH Connection` sectie:

* `Remote Address`: Het IP-adres of de hostnaam van de server [!DNL Commerce Intelligence] wordt
* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] SSH ([!DNL Linux]) gebruiker
* `SSH Port`: SSH-poort op uw server (standaard 22)

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Verwante:

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
