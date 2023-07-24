---
title: Het wijzigen van Uw Gegevensbestand aan Steun voor Incrementele Replicatie
description: Leer hoe u uw database kunt aanpassen om incrementele replicatie te ondersteunen.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Ondersteuning voor incrementele replicatie

Als uw lijsten momenteel niet voor stijgende replicatie toestaan, verwijs naar de volgende aanbevelingen voor mogelijke oplossingen.

## Wijzigingen voor gewijzigd bij

De `Modified At` de methode, die de meest ideale replicatiemethode is, gebruikt een `datetime` om nieuwe en/of bijgewerkte gegevens te detecteren. Vergeet niet dat de `datetime` de kolom in lijsten die deze methode gebruiken moet worden geïndexeerd en kan op geen enkel ogenblik ongeldige waarden bevatten.

Als uw tabel geen `datetime` kolom, kunt u een index toevoegen `modified at` kolom. Null-waarden zijn niet toegestaan in een `modified at` kolom. Controleer of de kolom voor elke rij is gevuld.

Om ervoor te zorgen dat `Modified At` de methode werkt zoals bedoeld, kunt u geen rijen uit de tabel verwijderen. In plaats daarvan moet u de rij als ongeldig markeren door een `deleted` aan de tabel. Deze kolom retourneert een `1` als de rij ongeldig is en `0` anders. U kunt deze kolom dan gebruiken om ongeldige rijen uit te filteren wanneer u metriek en rapporten bouwt.

## Wijzigingen voor de enkelvoudige sneltoets

Als de `Modified At` De methode kan niet worden toegelaten, dan is de Enige Auto het Toename Primaire Sleutel de volgende beste optie. Nieuwe gegevens worden in tabellen gevonden met deze methode door te zoeken naar waarden voor primaire sleutels die hoger zijn dan de huidige hoogste waarde in de Data Warehouse.

Tabellen die deze methode gebruiken, zijn één kolom met een geheel getal die de primaire sleutels automatisch verhoogt. Als u deze methode in uw database wilt gebruiken, brengt u de volgende wijzigingen aan:

* Als de primaire sleutel een samengestelde sleutel of een niet-geheel is, wijzigt u de primaire sleutel in een automatisch toenemend geheel getal
* Als de primaire sleutel één kolom met gehele getallen is maar sleutels niet opeenvolgend kunnen worden toegewezen, wijzigt u de primaire sleutel in automatisch verhogen

## Omloop omhoog

Door kleine wijzigingen in uw tabellen aan te brengen, kunt u de snellere, efficiëntere methoden voor incrementele replicatie benutten. Als dit echter niet mogelijk is, kunt u nog andere stappen ondernemen om [verkort uw updatetijd](../best-practices/reduce-update-cycle-time.md) en [uw database optimaliseren](../best-practices/opt-db-analysis.md).
