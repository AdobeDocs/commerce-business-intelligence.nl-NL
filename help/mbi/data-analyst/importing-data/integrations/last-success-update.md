---
title: Begrijp resultaten tussen Gegevensbestand en SQL Redacteur
description: Leer resultaten te begrijpen tussen database en SQL editor.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Resultaten database versus [!DNL SQL Editor] resultaten

Mogelijk bent u nieuwsgierig wat het veld `Last successful update began` in de `Integrations` -pagina staat:

![ Last_success_update.png ](../../../assets/Last_successful_update.png)

## Het veld `timestamp` begrijpen

Het toont het begin `timestamp` (in timezone die op uw rekening wordt geplaatst) van de _laatste succesvolle updatecyclus_ op uw rekening.

- Als om het even welke gesynchroniseerde lijsten een kwestie tijdens de laatste updatecyclus tegenkwamen, wordt dit timestamp niet bijgewerkt **.
- Vandaar, kunnen er gevallen zijn wanneer de rapporten met nieuwe gegevens zijn bijgewerkt, maar de *Laatste succesvolle update begon* is nog achterblijvend.

## Identificeer het &quot;echte&quot;laatste gegevenspunt

Het meest recente gegevenspunt voor een bepaalde integratie wordt bepaald door de `Last Data Point Received` tijdstempel rechts van elke integratie. Die timestamp verwijst naar het laatste punt waarop uw Data Warehouse met succes gegevenspunten van die bron ontving, of het een gegevensbestand, API, of derdenintegratie was.

Om voor versheid van gegevens van *specifieke lijsten* te controleren, adviseert de Adobe het creëren van een snel [[!DNL SQL]  rapport ](../../dev-reports/sql-rpt-bldr.md) dat a `MAX(timestamp)` op de belangrijkste lijst op uw rekening uitvoert. Wanneer u deze tijdstempel vergelijkt met de `Last Data Point` , wordt aangegeven of de uitgave van invloed is op de gehele account of op een subset van de tabellen. De Adobe beveelt aan dit voor drie tot vier belangrijke, algemeen gebruikte lijsten te doen.

- Als de `MAX(timestamp)` -waarden recenter zijn dan `Last Data Point Received` , heeft dit invloed op een subset van de tabellen, maar is de updatecyclus van de account in zijn geheel stabiel.
- Als de `MAX(timestamp)` -waarden gelijk zijn aan of voor `Last Data Point Received` , heeft dit invloed op de updatecyclus van de account. In deze situatie, [ voorlegt een steunkaartje ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL).
