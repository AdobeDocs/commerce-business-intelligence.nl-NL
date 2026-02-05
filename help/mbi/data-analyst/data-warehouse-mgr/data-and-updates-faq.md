---
title: Gegevens en updates
description: Leer hoe u de status van uw updatecyclus kunt controleren.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: db93e5284950fa9336d0833af24589754c94a8b3
workflow-type: tm+mt
source-wordcount: '481'
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

De grafiekwaarden kunnen de hele dag veranderen als er nieuwe gegevens worden gesynchroniseerd met uw Data Warehouse. Ook, kunnen de waarden voor bestaande gegevenskolommen toe te schrijven aan [&#x200B; rechecks &#x200B;](../data-warehouse-mgr/cfg-data-rechecks.md) veranderen. Een nieuwe controle is een proces waarin wordt gezocht naar gewijzigde waarden in gegevenskolommen, zoals een ordestatus die zich van `open` naar `shipped` beweegt.

Er zijn een paar verschillende manieren [&#x200B; om het statuut van uw updatecyclus &#x200B;](../../best-practices/check-update-cycle.md), afhankelijk van de de toestemmingsmontages van de gebruiker te controleren:

* **[!UICONTROL Read-Only]en [!UICONTROL Standard] Gebruikers** - kan de muisaanwijzer boven het pictogram rechtsboven op de pagina houden om te zien wanneer het laatste gegevenspunt is getrokken.
* **[!UICONTROL Admin]Gebruikers** - Kan het laatste gegevenspunt en statuspictogram voor accountintegratie weergeven. Navigeer voor meer informatie naar **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** om de huidige updatestatus en het tijdstip van de laatste voltooide update weer te geven.
* **API Methode** - kan de meest recente voltooide updatecyclus terugwinnen gebruikend de Status API van de Cyclus van de Update.

Voor volledige details bij het controleren van uw status van de updatecyclus, zie [&#x200B; Controlerend de Status van de Cyclus van de Update &#x200B;](../../best-practices/check-update-cycle.md).

## Wat is het verschil tussen een regelmatige en gedwongen update? {#regularforcedupdates}

De regelmatige updates zijn **geplande** processen terwijl de gedwongen updates **handprocessen zijn die door u** worden in werking gesteld. Als u brainstormuren hebt (of een periode waarin [!DNL Commerce Intelligence] uw gegevens niet moet bijwerken), wordt met het dwingen van een update een cyclus gestart die niet voldoet aan de beperkingen van de brainstormperiode.

## Waarom duurt de updatecyclus lang? {#updatecycletime}

Talrijke factoren kunnen aan een reeds lange updatetijd toevoegen. Bepaalde [&#x200B; replicatiemethodes &#x200B;](../data-warehouse-mgr/cfg-replication-methods.md), [&#x200B; hogere recheck frequenties &#x200B;](../data-warehouse-mgr/cfg-data-rechecks.md), en het aantal dashboards en grafieken zijn enkel een paar contribuanten. Adobe adviseert [&#x200B; het aanpassen van sommige van uw montages &#x200B;](../../best-practices/reduce-update-cycle-time.md) en [&#x200B; het optimaliseren van uw gegevensbestand voor analyse &#x200B;](../../best-practices/opt-db-analysis.md) om updatetijden te verminderen.

## Kan ik op de hoogte worden gesteld wanneer een updatecyclus is voltooid? {#notifyupdate}

Als er een update wordt uitgevoerd, staat er een koppeling op de pagina **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** waarmee u een e-mailmelding kunt aanvragen zodra de cyclus is voltooid. Als er geen update wordt uitgevoerd, ziet u een koppeling waarmee een update wordt geforceerd om te starten.

## Waarom is [!DNL Google ECommerce] gegevens verschillend van mijn gegevensbestand? {#ecommdatabase}

Er kunnen verschillende oorzaken zijn voor verschillen tussen [!DNL Google Analytics] en uw database. Het volgen wordt niet correct toegelaten, gebruikers die incognito bezoeken, en gebeurtenissen klikken die niet correct werken zijn slechts een paar voorbeelden. Als uw opbrengst en de orden niet goed kijken, [&#x200B; zie dit onderwerp &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) om een probleem te diagnostiseren.

## Hoe los ik een gegevensdiscrepantie problemen op? {#datadiscrepancy}

Adobe weet dat inconsistente gegevens een frustrerende ervaring kunnen zijn. Probeer gebruikend de [&#x200B; Controlelijst van de Discretie van Gegevens &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) of [&#x200B; Gegevens voert leerprogramma &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) uit om het probleem te diagnostiseren. Als u nog wordt tegengehouden, [&#x200B; contactsteun &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
