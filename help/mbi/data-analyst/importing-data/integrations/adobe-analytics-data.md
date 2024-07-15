---
title: Verwachte  [!DNL Adobe Analytics]  Gegevens
description: Leer de stappen voor het aansluiten van uw instantie RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# [!DNL Adobe Analytics] gegevens verwacht

De [!DNL Adobe Analytics] integratie voor [!DNL Adobe Commerce Intelligence] gebruikt [ Analytics 2.0 die API ](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md) melden.

>[!INFO]
>
>Om ervoor te zorgen dat u de gegevens verkrijgt die u verwacht, kunt u eerst een rapport maken in de [!DNL Adobe Analytics] Workspace met de gewenste maatstaven en afmetingen. Hierdoor kunt u controleren op compatibiliteit en beschikbaarheid van gegevens.

Er wordt één tabel per verbonden rapportsuite met de naam `report-suite-<ID>` (waarbij `<ID>` een unieke id is die door [!DNL Commerce Intelligence] wordt gegenereerd) gemaakt in uw Data Warehouse.

Het schema van deze lijst is samengesteld uit de metriek en de afmetingen die u in het integratieproces selecteerde. Er worden ook meerdere extra kolommen gegenereerd door [!DNL Commerce Intelligence] voor identificatiedoeleinden.

Bijvoorbeeld, als u volgende metrisch en afmeting tijdens opstelling selecteerde:
- `Metric`: `Page views`
- `Dimension`: `Page`

De tabel bevat de volgende kolommen:

| Kolomnaam | Beschrijving |
| --- | --- |
| `_id` | Deze kolom is de primaire sleutel. |
| `_item_hash` | [!DNL Commerce Intelligence] unieke id. Deze kolom wordt gemaakt door [!DNL Commerce Intelligence] . |
| `_updated_at` | Deze kolom bevat de laatste keer dat de gegevensrij is bijgewerkt. Deze wordt gemaakt door [!DNL Commerce Intelligence] . |
| `start_date` | Begindatum van de opgenomen gegevens voor de rij. `start_date` is altijd 00:00 van dezelfde dag binnen één rij. |
| `end_date` | Einddatum van opgenomen gegevens voor de rij. `end_date` is altijd 23:59 van dezelfde dag binnen één rij. |
| `page_views` | Geselecteerde metrische waarde: het totale aantal paginaweergaven voor de opgegeven tijdsperiode. |
| `page` | Geselecteerde dimensie: afzonderlijke paginanamen met bijgehouden weergaven. |

Controle die van de geselecteerde metriek en de afmetingen gegevens beschikbaar in uw [!DNL Commerce Intelligence] lijst door de *synchronisatie* of *unsync* opties in de `Data Warehouse` pagina te gebruiken hebben. Kolommen die momenteel niet worden gesynchroniseerd, worden grijs weergegeven. Als u stopt met het synchroniseren van een kolom, kunt u deze later opnieuw synchroniseren.

## Huidige beperkingen

In deze sectie worden de beperkingen van de [!DNL Adobe Analytics] -integratie voor [!DNL Commerce Intelligence] beschreven.

| Beperking | Beschrijving |
| --- | --- |
| `Historical data period` | Net als bij andere integraties van derden, haalt de [!DNL Adobe Analytics] -integratie een beperkte hoeveelheid historische gegevens op en worden de gegevens vervolgens bijgewerkt. De historische periode wordt gevormd aan 2 weken. |
| `Empty component combinations` | Sommige combinaties van metriek en afmetingen bevatten geen gegevens. Als een dergelijke combinatie voor replicatie wordt geselecteerd, sluit [!DNL Commerce Intelligence] de kolom van de herhaalde lijst uit. Om te vermijden selecterend zulk een combinatie, kunt u een rapport in [[!DNL Adobe Analytics]  Workspace ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) eerst tot stand brengen om te verifiëren u de gegevens krijgt u verwacht. |
| `Re-authorization cadence` | Om de twee weken moet de [!DNL Adobe Analytics] -integratie opnieuw worden geautoriseerd. Als u opnieuw wilt autoriseren, gaat u naar de pagina Bewerken voor de integratie en klikt u op **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]** . |
| `One dimension per row` | [!DNL Adobe Analytics] biedt metrische gegevens voor één dimensie tegelijk. Als u tijdens de installatie meerdere afmetingen selecteert, bevat elke rij in de [!DNL Commerce Intelligence] -tabel één waarde voor de dimensie en wordt voor elke andere dimensie nul. |
