---
title: Gegevensmigratieservices
description: Leer alles wat u nodig hebt om een aanvraag in te dienen en aan de slag te gaan met de migratie.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Gegevensmigratie

Het migreren naar een nieuw gegevensbestandschema, de server, of het melden van gegevensbestand hoeft niet stressvol te zijn. Ons **[!DNL Adobe Commerce Services - Analytics]** team biedt migratiehulp - wij doen al het zware heft zodat u niet hoeft te hoeven.

Om ervoor te zorgen dat de overgang zo soepel mogelijk verloopt, vragen we u om uw migratieverzoek zo gedetailleerd mogelijk in te dienen. In dit artikel staat alles wat u nodig hebt om een aanvraag in te dienen en aan de migratie te beginnen. Als u ons een volledig beeld geeft van uw behoeften, kunt u er zeker van zijn dat uw project op de juiste wijze wordt uitgevoerd en dat de schatting correct is.

## Aan de slag {#started}

Voordat we binnenduiken, moeten we de antwoorden op deze vragen kennen:

* **Is het nieuwe gegevensbestand op een nieuwe server?** Voordat u een aanvraag indient, moet u de instellingen van de gegevensverbinding bijwerken onder **[!UICONTROL Manage Data** > **Connections]**. Als u een verfrisser nodig hebt op hoe te om dit te doen, ga naar [`Integrations`](../integrations/integrations.md) en zoekt u naar de instructies voor het type database dat u gebruikt.
* **Bestaan alle historische gegevens in de nieuwe database of moet deze worden gemigreerd?** We kunnen de historische en nieuwe gegevens tijdens het migratieproces consolideren. Zelfs als u geen consolidatie nodig hebt, vragen wij u ons in uw verzoek op de hoogte te stellen.

Nadat u de antwoorden op het bovenstaande hebt ontvangen, moeten we weten wat voor soort migratie er is: zal de nieuwe database de [`same`](#sameschema) schema, of zal het een [`different`](#newschema) schema? In de onderstaande secties vindt u gedetailleerde instructies voor elk type migratie.

## Migreren naar een nieuwe database met hetzelfde schema {#sameschema}

Wanneer het voorleggen van het verzoek, laat ons weten dat het gegevensbestandschema niet verandert en dat de verbinding reeds opstelling is in [!DNL MBI].

Als de database een nieuwe naam heeft, neemt u deze op in de aanvraag zodat de dashboards correct kunnen worden gemigreerd.

Als de databasenaam niet wordt gewijzigd, is de migratie voltooid. De dashboards en de rapporten zullen verfrissen na de volgende volledige update wordt voltooid. We vragen u nog steeds contact met ons op te nemen, zodat we de problemen die de migratie met zich meebrengt, kunnen overwinnen.

## Migreren naar een nieuwe database met een ander schema {#newschema}

>[!IMPORTANT]
>
>Als bepaalde gegevenskolommen geen gelijkwaardige kolommen in het nieuwe gegevensbestand hebben, is er een kans dat bepaalde analyses in het proces zullen verloren gaan.

Om dit type migratie te voltooien, moeten bestaande gegevenskolommen worden aangepast aan hun equivalenten in de nieuwe database. Dit is niet verplicht voor u om te doen, maar het uitvoeren van de overeenkomst voor ons zal helpen de draaisnelheid van uw verzoek versnellen en de prijs van de migratie verlagen.

Als u zich comfortabel voelt het aanpassen zelf, volg deze instructies en maak de voltooide spreadsheet aan uw verzoek vast:

1. Bekijk alle tabellen en kolommen die momenteel met uw Data Warehouse worden gesynchroniseerd (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. Maak in een spreadsheet een tab voor elke tabel die naar de nieuwe database moet worden gemigreerd.
1. Maak op elk tabblad een kolom voor alle bestaande kolommen die moeten worden gemigreerd. We raden u aan het een of andere naam te geven `Existing column name`.
1. U moet ook een andere kolom voor de kolomequivalenten in het nieuwe gegevensbestand in elk lusje van het spreadsheet maken. We raden u aan de kolom een naam te geven, zoals `New column name`.
1. Voer de bestaande kolommen en de equivalente kolommen in. Als een bestaande kolom geen nieuw equivalent heeft, ga enkel in `N/A`.

   Als er een nieuwe manier is om dezelfde informatie in de nieuwe database te berekenen, voert u deze bovendien in het dialoogvenster [`New column name`] kolom.

Hier volgt een voorbeeld:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Als bepaalde gegevenskolommen geen gelijkwaardige kolommen in het nieuwe gegevensbestand hebben, is er een kans dat bepaalde analyses in het proces zullen verloren gaan.

## Hoe dien ik een verzoek in? {#submitreq}

Je kunt ons bereiken door [een supportverzoek indienen](../../../guide-overview.md).

Als u de stappen in de vorige sectie hebt uitgevoerd voor het maken van de overeenkomstige kolomspreadsheet, vergeet dan niet deze bij te voegen.

## Wat nu? {#wrapup}

Het bepalen van het werkingsgebied van het project zal wat samenwerking tussen u en de analist van het team van de Diensten van de Handel nemen die de migratie uitvoeren. De complexiteit van de wijzigingen en de responsiviteit van u en de analist beïnvloeden rechtstreeks de hoeveelheid tijd die de migratie kan kosten. Nadat we de details hebben nagelaten, wordt er een tijdlijn gemaakt en wordt er een werkoverzicht naar u gestuurd.
