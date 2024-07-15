---
title: Metrisch maken
description: Leer hoe u metriek kunt gebruiken om grafieken te maken.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Metrisch maken

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../administrator/user-management/user-management.md).

Een metrische waarde is een maat. In SQL en gegevensbestandstructuren, is metrisch als een opgeslagen vraag over een veranderlijke periode.

In [!DNL Commerce Intelligence], kunt u metriek gebruiken om [ grafieken ](../../data-user/reports/ess-rpt-build-visual.md) tot stand te brengen. De metrische waarde `revenue` is bijvoorbeeld het totale aantal bestellingen. Metrisch `average customer revenue per order` is wat de gemiddelde klant per orde besteedt.

Wanneer gebruikt in rapporten, kunnen de metriek over een gespecificeerde tijdspanne worden geanalyseerd en [ gefiltreerd of gesegmenteerd ](../../best-practices/segment-filter.md) door verschillende categorieën. Overweeg een analyse te maken van de gemiddelde opbrengsten van klanten, gegroepeerd op geslacht. In dit geval is `average customer revenue per order` de metrische waarde en is het geslacht de groepering.

## De metrische waarde definiëren {#define}

1. Klik op **[!UICONTROL Data** > **Metrics]** om een metrische waarde te maken.

1. Klik op **[!UICONTROL Create New Metric]**.

1. Klik in het vervolgkeuzemenu op de tabel die de native of berekende kolom bevat die u voor de metrische waarde wilt gebruiken.

1. Geef de metrische naam.

   De Adobe adviseert een naam die, in een blik, u vertelt wat metrisch is. Bijvoorbeeld: `Average Order Revenue` .

1. De volgende stap is te bepalen wat uw metrisch doet. Definieer met de vervolgkeuzemenu&#39;s de bewerking van de meting, de kolom `operation` en een `date` -dimensie:

   * Kies een bewerking:
      * `Count` - Deze bewerking telt het aantal rijen in een gegevenstabel
      * `Max` - Max retourneert de maximumwaarde van een specifieke gegevenskolom
      * `Min` - Min retourneert de minimumwaarde van een specifieke gegevenskolom
      * `Sum` - Met deze bewerking worden de waarden van een specifieke gegevenskolom opgeteld
      * `Average` - Deze bewerking berekent het gemiddelde van de waarden in de gegevenskolom
      * `Count Distinct Value` - Hiermee wordt het unieke aantal waarden in een specifieke gegevenskolom geteld
      * `Median` - Deze bewerking berekent de mediaan van de waarden in de gegevenskolom
      * `First and Third Quartiles` - Deze bewerkingen berekenen respectievelijk het 25e en 75e percentiel van de waarden in de gegevenskolom
      * `Tenth and Ninetieth Percentiles` - Deze bewerkingen berekenen respectievelijk het tiende en negentigste percentiel van de waarden in de gegevenskolom

   * Kies een kolom waarop de bewerking moet worden uitgevoerd. Als u bijvoorbeeld uw totale omzet wilt vinden, voert u een saldobewerking uit op de kolom `order total` .

     Als u bestaande metrisch uitgeeft, kunt u ook [ de operationele lijst van metrische metrisch ](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in deze sectie veranderen.

   * Kies een datumdimensie die kan worden gebruikt om metrisch te trenderen. Bijvoorbeeld `order date` .

## Filters toevoegen {#filters}

De `Filter` sectie staat u toe om een filter tot stand te brengen of a [ bewaarde filterreeks ](../../data-user/reports/ess-manage-data-filters.md) op metrisch toe te passen.

Voor `average order revenue` metrisch, zou u geen testorden willen omvatten die zouden kunnen worden gedaan terwijl het opzetten van uw opslag - dit zou ons een onnauwkeurig resultaat geven. Kan een filterset toepassen om deze orders uit de gegevensset te verwijderen. Nadat het filter is gemaakt, wordt het toegepast op alle diagrammen die met deze metrische waarde zijn gemaakt.

In de sectie `Filter Logic` kunt u nader bepalen hoe een metrische waarde zich moet gedragen.

* &quot;\[{0\] of \[`B`\]&quot; staat om het even welke gegevens toe die de filters \[{2\] OF \[`B` \] tevredenstellen`A``A`
* &quot;\[{0\] en \[`B`\]&quot;staat slechts gegevens toe die zowel filters \ [`A` \] als \ [`B` \] tevredenstellen`A`
* &quot;(\[{0\] en \[`B`\]) OF \[`C`\]&quot; staat alleen gegevens toe die aan beide filters \[`A`\] en \[`B`\] voldoen, of alleen aan filter \[`C`\] voldoen`A`

## Dimensionen toevoegen {#dimensions}

In de sectie [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) worden alle beschikbare gegevensafmetingen voor filteren of groeperen weergegeven. Standaard worden alle beschikbare gegevenskolommen weergegeven als afmetingen. Als u doorgaat met het voorbeeld, als u uw inkomsten wilt segmenteren op verwijzingsbron, kunt u dat hier doen.

Naast het weergeven van alle beschikbare gegevenskolommen als dimensies, wordt in [!DNL Commerce Intelligence] aangegeven welke kolommen kunnen worden gegroepeerd. *om gegevens over rapporten* te segmenteren of te groeperen, moeten de kolommen als groeperbaar worden gemerkt.

## Voltooien {#finish}

U kunt niet alleen definiëren hoe de metrische waarden werken, maar ook machtigingsniveaus instellen in de sectie `User Rights` . Hoewel `Admin` -gebruikers toegang hebben tot alle metriek, moet u de gebruikers aangeven die deze metrische waarde kunnen gebruiken door het selectievakje naast de juiste groep in te schakelen.

Als u een bestaande metrische waarde bewerkt, kunt u een lijst met grafieken (en wie er eigenaar van is) weergeven die deze metrische waarde in de sectie `Dependent Charts` gebruiken.

Wijzigingen worden automatisch opgeslagen en de metrische waarde is nu goed om te gaan.
