---
title: MySQL verbinden via een directe verbinding
description: Leer hoe te om  [!DNL MongoDB]  via directe verbinding te verbinden.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Verbinding maken [!DNL MySQL] via directe verbinding

## In dit onderwerp

* [Toestaan toegang tot het  [!DNL Commerce Intelligence]  IP adres](#allowlist)
* [Creeer a [!DNL MySQL]  gebruiker voor  [!DNL Commerce Intelligence]](#steptwo)
* [Verbindingsgegevens invoeren in  [!DNL Commerce Intelligence]](#stepthree)

## Springen naar

* [[!DNL MySQL] via ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] adviseert u [ SSH ](../integrations/mysql-via-ssh-tunnel.md) of één of andere andere vorm van encryptie gebruiken om uw gegevens te beveiligen! Als dit geen optie is, kunt u [!DNL Commerce Intelligence] met uw gegevensbestand nog direct verbinden gebruikend de instructies in dit onderwerp.

In dit onderwerp wordt u door de [!DNL MySQL] -database rechtstreeks verbonden met [!DNL Commerce Intelligence] . Deze instellingen kunnen ook worden gebruikt met [!DNL Adobe Commerce] of andere eCommerce-databases die MySQL gebruiken.

## Toegang tot de IP-adressen van [!DNL Commerce Intelligence] toestaan {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151` , maar ze staan ook op de aanmeldingspagina van [!DNL MySQL] :

![ MBI_Allow_Access_IPs.png ](../../../assets/MBI_allow_access_IPs.png)

## Een [!DNL MySQL] gebruiker voor [!DNL Commerce Intelligence] maken

De eenvoudigste manier om een `MySQL` gebruiker voor [!DNL Commerce Intelligence] te maken, is om de volgende query uit te voeren wanneer u bent aangemeld bij `MySQL` met `GRANT` -bevoegdheden. Vervang `Commerce Intelligence IP Address` door het [!DNL Commerce Intelligence] IP-adres en vervang `secure password` door een beveiligd wachtwoord van uw keuze:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Als u deze gebruiker toegang wilt ontzeggen tot gegevens in specifieke databases, tabellen of kolommen, kunt u in plaats daarvan `GRANT` -query&#39;s uitvoeren die alleen toegang toestaan tot de gegevens die u toestaat.

**hervat de vraag GRANT voor alle vereiste IPs gebruikend de zelfde gebruiker en het wachtwoord.**

## Verbindingsgegevens invoeren in Commerce Intelligence

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] . Hebt u de aanmeldingspagina van [!DNL MySQL] geopend? Als dat niet het geval is, gaat u naar **[!UICONTROL Data** > **Connections]** en klikt u op **[!UICONTROL Add New Data Source]** en klikt u op het pictogram [!DNL MySQL] . Vergeet niet de `Encrypted` -schakeloptie in `Yes` te wijzigen.

Voer de volgende gegevens op deze pagina in, te beginnen met de sectie `Database Connection` :

* `Connection Nickname`: voer een naam in voor de integratie (bijvoorbeeld Ecommerce Store)
* `Username`: De gebruikersnaam voor de gebruiker [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: Het wachtwoord voor de gebruiker [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: Standaard is dit localhost. Over het algemeen is dit de waarde voor het bind-adres van uw [!DNL MySQL] -server, die standaard `127.0.0.1 (localhost)` is, maar ook een lokaal netwerkadres (bijvoorbeeld `192.168.0.1` ) of het openbare IP-adres van uw server kan zijn.

  De waarde staat in het `my.cnf` -bestand (dat zich bevindt op `/etc/my.cnf` ) onder de regel die `\[mysqld\]` leest. Als de bind-adreslijn uit in dat dossier wordt becommentarieerd, wordt uw server beveiligd van buitenverbindingspogingen.

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Gerelateerde documentatie

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
