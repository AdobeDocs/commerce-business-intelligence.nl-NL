---
title: Gegevens en updates
description: Leer hoe u de status van uw updatecyclus kunt controleren.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '401'
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

De waarden van de grafiek kunnen door de dag veranderen toe te schrijven aan nieuwe gegevens die aan uw gegevenspakhuis worden gesynchroniseerd. Bovendien kunnen waarden voor bestaande gegevenskolommen veranderen als gevolg van [hercontroles](../data-warehouse-mgr/cfg-data-rechecks.md). Een nieuwe controle is een proces dat zoekt naar gewijzigde waarden in gegevenskolommen, bijvoorbeeld een orderstatus die overgaat van `open` tot `shipped`.

Er zijn een paar verschillende manieren [om de status van uw updatecyclus te controleren](../../best-practices/check-update-cycle.md), afhankelijk van het type gebruikersmachtigingen dat u hebt.

## Wat is het verschil tussen een regelmatige en gedwongen update? {#regularforcedupdates}

Normale updates zijn **gepland** processen terwijl geforceerde updates **handmatige processen die door u zijn gestart**. Als u brainstormuren hebt - of een periode waarin [!DNL MBI] moet uw gegevens niet bijwerken - door een update af te dwingen, wordt een cyclus gestart die niet voldoet aan de beperkingen van de periode van stroomuitval.

## Waarom duurt de updatecyclus lang? {#updatecycletime}

Veel factoren kunnen een reeds lange updatetijd vergroten. Bepaalde [replicatiemethoden](../data-warehouse-mgr/cfg-replication-methods.md), [hogere recheck frequenties](../data-warehouse-mgr/cfg-data-rechecks.md)En het aantal dashboards en grafieken zijn slechts een paar contribuanten. We raden aan [het aanpassen van sommige montages](../../best-practices/reduce-update-cycle-time.md) en [uw database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md) om de updatetijden te verminderen.

## Kan ik op de hoogte worden gesteld wanneer een updatecyclus is voltooid? {#notifyupdate}

Absoluut! Als er een update wordt uitgevoerd, wordt er een koppeling weergegeven op het tabblad `Connections` pagina die u kunt gebruiken om een e-mailbericht aan te vragen zodra de cyclus is voltooid.

## Waarom[!DNL Google ECommerce]andere gegevens dan mijn database? {#ecommdatabase}

Verschillen tussen [!DNL Google Analytics] en uw database kan om een aantal redenen ontstaan. Het volgen wordt niet correct toegelaten, gebruikers die incognito bezoeken, en gebeurtenissen klikken die niet correct werken zijn slechts een paar voorbeelden. Als uw inkomsten en bestellingen er niet helemaal goed uitzien, [dit artikel gebruiken](https://support.magento.com/hc/en-us/articles/360016505232) om het probleem te diagnostiseren.

## Hoe los ik een gegevensdiscrepantie problemen op? {#datadiscrepancy}

We weten dat inconsistente gegevens een frustrerende ervaring kunnen zijn. Probeer onze [Controlelijst voor gegevensdiscrepantie](https://support.magento.com/hc/en-us/articles/360016731271) of [Zelfstudie voor gegevensuitvoer](https://support.magento.com/hc/en-us/articles/360016730631) om het probleem te diagnostiseren. Als u nog steeds vastzit, [contactondersteuning](../../guide-overview.md).
