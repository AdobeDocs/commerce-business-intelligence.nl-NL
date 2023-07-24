---
title: Gegevens en updates
description: Leer hoe u de status van uw updatecyclus kunt controleren.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Gegevens en updates

* [Waarom zijn mijn gegevens gewijzigd?](#datachange)
* [Wat is het verschil tussen een regelmatige en gedwongen update?](#regularforcedupdates)
* [Waarom duurt de updatecyclus lang?](#updatecycletime)
* [Kan ik op de hoogte worden gesteld wanneer een updatecyclus is voltooid?](#notifyupdate)
* [Waarom [!DNL Google ECommerce] andere gegevens dan mijn database?](#ecommdatabase)
* [Hoe los ik een gegevensdiscrepantie problemen op?](#datadiscrepancy)

## Waarom zijn mijn gegevens gewijzigd? {#datachange}

De waarden van de grafiek kunnen door de dag veranderen toe te schrijven aan nieuwe gegevens die aan uw Data Warehouse worden gesynchroniseerd. Ook kunnen waarden voor bestaande gegevenskolommen veranderen als gevolg van [hercontroles](../data-warehouse-mgr/cfg-data-rechecks.md). Een nieuwe controle is een proces dat op veranderde waarden in gegevenskolommen zoals een ordestatus zoekt die zich van `open` tot `shipped`.

Er zijn een paar verschillende manieren [om de status van uw updatecyclus te controleren](../../best-practices/check-update-cycle.md), afhankelijk van de machtigingsinstellingen van de gebruiker.

## Wat is het verschil tussen een regelmatige en gedwongen update? {#regularforcedupdates}

Normale updates zijn **gepland** processen terwijl geforceerde updates **handmatige processen die door u zijn gestart**. Als u brainstormuren hebt (of een periode waarin [!DNL Commerce Intelligence] moet uw gegevens niet bijwerken), door een update te forceren wordt een cyclus gestart die niet voldoet aan de beperkingen van de uitvalperiode.

## Waarom duurt de updatecyclus lang? {#updatecycletime}

Talrijke factoren kunnen aan een reeds lange updatetijd toevoegen. Bepaalde [replicatiemethoden](../data-warehouse-mgr/cfg-replication-methods.md), [hogere recheck frequenties](../data-warehouse-mgr/cfg-data-rechecks.md)En het aantal dashboards en grafieken zijn slechts een paar contribuanten. Adobe beveelt aan [het aanpassen van sommige montages](../../best-practices/reduce-update-cycle-time.md) en [uw database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md) om de updatetijden te verminderen.

## Kan ik op de hoogte worden gesteld wanneer een updatecyclus is voltooid? {#notifyupdate}

Als er een update wordt uitgevoerd, staat er een koppeling op het tabblad `Connections` pagina die u kunt gebruiken om een e-mailbericht aan te vragen zodra de cyclus is voltooid.

## Waarom[!DNL Google ECommerce]andere gegevens dan mijn database? {#ecommdatabase}

Verschillen tussen [!DNL Google Analytics] en uw database kan om verschillende redenen ontstaan. Het volgen wordt niet correct toegelaten, gebruikers die incognito bezoeken, en gebeurtenissen klikken die niet correct werken zijn slechts een paar voorbeelden. Als uw inkomsten en bestellingen er niet goed uitzien, [zie dit onderwerp](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) om een probleem te diagnostiseren.

## Hoe los ik een gegevensdiscrepantie problemen op? {#datadiscrepancy}

Adobe weet dat het zien van inconsistente gegevens een frustrerende ervaring kan zijn. Probeer de [Controlelijst voor gegevensdiscrepantie](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) of [Zelfstudie voor gegevensuitvoer](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) om het probleem te diagnostiseren. Als u nog steeds vastzit, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
