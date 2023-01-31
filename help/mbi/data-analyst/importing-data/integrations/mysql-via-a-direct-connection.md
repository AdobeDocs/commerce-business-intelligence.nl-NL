---
title: MySQL verbinden via een directe verbinding
description: Leer hoe u verbinding maakt [!DNL MongoDB] via directe verbinding.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '403'
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
>We raden u sterk aan [SSH](../integrations/mysql-via-ssh-tunnel.md) of een andere vorm van versleuteling om uw gegevens te beveiligen! Als dit geen optie is, kunt u nog steeds rechtstreeks verbinding maken [!DNL MBI] aan uw database toe met behulp van de instructies in dit artikel.

In dit artikel, lopen wij u door uw gegevensbestand MySQL rechtstreeks aan te sluiten [!DNL MBI]. Deze montages kunnen ook met Handel of om het even welke andere gegevensbestanden worden gebruikt eCommerce die MySQL gebruiken.

## Toegang tot de [!DNL MBI] IP-adressen {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf onze IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151`, maar het staat ook op de MySQL aanmeldingspagina:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Een MySQL-gebruiker maken voor [!DNL MBI]

De eenvoudigste manier om een `MySQL` gebruiker voor [!DNL MBI] moet de volgende query uitvoeren wanneer u bent aangemeld `MySQL` with `GRANT` rechten. Vervangen `MBI IP Address` met de [!DNL MBI] IP-adres en vervangen `secure password` met een beveiligd wachtwoord van uw keuze:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Als u deze gebruiker toegang wilt ontzeggen tot gegevens in specifieke databases, tabellen of kolommen, kunt u in plaats daarvan `GRANT` vragen die alleen toegang geven tot de gegevens die u toestaat.

**Voer de query GRANT voor alle vereiste IP&#39;s opnieuw uit met dezelfde gebruiker en hetzelfde wachtwoord.**

## Verbindingsgegevens invoeren in MBI

Om dingen te verpakken, moeten wij de verbinding en gebruikersinformatie ingaan in [!DNL MBI]. Hebt u de MySQL aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** en vervolgens het MySQL-pictogram. Vergeet niet de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Connection Nickname`: Voer een naam in voor de integratie (bijvoorbeeld Ecommerce Store)
* `Username`: De gebruikersnaam voor de [!DNL MBI] MySQL-gebruiker
* `Password`: Het wachtwoord voor de [!DNL MBI] MySQL-gebruiker
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: Standaard is dit localhost. In het algemeen zal het de bind-adrewaarde voor uw server MySQL zijn, die door gebrek is `127.0.0.1 (localhost)`, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1`) of het openbare IP-adres van uw server.

   U vindt de waarde in uw `my.cnf` bestand (meestal te vinden op `/etc/my.cnf`) onder de regel die leest `\[mysqld\]`. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

Dat is het! Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Gerelateerde documentatie

* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151)
