---
title: Het verbinden  [!DNL MySQL]  via de tunnel van SSH
description: Leer hoe te om  [!DNL MySQL]  via de Tunnel van SSH te verbinden.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Verbinden [!DNL MySQL] via [!DNL SSH Tunnel]

* [Wint  [!DNL Commerce Intelligence]  openbare sleutel terug](#retrieve)
* [Toestaan toegang tot het  [!DNL Commerce Intelligence]  IP adres](#allowlist)
* [Een Linux-gebruiker maken voor  [!DNL Commerce Intelligence]](#linux)
* [Creeer a [!DNL MySQL]  gebruiker voor  [!DNL Commerce Intelligence]](#mysql)
* [Ga de verbinding en gebruikersinformatie in  [!DNL Commerce Intelligence]](#finish)

## GA NAAR

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Als u de [!DNL MySQL] -database wilt verbinden met [!DNL Commerce Intelligence] via een `SSH tunnel` , moet u een aantal dingen doen:

1. De lus [!DNL Commerce Intelligence] `public key` ophalen
1. Toegang tot de [!DNL Commerce Intelligence] `IP address` toestaan
1. Een `Linux` gebruiker voor [!DNL Commerce Intelligence] maken
1. Een `MySQL` gebruiker voor [!DNL Commerce Intelligence] maken
1. Voer de verbinding en gebruikersgegevens in [!DNL Commerce Intelligence]


## De openbare sleutel [!DNL Commerce Intelligence] ophalen {#retrieve}

`public key` wordt gebruikt om de gebruiker [!DNL Commerce Intelligence] `Linux` te autoriseren. In de volgende sectie maakt u de gebruiker en importeert u de sleutel.

1. Ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** .
1. Klik op het pictogram `MySQL` .
1. Nadat de pagina `MySQL credentials` is geopend, stelt u de `Encrypted` toggle in op `Yes` . Dit toont de de opstellingsvorm van SSH.
1. De `public key` bevindt zich onder dit formulier.

Laat deze pagina gedurende de zelfstudie open - u hebt deze nodig in de volgende sectie en aan het einde.

Hieronder wordt beschreven hoe u door [!DNL Commerce Intelligence] kunt navigeren om de toets op te halen:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Toegang tot het IP-adres van [!DNL Commerce Intelligence] toestaan {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze staan `54.88.76.97` en `34.250.211.151` , maar ze staan ook op de pagina `MySQL credentials` . Zie de blauwe doos in de GIF hierboven.

## Een [!DNL Linux] gebruiker voor [!DNL Commerce Intelligence] maken {#linux}

Dit kan een productie of secundaire machine zijn, zolang het (of vaak bijgewerkt) gegevens in real time bevat. U kunt [ deze gebruiker ](../../../administrator/account-management/restrict-db-access.md) om het even welke manier beperken u houdt, zolang het het recht behoudt om met de `MySQL` server te verbinden.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Als het `sshd\_config` -bestand dat aan de server is gekoppeld niet is ingesteld op de standaardoptie, hebben alleen bepaalde gebruikers toegang tot de server. Hierdoor wordt een geslaagde verbinding met [!DNL Commerce Intelligence] voorkomen. In deze gevallen is het nodig een opdracht als `AllowUsers` uit te voeren om de `rjmetric` -gebruiker toegang te geven tot de server.

## Een [!DNL MySQL] gebruiker voor [!DNL Commerce Intelligence] maken {#mysql}

Uw organisatie heeft mogelijk een ander proces nodig, maar de eenvoudigste manier om deze gebruiker te maken is om de volgende query uit te voeren wanneer deze is aangemeld bij [!DNL MySQL] als een gebruiker met het recht om rechten toe te kennen:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Vervang `secure password here` door een beveiligd wachtwoord, dat anders kan zijn dan het wachtwoord van `SSH` .

Om deze gebruiker tot gegevens in specifieke gegevensbestanden, lijsten, of kolommen te beperken, kunt u vragen in plaats daarvan in werking stellen GRANT die slechts toegang tot de gegevens toestaan u toelaat.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] . Hebt u de pagina `MySQL credentials` open gelaten? Als dat niet het geval is, gaat u naar **[!UICONTROL Data** > **Connections]** en klikt u op **[!UICONTROL Add New Data Source]** , gevolgd door het pictogram [!DNL MySQL] . Vergeet niet de `Encrypted` -schakeloptie in te stellen op `Yes` .

Voer de volgende gegevens op deze pagina in, te beginnen met de sectie `Database Connection` :

* `Username`: De gebruikersnaam voor de gebruiker [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: Het wachtwoord voor de gebruiker [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: [!DNL MySQL] poort op de server (standaard 3306)
* `Host` Standaard is dit localhost. Over het algemeen is dit de waarde voor het bind-adres van uw [!DNL MySQL] -server, die standaard `127.0.0.1 (localhost)` is, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1` ) of het openbare IP-adres van uw server kan zijn.

  De waarde staat in het `my.cnf` -bestand (dat zich bevindt op `/etc/my.cnf` ) onder de regel die `\[mysqld\]` leest. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

In de sectie `SSH Connection` :

* `Remote Address`: Het IP-adres of de hostnaam van de server [!DNL Commerce Intelligence] wordt via een tunnel verzonden naar
* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] SSH ([!DNL Linux])-gebruiker
* `SSH Port`: SSH-poort op uw server (standaard 22)

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Verwante:

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
