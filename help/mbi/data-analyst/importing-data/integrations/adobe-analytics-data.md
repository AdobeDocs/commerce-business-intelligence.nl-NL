---
title: Verwacht [!DNL Adobe Analytics] Gegevens
description: Leer de stappen voor het aansluiten van uw instantie RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Verwacht [!DNL Adobe Analytics] Gegevens

De [!DNL Adobe Analytics] integratie voor [!DNL Adobe Commerce Intelligence] gebruikt de [Analyse 2.0 API voor rapportage](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Om ervoor te zorgen dat u de gegevens verkrijgt die u verwacht, kunt u eerst een rapport maken in het dialoogvenster [!DNL Adobe Analytics] Werkruimte met de gewenste afmetingen en afmetingen. Hierdoor kunt u controleren op compatibiliteit en beschikbaarheid van gegevens.

Eén tabel per verbonden rapportsuite, genaamd `report-suite-<ID>` waarbij `<ID>` is een unieke id die is gegenereerd door [!DNL Commerce Intelligence]) is gemaakt in uw Data Warehouse.

Het schema van deze lijst is samengesteld uit de metriek en de afmetingen die u in het integratieproces selecteerde. Verschillende extra kolommen worden ook gegenereerd door [!DNL Commerce Intelligence]voor identificatiedoeleinden.

Bijvoorbeeld, als u volgende metrisch en afmeting tijdens opstelling selecteerde:
- `Metric`: `Page views`
- `Dimension`: `Page`

De tabel bevat de volgende kolommen:

| Kolomnaam | Beschrijving |
| --- | --- |
| `_id` | Deze kolom is de primaire sleutel. |
| `_item_hash` | [!DNL Commerce Intelligence] unieke id. Deze kolom wordt gemaakt door [!DNL Commerce Intelligence]. |
| `_updated_at` | Deze kolom bevat de laatste keer dat de gegevensrij is bijgewerkt. Het wordt gemaakt door [!DNL Commerce Intelligence]. |
| `start_date` | Begindatum van de opgenomen gegevens voor de rij. `start_date` is altijd 00:00 van dezelfde dag binnen één rij. |
| `end_date` | Einddatum van opgenomen gegevens voor de rij. `end_date` is altijd 23:59 van dezelfde dag binnen één rij. |
| `page_views` | Geselecteerde metrisch: Het totale aantal paginaweergaven voor de opgegeven tijdsperiode. |
| `page` | Geselecteerde afmeting: Afzonderlijke paginanamen met bijgehouden weergaven. |

Bepaal welke van de geselecteerde metriek en afmetingen gegevens beschikbaar hebben in uw [!DNL Commerce Intelligence] tabel met *synchroniseren* of *unsync* opties in het dialoogvenster `Data Warehouse` pagina. Kolommen die momenteel niet worden gesynchroniseerd, worden grijs weergegeven. Als u stopt met het synchroniseren van een kolom, kunt u deze later opnieuw synchroniseren.

## Huidige beperkingen

In deze sectie worden de beperkingen van de [!DNL Adobe Analytics] integratie voor [!DNL Commerce Intelligence].

| Beperking | Beschrijving |
| --- | --- |
| `Historical data period` | Net als bij andere integraties van derden [!DNL Adobe Analytics] de integratie trekt een beperkte hoeveelheid historische gegevens en blijft dan gegevens bijgewerkt houden. De historische periode wordt gevormd aan 2 weken. |
| `Empty component combinations` | Sommige combinaties van metriek en afmetingen bevatten geen gegevens. Als een dergelijke combinatie voor replicatie wordt geselecteerd, [!DNL Commerce Intelligence] Hiermee sluit u de kolom uit van de gekopieerde tabel. Als u een dergelijke combinatie niet wilt selecteren, kunt u eerst een rapport maken in het dialoogvenster [[!DNL Adobe Analytics] Werkruimte](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) om te verifiëren u de gegevens krijgt u verwacht. |
| `Re-authorization cadence` | Hertoelating van de [!DNL Adobe Analytics] om de twee weken is integratie vereist . Als u opnieuw wilt autoriseren, gaat u naar de pagina Bewerken voor de integratie en klikt u op **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] verstrekt metrische gegevens voor één afmeting tegelijkertijd. Als u tijdens de installatie meerdere afmetingen selecteert, wordt elke rij in uw [!DNL Commerce Intelligence] de lijst bevat één enkele afmetingswaarde en nulls voor elke andere afmeting. |
