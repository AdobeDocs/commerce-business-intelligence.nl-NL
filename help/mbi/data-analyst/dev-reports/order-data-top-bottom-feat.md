---
title: Gegevens sorteren met de functie Boven/Onder tonen
description: Leer hoe u uw gegevens kunt bestellen met de functie Boven/Onder tonen.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Gegevens ordenen met `Show Top/Bottom` functie

U kunt meer doen in het dialoogvenster `Visual Report Builder` dan maakt u analyses die trend in de loop der tijd. U kunt bijvoorbeeld een rapport maken om te laten zien hoe waardevol uw aankoop- en marketingkanalen zijn, maar u kunt ook een rapport maken waarin alleen de vijf belangrijkste uitvoerders worden getoond. Op dezelfde manier kunt u uw marketing inspanningen door een rapport concentreren te creëren dat u toont welke staten de meeste opbrengst produceren.

Dit soort het sorteren en het opdracht geven tot van gegevens kan in rapporten worden gedaan die zowel `Group By` en `Time Interval of None`. Wanneer beide elementen in een rapport zijn opgenomen, `Show Top/Bottom` boven de voorvertoning van het diagram. Met deze functie kunt u de bovenste (hoogste tot laagste) en onderste (laagste tot hoogste) gegevenspunten weergeven op basis van de parameters die u instelt.

![Toon Hoogste/Onderste eigenschap in Visuele Report Builder.](../../assets/Show_Top_Bottom.png)

## Hoe gebruik ik dit? {#how}

Nadat u op de knop **[!UICONTROL Show Top/Bottom link]** Er wordt een venster weergegeven waarin u de parameters voor weergave en sorteren kunt instellen. Het getal in het tekstvak kan een geheel getal zijn (zoals `5`) of `ALL`. Daarna, kunt u verkiezen om het rapport of door metrisch OF door de groepering te sorteren.

Als we bijvoorbeeld de vijf verwijzingsbronnen willen weergeven die de meeste inkomsten hebben opgeleverd, is dit hoe we het doen:

1. Voeg de `Revenue` metrisch aan het rapport.

1. Voeg een `Group By` om de metrische waarde te segmenteren door verwijzingsbron.

1. Set `Time Interval` tot `None`.

1. In de `Show Top/Bottom` instellingen, de weergave instellen op `5` daarom worden alleen de referentiebronnen met de hoogste vijf totale ontvangsten in het verslag opgenomen .

>[!NOTE]
>
>Omdat het rapport geen `Time Interval`De waarden - in dit geval de vijf belangrijkste verwijzingsbronnen - kunnen in de loop der tijd veranderen. Als één verwijzingsbron een andere in termen van opbrengst overtreft, zal de orde waarin de bronvertoning zal veranderen.

## Hoe zit het met het gebruik van meerdere metriek? {#multiplemetrics}

Het gebruiken van deze eigenschap wordt gecompliceerd wanneer tHere meer dan één metrisch in een rapport is omdat elke metrisch slechts door zich of door één van de groeperingen kan worden gesorteerd.

Laten we zeggen dat we een verslag hebben opgesteld met beide `Revenue` en `Number of orders` metriek, gegroepeerd op verwijzingsbron. `Revenue` kan alleen worden gesorteerd op `Revenue` of de verwijzingsbron en `Number of orders` kan alleen worden gesorteerd op `Number of orders` of de verwijzingsbron.

Dat betekent dat we de `Revenue` alleen bovenaan `5` inkomsten die verwijzingsbronnen genereren, kunnen we het aantal bestellingen niet ook bij de top laten zien `5` inkomsten die verwijzingsbronnen genereren. Eenvoudig gezegd: wanneer er veelvoudige metriek zijn, is de beste weddenschap om elke metrisch door het groeperen te sorteren.

Hier is een voorbeeld van een grafiek waarin we de grafiek sorteerden `Revenue` op zichzelf metrisch in plaats van door het groeperen. Zoals u kunt zien, creeerde het sorteren metrisch door het groeperen geen vreemd (en uiteindelijk onnuttig) rapport:

![Vreemde en nutteloze rapportresultaten.](../../assets/strange-report-results.png)

Als wij beide metriek door de groepering hadden gesorteerd, zou de grafiek als dit kijken:

![Beide metriek worden gesorteerd op de groepering.](../../assets/sort-metrics-by-grouping.png)

## Hoe worden waarden standaard gesorteerd? {#defaultsorting}

Wanneer slechts één metrisch is inbegrepen in een rapport met a `Group by` en `Time Interval` van `None`, de standaardvolgorde in de `Visual Report Builder` moet de hoogste waarden tonen die op metrisch worden gebaseerd. In dit geval worden de `Show Top/Bottom` is wellicht niet nodig als dit aan uw behoeften voldoet.

In dit voorbeeld bekijken we hoeveel mogelijkheden onze verkoopvertegenwoordigers hebben gesloten. Deze tabel wordt automatisch van hoogste naar laagste gesorteerd op basis van de metrische waarde, in dit geval `Won Opportunities`.

![Volgorde met metrisch.](../../assets/Ordered_by_metric.png)

Wanneer u echter een tweede metrische waarde toevoegt, wordt de bovenste waarde standaard op basis van de groepering ingesteld. Als metriek en groepen worden toegevoegd, wordt de standaardsortering gebaseerd op de eerste groepering, daarna op de tweede groepering, enzovoort.

![Volgorde op groepering.](../../assets/Ordered_by_grouping.png)

## Omloop {#wrapup}

We hebben het aan het begin van het artikel genoemd, maar we zeggen het opnieuw: hoewel we enkele basisvoorbeelden hebben besproken , heeft deze functie veel interessante toepassingen .

Denk aan ons vorige voorbeeld van verkoopvertegenwoordiger en kansen. De `Time Interval`, waarbij een `Group By`En door de gegevens te sorteren op basis van de groepering konden we een gedetailleerd beeld krijgen van het aantal gewonnen kansen van elke vertegenwoordiger. Daarnaast kunt u de opdracht `Show Top/Bottom` laten we zien wie de beste uitvoerders zijn .
