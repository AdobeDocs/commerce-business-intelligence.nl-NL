---
title: Googles Analytics met opslaggegevens verwacht
description: Leer om met uw Google Analytics op te slaan gegevens in wisselwerking te staan.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Verwacht [!DNL Google Analytics Warehoused] Gegevens

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Sommige informatie is gebruikt met toestemming van uw vrienden op [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integratie in [!DNL Commerce Intelligence] gebruikt de [!DNL Google Analytics] [Core Reporting API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Om onverwachte of onzinnige resultaten te voorkomen, moet u bevestigen dat de dimensies die u gebruikt [compatibel zijn met een of meer maateenheden](https://ga-dev-tools.google/dimensions-metrics-explorer/) u gebruikt in het dialoogvenster `Report Builder`.

Eén tabel, genaamd `report` - is gemaakt in uw Data Warehouse.

Het schema van deze lijst is samengesteld uit de Metriek en de Dimensionen die u tijdens het opstellingsproces en twee andere kolommen selecteerde: `start-date` en `end-date`.

Als u bijvoorbeeld de volgende Metriek en Dimensionen hebt geselecteerd tijdens de installatie:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

De tabel ziet er zo uit als in het onderstaande voorbeeld.

| **Kolomnaam** | **Beschrijving** |
|-----|-----|
| `\_id` | Deze kolom is `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] unieke id. Deze kolom wordt gemaakt door [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Deze kolom bevat de laatste keer dat de gegevensrij is bijgewerkt. Deze kolom wordt gemaakt door [!DNL Commerce Intelligence]. |
| `start-date` | Identificatie van de dag waarop de rij staat. |
| `end-date` | Identificatie van de dag waarop de rij staat. |
| `month` | Geselecteerde dimensie: maand van de sessie, een geheel getal van twee cijfers van 01 tot en met 12. |
| `users` | Geselecteerde metrisch: Het totale aantal gebruikers voor de gevraagde tijdspanne. |

{style="table-layout:auto"}

## Het verschil tussen [!DNL Google Analytics Warehoused] en [!DNL Live Integration]

De belangrijkste differentiator is dat één integratie wordt opgeslagen ([!DNL Google Analytics Warehoused]) en de andere is niet ([!DNL Google Analytics Live]). In gevallen van [!DNL Google Analytics Warehoused]kunt u uw [!DNL Google Analytics] gegevens en biedt u de mogelijkheid [!DNL Google Analytics] en andere gegevensbronnen om inzichtelijke rapportage te maken.

Kijk naar [!DNL Google Analytics] advertentiecampagnes voor een voorbeeld van wat vanuit een manipulatiestandpunt kan worden gedaan. Stel dat u meerdere advertentiecampagnes voor Q4 met verschillende namen had. De campagnes waren het resultaat van een specifiek marketinginitiatief. Met opgeslagen gegevens, kunt u een kolom creëren die de campagnemenamen in kwestie vindt en Q4 initiatiefnaam van terugkeert `Operation Dumbo`.

Met het combinatieaspect [!DNL Google Analytics] gegevens die met het oog op de uitvoering van analyses aan andere gegevens moeten worden toegevoegd. Neem bijvoorbeeld `Total Time On Site By Ad Campaign` gegevens van [!DNL Google Analytics] en doe mee met `Total Spent Per Campaign` gegevens van [!DNL Facebook Ads] om een volledig beeld te krijgen van hoeveel betrokkenheid u kost.

Met de [!DNL Google Analytics Live] integratie daarentegen , elke [!DNL Google Analytics] een grafiek is als een kleine silo die niet is opgeslagen in uw [!DNL Commerce Intelligence] Data Warehouse.

## Verwante:

* [Verbinding maken [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
