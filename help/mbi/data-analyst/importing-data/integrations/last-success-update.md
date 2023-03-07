---
title: Begrijp resultaten tussen Gegevensbestand en SQL Redacteur
description: Leer resultaten te begrijpen tussen database en SQL editor.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Resultaten van databases vs `SQL Editor` Resultaten

U bent misschien nieuwsgierig naar de `Last successful update began` veld bevindt zich in uw `Integrations` pagina:

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Begrijp het `timestamp` field

Het laat het begin zien `timestamp` (in de tijdzone die op uw account is ingesteld) van de _laatste voltooide updatecyclus_ op uw account.

- Als een van de gesynchroniseerde tabellen tijdens de laatste updatecyclus een probleem heeft aangetroffen, is deze tijdstempel *niet bijgewerkt*.
- Er kunnen zich dus gevallen voordoen waarin de verslagen met nieuwe gegevens zijn bijgewerkt, maar de *Laatste succesvolle update is gestart* is nog steeds achterop.

## Identificeer het &quot;echte&quot;laatste gegevenspunt

Het meest recente gegevenspunt voor een bepaalde integratie wordt bepaald door de `Last Data Point Received` `timestamp` rechts van elke integratie. Die timestamp verwijst naar het laatste punt waarop uw Data Warehouse met succes gegevenspunten van die bron ontving, of het een gegevensbestand, API, of derdenintegratie was.

Controleren op versheid van gegevens van *specifieke tabellen*, raadt Adobe u aan snel [SQL-rapport](../../dev-reports/sql-rpt-bldr.md) die een `MAX(timestamp)` op de belangrijkste tabel van uw account. Deze tijdstempel vergelijken met de `Last Data Point` Hiermee wordt aangegeven of de uitgave invloed heeft op de gehele account of op een subset van de tabellen. Adobe raadt u aan dit voor drie tot vier belangrijke, veelgebruikte tabellen te doen.

- Als de `MAX(timestamp)` waarden zijn recenter dan `Last Data Point Received`, betekent dit dat een subset van de tabellen werd beïnvloed, maar dat de updatecyclus van de gehele account stabiel is.
- Als de `MAX(timestamp)` waarden zijn gelijk aan of eerder `Last Data Point Received`, betekent dit dat de updatecyclus van de account is beïnvloed. In deze situatie [een ondersteuningsticket indienen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
