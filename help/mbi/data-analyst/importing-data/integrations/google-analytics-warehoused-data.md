---
title: Google Analytics-opslaggegevens verwacht
description: Leer hoe u communiceert met gegevens die zijn opgeslagen in Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Google Analytics Warehoused] gegevens verwacht

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Sommige informatie werd gebruikt met toestemming van uw vrienden op [[!DNL Stitch] ](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integratie in [!DNL Commerce Intelligence] gebruikt [!DNL Google Analytics] [ Kern die API meldt ](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Om onverwachte of onzinnige resultaten te vermijden, bevestig dat om het even welke afmetingen u gebruikt [ compatibel met één of meerdere metriek ](https://ga-dev-tools.google/dimensions-metrics-explorer/) zijn u in `Report Builder` gebruikt.

Er wordt één tabel, genaamd `report`, gemaakt in uw Data Warehouse.

Het schema van deze tabel bestaat uit de metriek en afmetingen die u tijdens het installatieproces hebt geselecteerd en twee andere kolommen: `start-date` en `end-date` .

Als u bijvoorbeeld de volgende maateenheden en afmetingen hebt geselecteerd tijdens de installatie:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

De tabel ziet er zo uit als in het onderstaande voorbeeld.

| **de Naam van de Kolom** | **Beschrijving** |
|-----|-----|
| `\_id` | Deze kolom is de `primary key` . |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] unieke id. Deze kolom wordt gemaakt door [!DNL Commerce Intelligence] . |
| `\_updated\_at` | Deze kolom bevat de laatste keer dat de gegevensrij is bijgewerkt. Deze kolom wordt gemaakt door [!DNL Commerce Intelligence] . |
| `start-date` | Identificatie van de dag waarop de rij staat. |
| `end-date` | Identificatie van de dag waarop de rij staat. |
| `month` | Geselecteerde dimensie: maand van de sessie, een geheel getal van twee cijfers van 01 tot en met 12. |
| `users` | Geselecteerde metrisch: Het totale aantal gebruikers voor de gevraagde tijdspanne. |

{style="table-layout:auto"}

## Wat is het verschil tussen [!DNL Google Analytics Warehoused] en [!DNL Live Integration]

Het belangrijkste differentiator is dat één integratie wordt opgeslagen ([!DNL Google Analytics Warehoused]), en andere is niet ([!DNL Google Analytics Live]). In gevallen van [!DNL Google Analytics Warehoused] kunt u hiermee uw [!DNL Google Analytics] -gegevens bewerken en kunt u [!DNL Google Analytics] en andere gegevensbronnen combineren om een inzichtelijke rapportage te maken.

Bekijk [!DNL Google Analytics] advertentiecampagnes voor een voorbeeld van wat van een manipulatiestandpunt kan worden gedaan. Stel dat u meerdere advertentiecampagnes voor Q4 met verschillende namen had. De campagnes waren het resultaat van een specifiek marketinginitiatief. Met opgeslagen gegevens, kunt u een kolom tot stand brengen die de campagnemenamen in kwestie vindt en Q4 initiatiefnaam van `Operation Dumbo` terugkeert.

Met het combinatieaspect kunnen [!DNL Google Analytics] -gegevens worden gekoppeld aan andere gegevens om analyses uit te voeren. Neem bijvoorbeeld `Total Time On Site By Ad Campaign` gegevens van [!DNL Google Analytics] en voeg deze samen met `Total Spent Per Campaign` gegevens van [!DNL Facebook Ads] om een volledig beeld te krijgen van hoeveel betrokkenheid u kost.

Met de [!DNL Google Analytics Live] -integratie aan de andere kant is elke [!DNL Google Analytics] -grafiek een soort kleine silo die niet is opgeslagen in uw [!DNL Commerce Intelligence] Data Warehouse.

## Verwante:

* [Verbinding maken  [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
