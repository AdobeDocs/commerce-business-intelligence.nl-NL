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
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

Een metrische waarde is een maat. In SQL en gegevensbestandstructuren, is metrisch als een opgeslagen vraag over een veranderlijke periode.

In [!DNL Commerce Intelligence], kunt u metriek gebruiken aan [grafieken maken](../../data-user/reports/ess-rpt-build-visual.md). De metrische `revenue` het totale aantal orders. De metrische `average customer revenue per order` is wat de gemiddelde klant per orde besteedt.

Indien gebruikt in rapporten, kunnen de metriek over een gespecificeerde tijdspanne worden geanalyseerd en [gefilterd of gesegmenteerd](../../best-practices/segment-filter.md) naar verschillende categorieën. Overweeg een analyse te maken van de gemiddelde opbrengsten van de klant, ingedeeld naar geslacht - in dit geval, `average customer revenue per order` is het metrisch en het geslacht is de groepering.

## De metrische waarde definiëren {#define}

1. Als u metrische gegevens wilt maken, klikt u op **[!UICONTROL Data** > **Metrics]**.

1. Klik op **[!UICONTROL Create New Metric]**.

1. Klik in het vervolgkeuzemenu op de tabel die de native of berekende kolom bevat die u voor de metrische waarde wilt gebruiken.

1. Geef de metrische naam.

   De Adobe adviseert een naam die, in een blik, u vertelt wat metrisch is. Bijvoorbeeld: `Average Order Revenue`.

1. De volgende stap is te bepalen wat uw metrisch doet. Definieer met behulp van de vervolgkeuzemenu&#39;s de bewerking van de meting, en `operation` en een `date` dimensie:

   * Kies een bewerking:
      * `Count` - Deze bewerking telt het aantal rijen in een gegevenstabel
      * `Max` - Max retourneert de maximumwaarde van een specifieke gegevenskolom
      * `Min` - Min retourneert de minimumwaarde van een specifieke gegevenskolom
      * `Sum` - Met deze bewerking worden de waarden van een specifieke gegevenskolom samengevat
      * `Average` - Deze bewerking berekent het gemiddelde van de waarden in de gegevenskolom
      * `Count Distinct Value` - Dit telt het unieke aantal waarden in een specifieke gegevenskolom
      * `Median` - Deze bewerking berekent de mediaan van de waarden in de gegevenskolom
      * `First and Third Quartiles` - Deze bewerkingen berekenen respectievelijk het 25e en 75e percentiel van de kolomwaarden van de gegevens
      * `Tenth and Ninetieth Percentiles` - Deze bewerkingen berekenen respectievelijk het tiende en het negentigste percentiel van de waarden van de gegevenskolom

   * Kies een kolom waarop de bewerking moet worden uitgevoerd. Bijvoorbeeld, als u uw totale opbrengst wilde vinden, zou u een summiere verrichting op uitvoeren `order total` kolom.

     Als u een bestaande metrische waarde bewerkt, kunt u ook [veranderen de operationele lijst van metrisch](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in deze afdeling.

   * Kies een datumdimensie die kan worden gebruikt om metrisch te trenderen. Bijvoorbeeld, `order date`.

## Filters toevoegen {#filters}

De `Filter` kunt u een filter maken of een [opgeslagen filterset](../../data-user/reports/ess-manage-data-filters.md) op uw metrische waarde.

Voor de `average order revenue` metrisch, zou u geen testorden willen omvatten die zouden kunnen worden gedaan terwijl het opzetten van uw opslag - dit zou ons een onjuist resultaat geven. Kan een filterset toepassen om deze orders uit de gegevensset te verwijderen. Nadat het filter is gemaakt, wordt het toegepast op alle diagrammen die met deze metrische waarde zijn gemaakt.

De `Filter Logic` is waar u kunt verder bepalen hoe metrisch zich zou moeten gedragen.

* &quot;\[`A`\] of \[`B`\]&quot; staat alle gegevens toe die voldoen aan de filters \[`A`\] OF \[`B`\]
* &quot;\[`A`\] en \[`B`\]&quot; staat alleen gegevens toe die aan beide filters voldoen \[`A`\] en \[`B`\]
* &quot;(\[`A`\] en \[`B`\]) OF \[`C`\]&quot; staat alleen gegevens toe die aan beide filters voldoen \[`A`\] en \[`B`\] of filter \[`C`\] alleen

## Dimensionen toevoegen {#dimensions}

De [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) toont alle beschikbare gegevensafmetingen voor het filtreren of groeperen; door gebrek, zijn alle beschikbare gegevenskolommen vermeld als afmetingen. Als u doorgaat met het voorbeeld, als u uw inkomsten wilt segmenteren op verwijzingsbron, kunt u dat hier doen.

Naast het weergeven van alle beschikbare gegevenskolommen als afmetingen, [!DNL Commerce Intelligence] Gecontroleerd bij welke kolommen gegroepeerd kunnen worden. *Gegevens segmenteren of groeperen in rapporten*, moeten kolommen worden gemarkeerd als gegroepeerd.

## Voltooien {#finish}

Naast het bepalen van hoe uw metrisch gedrag, kunt u toestemmingsniveaus in `User Rights` sectie. while `Admin` gebruikers hebben toegang tot alle metriek, moet u de gebruikers aangeven die deze metrische waarde kunnen gebruiken door de doos naast de aangewezen groep te controleren.

Als u bestaande metrisch uitgeeft, kunt u een lijst van grafieken (en wie hen bezit) bekijken die deze metrisch in gebruiken `Dependent Charts` sectie.

Wijzigingen worden automatisch opgeslagen en de metrische waarde is nu goed om te gaan.
