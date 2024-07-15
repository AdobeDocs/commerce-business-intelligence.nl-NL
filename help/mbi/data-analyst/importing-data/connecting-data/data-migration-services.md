---
title: Gegevensmigratieservices
description: Leer alles wat u nodig hebt om een aanvraag in te dienen en aan de slag te gaan met de migratie.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Gegevensmigratie

Het migreren naar een nieuw gegevensbestandschema, de server, of het melden van gegevensbestand hoeft niet stressvol te zijn. Het [[!DNL Adobe]  team van de Diensten ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) biedt migratiehulp aan.

Om ervoor te zorgen dat de overgang zo soepel mogelijk verloopt, dient u uw migratieverzoek zo gedetailleerd mogelijk in te dienen. Dit onderwerp heeft alles dat u een verzoek moet voorleggen en op de migratie begonnen worden. Als u ons een volledig beeld geeft van uw behoeften, bent u er zeker van dat uw project binnen de juiste reikwijdte valt en dat de schatting correct is.

## Aan de slag {#started}

Voordat u aan de slag gaat, moet u de antwoorden op de volgende vragen kennen:

* **is het nieuwe gegevensbestand op een nieuwe server?** Voordat u een aanvraag indient, moet u de instellingen van de gegevensverbinding bijwerken onder **[!UICONTROL Manage Data** > **Connections]** . Ga naar de sectie [`Integrations`](../integrations/integrations.md) en zoek de instructies voor het type database dat u gebruikt als u dit wilt vernieuwen.

* **bestaat uw alle historische gegevens in het nieuwe gegevensbestand of het moet worden gemigreerd?** U kunt de historische en nieuwe gegevens tijdens het migratieproces consolideren. Zelfs als u geen consolidatie nodig hebt, laat het ons weten in uw verzoek.

Nadat u de antwoorden op het bovenstaande hebt, moet u het type migratie kennen. Heeft de nieuwe database het [`same`](#sameschema) -schema of heeft deze een [`different`](#newschema) -schema? In de onderstaande discussies vindt u gedetailleerde instructies voor elk type migratie.

## Migreren naar een nieuwe database met hetzelfde schema {#sameschema}

Laat ons weten dat het databaseschema niet wordt gewijzigd en dat de verbinding al is ingesteld in [!DNL Adobe Commerce Intelligence] wanneer u de aanvraag indient.

Als de database een nieuwe naam heeft, neemt u deze op in de aanvraag zodat de dashboards correct kunnen worden gemigreerd.

Als de databasenaam niet wordt gewijzigd, is de migratie voltooid. De dashboards en de rapporten zullen verfrissen na de volgende volledige update wordt voltooid.

## Migreren naar een nieuwe database met een ander schema {#newschema}

>[!IMPORTANT]
>
>Als bepaalde gegevenskolommen geen gelijkwaardige kolommen in het nieuwe gegevensbestand hebben, is er een kans dat bepaalde analyses in het proces kunnen worden verloren.

Om dit type migratie te voltooien, moeten bestaande gegevenskolommen worden aangepast aan hun equivalenten in de nieuwe database. Dit is niet verplicht, maar het uitvoeren van de overeenkomst voor ons helpt de doorlooptijd van uw verzoek te versnellen en de prijs van de migratie te verlagen.

Als u zich comfortabel voelt het aanpassen zelf, volg deze instructies en maak de voltooide spreadsheet aan uw verzoek vast:

1. Herzie alle lijsten en kolommen momenteel synchroniserend aan uw Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).

1. Maak in een spreadsheet een tab voor elke tabel die naar de nieuwe database moet worden gemigreerd.

1. Maak op elk tabblad een kolom voor alle bestaande kolommen die moeten worden gemigreerd. Adobe raadt u aan de naam van een item als `Existing column name` te wijzigen.

1. U moet ook een andere kolom voor de kolomequivalenten in het nieuwe gegevensbestand in elk lusje van het spreadsheet maken. Adobe raadt aan de kolom een naam te geven, zoals `New column name` .

1. Voer de bestaande kolommen en de equivalente kolommen in. Als een bestaande kolom geen nieuw equivalent heeft, voert u `N/A` in.

   Als er een nieuwe manier is om dezelfde informatie in de nieuwe database te berekenen, voert u deze in de kolom [`New column name`] in.

Hier volgt een voorbeeld:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Als bepaalde gegevenskolommen geen gelijkwaardige kolommen in het nieuwe gegevensbestand hebben, is er een kans dat bepaalde analyses in het proces kunnen worden verloren.

## Hoe dien ik een verzoek in? {#submitreq}

U kunt uit naar ons bereiken door [ een steunverzoek ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) voor te leggen.

Als u de stappen in de vorige sectie hebt uitgevoerd voor het maken van de overeenkomende kolomspreadsheet, vergeet dan niet deze als bijlage toe te voegen.

## Wat nu? {#wrapup}

Voor het bepalen van het bereik van het project is enige samenwerking nodig tussen u en de analist van het Commerce Services-team dat de migratie uitvoert. De complexiteit van de wijzigingen en de responsiviteit van u en de analist beïnvloeden rechtstreeks de hoeveelheid tijd die de migratie kan kosten. Nadat u de details omlaag hebt gebracht, wordt er een tijdlijn gemaakt die u ontvangt met een overzicht van het werk.
