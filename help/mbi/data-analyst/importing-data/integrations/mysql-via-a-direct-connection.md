---
title: MySQL verbinden via een directe verbinding
description: Leer hoe u verbinding maakt [!DNL MongoDB] via directe verbinding.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Verbinden [!DNL MySQL] via directe verbinding

## In dit onderwerp

* [Toegang tot de [!DNL Commerce Intelligence] IP-adres](#allowlist)
* [Een [!DNL MySQL] gebruiker voor [!DNL Commerce Intelligence]](#steptwo)
* [Verbindingsgegevens invoeren in [!DNL Commerce Intelligence]](#stepthree)

## Springen naar

* [[!DNL MySQL] via ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] raadt u aan [SSH](../integrations/mysql-via-ssh-tunnel.md) of een andere vorm van versleuteling om uw gegevens te beveiligen! Als dit geen optie is, kunt u nog steeds rechtstreeks verbinding maken [!DNL Commerce Intelligence] aan uw gegevensbestand gebruikend de instructies in dit onderwerp.

Dit onderwerp loopt u door het rechtstreeks verbinden van uw [!DNL MySQL] database naar [!DNL Commerce Intelligence]. U kunt deze instellingen ook gebruiken met [!DNL Adobe Commerce] of andere eCommerce-databases die MySQL gebruiken.

## Toegang tot de [!DNL Commerce Intelligence] IP-adressen {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151`, maar het is ook [!DNL MySQL] aanmeldingspagina:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Een [!DNL MySQL] gebruiker voor [!DNL Commerce Intelligence]

De eenvoudigste manier om een `MySQL` gebruiker voor [!DNL Commerce Intelligence] moet de volgende query uitvoeren wanneer u bent aangemeld `MySQL` with `GRANT` rechten. Vervangen `Commerce Intelligence IP Address` met de [!DNL Commerce Intelligence] IP-adres en vervangen `secure password` met een beveiligd wachtwoord van uw keuze:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Als u deze gebruiker toegang wilt ontzeggen tot gegevens in specifieke databases, tabellen of kolommen, kunt u in plaats daarvan `GRANT` vragen die alleen toegang geven tot de gegevens die u toestaat.

**Voer de query GRANT voor alle vereiste IP&#39;s opnieuw uit met dezelfde gebruiker en hetzelfde wachtwoord.**

## Verbindingsgegevens invoeren in inlichtingen over handel

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]. Heb je de [!DNL MySQL] aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** klikt u op de knop [!DNL MySQL] pictogram. Vergeet niet de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Connection Nickname`: Voer een naam in voor de integratie (bijvoorbeeld Ecommerce Store)
* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: Het wachtwoord voor de [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: Standaard is dit localhost. In het algemeen is het de bind-adrewaarde voor uw [!DNL MySQL] server, die standaard `127.0.0.1 (localhost)`, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1`) of het openbare IP-adres van uw server.

   U vindt de waarde in uw `my.cnf` bestand (bevindt zich in `/etc/my.cnf`) onder de regel die leest `\[mysqld\]`. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Gerelateerde documentatie

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
