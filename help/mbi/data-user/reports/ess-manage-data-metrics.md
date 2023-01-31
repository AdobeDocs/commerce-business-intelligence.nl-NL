---
title: Metrisch maken
description: Leer hoe u metriek kunt gebruiken om grafieken te maken.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Metrisch maken

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

Eenvoudig gesteld, is metrisch een meting. In SQL en gegevensbestandstructuren, metrisch is als een opgeslagen vraag over een veranderlijke periode.

In [!DNL MBI], kunt u metriek gebruiken aan [grafieken maken](../../data-user/reports/ess-rpt-build-visual.md). Bijvoorbeeld de metrische `revenue` het totale bedrag van de orders. De metrische `average customer revenue per order` is wat de gemiddelde klant per orde besteedt.

Indien gebruikt in rapporten, kunnen de metriek over een gespecificeerde tijdspanne worden geanalyseerd en [gefilterd of gesegmenteerd](../../best-practices/segment-filter.md) naar verschillende categorieën. Overweeg een analyse te maken van de gemiddelde opbrengsten van klanten, ingedeeld naar geslacht - in dit geval, `average customer revenue per order` is het metrisch en het geslacht is de groepering.

## De metrische waarde definiëren {#define}

1. Als u een nieuwe metrische waarde wilt maken, klikt u op **[!UICONTROL Data** > **Metrics]**.

1. Klikken **[!UICONTROL Create New Metric]**.

1. Klik in het vervolgkeuzemenu op de tabel die de native of berekende kolom bevat die u voor de metrische waarde wilt gebruiken.

1. Geef de metrische waarde een naam.

   Wij adviseren een naam die, in een blik, u vertelt wat metrisch is. Bijvoorbeeld: `Average Order Revenue`.

1. De volgende stap is te bepalen wat uw metrisch doet. Definieer met behulp van de vervolgkeuzemenu&#39;s de bewerking van de meting, en `operation` en een `date` dimensie:

   * Kies een bewerking:
      * `Count` - Deze bewerking telt het aantal rijen in een gegevenstabel
      * `Max` - Max retourneert de maximumwaarde van een specifieke gegevenskolom
      * `Min` - Min retourneert de minimumwaarde van een specifieke gegevenskolom
      * `Sum` - Met deze bewerking worden de waarden van een specifieke gegevenskolom samengevat
      * `Average` - Deze bewerking berekent het gemiddelde van de waarden in de gegevenskolom
      * `Count Distinct Value` - Hiermee wordt het unieke aantal waarden in een specifieke gegevenskolom geteld
      * `Median` - Deze bewerking berekent de mediaan van de waarden in de gegevenskolom
      * `First and Third Quartiles` - Deze bewerkingen berekenen respectievelijk het 25e en 75e percentiel van de kolomwaarden van de gegevens
      * `Tenth and Ninetieth Percentiles` - Deze bewerkingen berekenen respectievelijk het tiende en het negentigste percentiel van de waarden van de gegevenskolom
   * Kies een kolom waarop de bewerking moet worden uitgevoerd. Bijvoorbeeld, als u uw totale opbrengst wilde vinden, zou u een summiere verrichting op uitvoeren `order total` kolom.

      Als u een bestaande metrische waarde bewerkt, kunt u ook [veranderen de operationele lijst van metrisch](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in deze afdeling.

   * Kies een datumdimensie die kan worden gebruikt om metrisch te trenderen. Bijvoorbeeld: `order date`.


## Filters toevoegen {#filters}

De `Filter` kunt u een nieuw filter maken of een [opgeslagen filterset](../../data-user/reports/ess-manage-data-filters.md) op uw metrische waarde.

Voor ons `average order revenue` metrisch, wij zouden geen testbevelen willen omvatten die zouden kunnen worden gedaan terwijl het opzetten van onze opslag - dit zou ons een onnauwkeurig resultaat geven. We kunnen een filterset toepassen om deze orders uit de gegevensset te verwijderen. Nadat het filter is gemaakt, wordt het toegepast op alle diagrammen die met deze metrische waarde zijn gemaakt.

De `Filter Logic` is waar u kunt verder bepalen hoe metrisch zich zou moeten gedragen.

* &quot;\[`A`\] of \[`B`\]&quot; staat alle gegevens toe die voldoen aan de filters \[`A`\] OF \[`B`\]
* &quot;\[`A`\] en \[`B`\]&quot; staat alleen gegevens toe die aan beide filters voldoen \[`A`\] en \[`B`\]
* &quot;(\[`A`\] en \[`B`\]) OF \[`C`\]&quot; staat alleen gegevens toe die aan beide filters voldoen \[`A`\] en \[`B`\] of filter \[`C`\] alleen

## Dimension toevoegen {#dimensions}

De [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) alle beschikbare gegevensafmetingen voor filteren of groeperen; standaard worden alle beschikbare gegevenskolommen weergegeven als afmetingen. Als we ons voorbeeld voortzetten, als we onze inkomsten willen segmenteren naar bron van verwijzing, zouden we dat hier kunnen doen.

Naast het weergeven van alle beschikbare gegevenskolommen als afmetingen, [!DNL MBI] Hierbij wordt ook raden bij welke kolommen gegroepeerd kunnen worden. *Gegevens segmenteren of groeperen in rapporten*, moeten kolommen worden gemarkeerd als gegroepeerd.

## Voltooien {#finish}

Naast het bepalen van hoe uw metrisch gedrag, kunt u toestemmingsniveaus in `User Rights` sectie. while `Admin` gebruikers hebben toegang tot alle metriek, moet u de gebruikers aangeven die deze metrische waarde kunnen gebruiken door de doos naast de aangewezen groep te controleren.

Als u bestaande metrisch uitgeeft, kunt u een lijst van grafieken (en wie hen bezit) bekijken die deze metrisch in gebruiken `Dependent Charts` sectie.

Wijzigingen worden automatisch opgeslagen en de metrische waarde is nu goed om te gaan.
