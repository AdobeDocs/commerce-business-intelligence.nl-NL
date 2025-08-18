---
title: Gegevens en updates
description: Leer hoe u de status van uw updatecyclus kunt controleren.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Gegevens en updates

* [Waarom zijn mijn gegevens gewijzigd?](#datachange)
* [Wat is het verschil tussen een regelmatige en gedwongen update?](#regularforcedupdates)
* [Waarom duurt de updatecyclus lang?](#updatecycletime)
* [Kan ik op de hoogte worden gesteld wanneer een updatecyclus is voltooid?](#notifyupdate)
* [Waarom is  [!DNL Google ECommerce]  gegevens verschillend van mijn gegevensbestand?](#ecommdatabase)
* [Hoe los ik een gegevensdiscrepantie problemen op?](#datadiscrepancy)

## Waarom zijn mijn gegevens gewijzigd? {#datachange}

De grafiekwaarden kunnen de hele dag veranderen als er nieuwe gegevens worden gesynchroniseerd met uw Data Warehouse. Ook, kunnen de waarden voor bestaande gegevenskolommen toe te schrijven aan [ rechecks ](../data-warehouse-mgr/cfg-data-rechecks.md) veranderen. Een nieuwe controle is een proces waarin wordt gezocht naar gewijzigde waarden in gegevenskolommen, zoals een ordestatus die zich van `open` naar `shipped` beweegt.

Er zijn een paar verschillende manieren [ om het statuut van uw updatecyclus ](../../best-practices/check-update-cycle.md), afhankelijk van de de toestemmingsmontages van de gebruiker te controleren.

## Wat is het verschil tussen een regelmatige en gedwongen update? {#regularforcedupdates}

De regelmatige updates zijn **geplande** processen terwijl de gedwongen updates **handprocessen zijn die door u** worden in werking gesteld. Als u brainstormuren hebt (of een periode waarin [!DNL Commerce Intelligence] uw gegevens niet moet bijwerken), wordt met het dwingen van een update een cyclus gestart die niet voldoet aan de beperkingen van de brainstormperiode.

## Waarom duurt de updatecyclus lang? {#updatecycletime}

Talrijke factoren kunnen aan een reeds lange updatetijd toevoegen. Bepaalde [ replicatiemethodes ](../data-warehouse-mgr/cfg-replication-methods.md), [ hogere recheck frequenties ](../data-warehouse-mgr/cfg-data-rechecks.md), en het aantal dashboards en grafieken zijn enkel een paar contribuanten. Adobe adviseert [ het aanpassen van sommige van uw montages ](../../best-practices/reduce-update-cycle-time.md) en [ het optimaliseren van uw gegevensbestand voor analyse ](../../best-practices/opt-db-analysis.md) om updatetijden te verminderen.

## Kan ik op de hoogte worden gesteld wanneer een updatecyclus is voltooid? {#notifyupdate}

Als er een update wordt uitgevoerd, staat er een koppeling op de pagina `Connections` waarmee u een e-mailmelding kunt aanvragen zodra de cyclus is voltooid.

## Waarom is [!DNL Google ECommerce] gegevens verschillend van mijn gegevensbestand? {#ecommdatabase}

Er kunnen verschillende oorzaken zijn voor verschillen tussen [!DNL Google Analytics] en uw database. Het volgen wordt niet correct toegelaten, gebruikers die incognito bezoeken, en gebeurtenissen klikken die niet correct werken zijn slechts een paar voorbeelden. Als uw opbrengst en de orden niet goed kijken, [ zie dit onderwerp ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=nl-NL) om een probleem te diagnostiseren.

## Hoe los ik een gegevensdiscrepantie problemen op? {#datadiscrepancy}

Adobe weet dat inconsistente gegevens een frustrerende ervaring kunnen zijn. Probeer gebruikend de [ Controlelijst van de Discretie van Gegevens ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=nl-NL) of [ Gegevens voert leerprogramma ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=nl-NL) uit om het probleem te diagnostiseren. Als u nog wordt tegengehouden, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL).
