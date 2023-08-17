---
title: Gegevens sorteren met de functie Boven/Onder tonen
description: Leer hoe u uw gegevens kunt bestellen met de functie Boven/Onder tonen.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Gegevens ordenen met `Show Top/Bottom` functie

U kunt meer doen in het dialoogvenster `Visual Report Builder` dan maakt u analyses die trend in de loop der tijd. U kunt bijvoorbeeld een rapport maken om te laten zien hoe waardevol uw aankoop- en marketingkanalen zijn, maar u kunt ook een rapport maken waarin alleen de vijf belangrijkste uitvoerders worden getoond. Op dezelfde manier kunt u uw marketing inspanningen door een rapport concentreren te creëren dat u toont welke staten de meeste opbrengst produceren.

Dit soort het sorteren en het opdracht geven tot van gegevens kan in rapporten worden gedaan die zowel `Group By` en `Time Interval of None`. Wanneer beide elementen in een rapport zijn opgenomen, `Show Top/Bottom` boven de voorvertoning van het diagram. Met deze functie kunt u de bovenste (hoogste tot laagste) en onderste (laagste tot hoogste) gegevenspunten weergeven op basis van de parameters die u instelt.

![Toon Hoogste/Onderste eigenschap in de Visuele Report Builder.](../../assets/Show_Top_Bottom.png)

## Hoe gebruik ik dit? {#how}

Klik op de knop **[!UICONTROL Show Top/Bottom link]** om de parameters voor weergave en sorteren in te stellen. Het getal in het tekstvak kan een geheel getal zijn (zoals `5`) of `ALL`. Daarna, kunt u verkiezen om het rapport of door metrisch OF door de groepering te sorteren.

Bijvoorbeeld, als u de vijf verwijzingsbronnen wilde tonen die de meeste opbrengst in brachten, is dit hoe u het doet:

1. Voeg de `Revenue` metrisch aan het rapport.

1. Voeg een `Group By` om de metrische waarde te segmenteren door verwijzingsbron.

1. Set `Time Interval` tot `None`.

1. In de `Show Top/Bottom` instellingen, de weergave instellen op `5` daarom worden alleen de referentiebronnen met de hoogste vijf totale ontvangsten in het verslag opgenomen .

>[!NOTE]
>
>Omdat het rapport geen `Time Interval`De waarden - in dit geval de vijf belangrijkste verwijzingsbronnen - kunnen in de loop der tijd veranderen. Als één verwijzingsbron een andere in termen van opbrengst overtreft, verandert de orde waarin de bronnen tonen.

## Hoe zit het met het gebruik van meerdere metriek? {#multiplemetrics}

Het gebruiken van deze eigenschap wordt gecompliceerd wanneer tHere meer dan één metrisch in een rapport is omdat elke metrisch slechts door zich of door één van de groeperingen kan worden gesorteerd.

Stel dat u een rapport hebt gemaakt met beide `Revenue` en `Number of orders` metriek, gegroepeerd op verwijzingsbron. `Revenue` kan alleen worden gesorteerd op `Revenue` of de verwijzingsbron `Number of orders` kan alleen worden gesorteerd op `Number of orders` of verwijzing.

Dit betekent dat terwijl u de `Revenue` alleen bovenaan `5` bronnen die inkomsten genereren, kunt u het aantal bestellingen niet ook aan de bovenkant tonen `5` inkomstengenererende verwijzingsbronnen. Eenvoudig gezet: wanneer er veelvoudige metriek zijn, is de beste weddenschap om elke metrisch door het groeperen te sorteren.

Hieronder ziet u een voorbeeld van een grafiek die de `Revenue` op zichzelf metrisch in plaats van door het groeperen. Zoals u kunt zien, creeerde het sorteren metrisch door het groeperen geen vreemd (en uiteindelijk onnuttig) rapport:

![Vreemde en nutteloze rapportresultaten.](../../assets/strange-report-results.png)

Als u beide metriek door het groeperen had gesorteerd, zou de grafiek als dit kijken:

![Beide metriek worden gesorteerd op de groepering.](../../assets/sort-metrics-by-grouping.png)

## Hoe worden waarden standaard gesorteerd? {#defaultsorting}

Wanneer slechts één metrisch is inbegrepen in een rapport met a `Group by` en `Time Interval` van `None`, de standaardvolgorde in de `Visual Report Builder` moet de hoogste waarden tonen die op metrisch worden gebaseerd. In dit geval worden de `Show Top/Bottom` is wellicht niet nodig als dit aan uw behoeften voldoet.

In dit voorbeeld wordt bekeken hoeveel mogelijkheden uw vertegenwoordigers hebben gesloten. Deze tabel wordt automatisch van hoogste naar laagste gesorteerd op basis van de metrische waarde, in dit geval `Won Opportunities`.

![Volgorde met metrisch.](../../assets/Ordered_by_metric.png)

Wanneer u echter een tweede metrische waarde toevoegt, wordt de bovenste waarde standaard op basis van de groepering ingesteld. Als metriek en groepen worden toegevoegd, wordt de standaardsortering gebaseerd op de eerste groepering, daarna op de tweede groepering, enzovoort.

![Volgorde op groepering.](../../assets/Ordered_by_grouping.png)

## Omloop {#wrapup}

Hoewel een aantal basisfuncties hier wordt behandeld, is deze functie voor veel interessante toepassingen geschikt.

Denk aan de vorige verkoopvertegenwoordiger en het voorbeeld van kansen. De `Time Interval`, waarbij een `Group By`En door de gegevens te sorteren op basis van de groepering konden we een gedetailleerd beeld krijgen van het aantal gewonnen kansen van elke vertegenwoordiger. Gebruik ook de opdracht `Show Top/Bottom` laten we zien wie de beste uitvoerders zijn .
