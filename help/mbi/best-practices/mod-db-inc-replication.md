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

De `Modified At` -methode, de meest ideale replicatiemethode, gebruikt een `datetime` -kolom om nieuwe en/of bijgewerkte gegevens te detecteren. Onthoud dat de kolom `datetime` in tabellen die deze methode gebruiken, moet worden geïndexeerd en op geen enkel moment null-waarden kan bevatten.

Als de tabel geen kolom `datetime` bevat, kunt u een kolom met de index `modified at` toevoegen. Null-waarden zijn niet toegestaan in een kolom `modified at` . Controleer of de kolom voor elke rij is gevuld.

Om ervoor te zorgen dat de methode `Modified At` naar behoren werkt, kunt u geen rijen uit de tabel verwijderen. In plaats daarvan moet u de rij als ongeldig markeren door een kolom `deleted` aan de tabel toe te voegen. Deze kolom retourneert een `1` als de rij ongeldig is, anders `0` . U kunt deze kolom dan gebruiken om ongeldige rijen uit te filteren wanneer u metriek en rapporten bouwt.

## Wijzigingen voor de enkelvoudige sneltoets

Als de methode `Modified At` niet kan worden ingeschakeld, is de op een na beste optie Eén automatische incrementele sleutel. Nieuwe gegevens worden in tabellen gevonden met deze methode door te zoeken naar waarden voor primaire sleutels die hoger zijn dan de huidige hoogste waarde in de Data Warehouse.

Tabellen die deze methode gebruiken, zijn één kolom met een geheel getal die de primaire sleutels automatisch verhoogt. Als u deze methode in uw database wilt gebruiken, brengt u de volgende wijzigingen aan:

* Als de primaire sleutel een samengestelde sleutel of een niet-geheel is, wijzigt u de primaire sleutel in een automatisch toenemend geheel getal
* Als de primaire sleutel één kolom met gehele getallen is maar sleutels niet opeenvolgend kunnen worden toegewezen, wijzigt u de primaire sleutel in automatisch verhogen

## Omloop omhoog

Door kleine wijzigingen in uw tabellen aan te brengen, kunt u de snellere, efficiëntere methoden voor incrementele replicatie benutten. Nochtans, als dit niet mogelijk is, kunt u andere stappen nog nemen om [&#x200B; uw updatetijd &#x200B;](../best-practices/reduce-update-cycle-time.md) te verminderen en [&#x200B; uw gegevensbestand &#x200B;](../best-practices/opt-db-analysis.md) te optimaliseren.
