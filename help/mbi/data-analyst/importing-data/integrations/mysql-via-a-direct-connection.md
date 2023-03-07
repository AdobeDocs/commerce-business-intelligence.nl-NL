---
title: MySQL verbinden via een directe verbinding
description: Leer hoe u verbinding maakt [!DNL MongoDB] via directe verbinding.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Verbinden [!DNL MongoDB] via directe verbinding

## In dit artikel

* [Toegang tot de [!DNL MBI] IP-adres](#allowlist)
* [Een ](#steptwo)
* [Verbindingsgegevens invoeren in [!DNL MBI]](#stepthree)

## Springen naar

* [&quot;MySQL via SSH-tunnel&quot;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [MySQL via cPanel`](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Adobe raadt u aan [SSH](../integrations/mysql-via-ssh-tunnel.md) of een andere vorm van versleuteling om uw gegevens te beveiligen! Als dit geen optie is, kunt u nog steeds rechtstreeks verbinding maken [!DNL MBI] aan uw database toe met behulp van de instructies in dit artikel.

Dit artikel begeleidt u door direct het verbinden van uw gegevensbestand MySQL met [!DNL MBI]. Deze montages kunnen ook met Handel of om het even welke andere gegevensbestanden worden gebruikt eCommerce die MySQL gebruiken.

## Toegang tot de [!DNL MBI] IP-adressen {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151`, maar het staat ook op de MySQL aanmeldingspagina:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Een MySQL-gebruiker maken voor [!DNL MBI]

De eenvoudigste manier om een `MySQL` gebruiker voor [!DNL MBI] moet de volgende query uitvoeren wanneer u bent aangemeld `MySQL` with `GRANT` rechten. Vervangen `MBI IP Address` met de [!DNL MBI] IP-adres en vervangen `secure password` met een beveiligd wachtwoord van uw keuze:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Als u deze gebruiker toegang wilt ontzeggen tot gegevens in specifieke databases, tabellen of kolommen, kunt u in plaats daarvan `GRANT` vragen die alleen toegang geven tot de gegevens die u toestaat.

**Voer de query GRANT voor alle vereiste IP&#39;s opnieuw uit met dezelfde gebruiker en hetzelfde wachtwoord.**

## Verbindingsgegevens invoeren in MBI

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL MBI]. Hebt u de MySQL aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** en vervolgens het MySQL-pictogram. Vergeet niet de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Connection Nickname`: Voer een naam in voor de integratie (bijvoorbeeld Ecommerce Store)
* `Username`: De gebruikersnaam voor de [!DNL MBI] MySQL-gebruiker
* `Password`: Het wachtwoord voor de [!DNL MBI] MySQL-gebruiker
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: Standaard is dit localhost. Over het algemeen is het de bind-adrewaarde voor uw server MySQL, die door gebrek is `127.0.0.1 (localhost)`, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1`) of het openbare IP-adres van uw server.

   U vindt de waarde in uw `my.cnf` bestand (bevindt zich in `/etc/my.cnf`) onder de regel die leest `\[mysqld\]`. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

Dat is het! Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Gerelateerde documentatie

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
