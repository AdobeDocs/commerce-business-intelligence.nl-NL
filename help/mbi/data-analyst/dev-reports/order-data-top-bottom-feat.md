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

# Gegevens sorteren met de functie `Show Top/Bottom`

U kunt meer doen in `Visual Report Builder` dan analyses maken die trend in de tijd. U kunt bijvoorbeeld een rapport maken om te laten zien hoe waardevol uw aankoop- en marketingkanalen zijn, maar u kunt ook een rapport maken waarin alleen de vijf belangrijkste uitvoerders worden getoond. Op dezelfde manier kunt u uw marketing inspanningen door een rapport concentreren te creëren dat u toont welke staten de meeste opbrengst produceren.

Dit soort sorteren en ordenen van gegevens kan worden uitgevoerd in rapporten die zowel een `Group By` als een `Time Interval of None` gebruiken. Wanneer beide elementen in een rapport staan, wordt de functie `Show Top/Bottom` boven de voorvertoning van het diagram weergegeven. Met deze functie kunt u de bovenste (hoogste tot laagste) en onderste (laagste tot hoogste) gegevenspunten weergeven op basis van de parameters die u instelt.

![ toon Hoogste/Onderste eigenschap in Visuele Report Builder.](../../assets/Show_Top_Bottom.png)

## Hoe gebruik ik dit? {#how}

Klik op **[!UICONTROL Show Top/Bottom link]** om de parameters voor weergave en sorteren in te stellen. Het getal in het tekstvak kan een geheel getal zijn (zoals `5` ) of `ALL` . Daarna, kunt u verkiezen om het rapport of door metrisch OF door de groepering te sorteren.

Bijvoorbeeld, als u de vijf verwijzingsbronnen wilde tonen die de meeste opbrengst in brachten, is dit hoe u het doet:

1. Voeg `Revenue` metrisch aan het rapport toe.

1. Voeg een `Group By` toe om metrisch door verwijzingsbron te segmenteren.

1. Stel `Time Interval` in op `None` .

1. Stel in de `Show Top/Bottom` -instellingen de weergave in op `5` , zodat alleen de verwijzingsbronnen met de bovenste vijf totale inkomstenbedragen in het rapport worden opgenomen.

>[!NOTE]
>
>Omdat het rapport geen `Time Interval` heeft, kunnen de waarden - in dit geval, de hoogste vijf verwijzingsbronnen - in de loop der tijd veranderen. Als één verwijzingsbron een andere in termen van opbrengst overtreft, verandert de orde waarin de bronnen tonen.

## Hoe zit het met het gebruik van meerdere metriek? {#multiplemetrics}

Het gebruiken van deze eigenschap wordt gecompliceerd wanneer tHere meer dan één metrisch in een rapport is omdat elke metrisch slechts door zich of door één van de groeperingen kan worden gesorteerd.

Stel dat u een rapport hebt gemaakt met zowel de metriek `Revenue` als `Number of orders` , gegroepeerd op verwijzingsbron. `Revenue` kan alleen worden gesorteerd op `Revenue` of verwijzingsbron en `Number of orders` kan alleen worden gesorteerd op `Number of orders` of verwijzingsbron.

Dit betekent dat u de `Revenue` alleen kunt weergeven van de bovenste `5` bronnen voor inkomstengenererende verwijzingen, maar dat u het aantal bestellingen niet ook kunt weergeven bij de bovenste `5` bronnen voor inkomstengenererende verwijzingen. Eenvoudig gezet: wanneer er veelvoudige metriek zijn, is de beste weddenschap om elke metrisch door het groeperen te sorteren.

Hieronder ziet u een voorbeeld van een grafiek die de `Revenue` -metrische waarde op zichzelf sorteerde in plaats van op de groepering. Zoals u kunt zien, creeerde het sorteren metrisch door het groeperen geen vreemd (en uiteindelijk onnuttig) rapport:

![ Vreemde en nutteloze rapportresultaten.](../../assets/strange-report-results.png)

Als u beide metriek door het groeperen had gesorteerd, zou de grafiek als dit kijken:

![ sorterend beide metriek door het groeperen.](../../assets/sort-metrics-by-grouping.png)

## Hoe worden waarden standaard gesorteerd? {#defaultsorting}

Wanneer slechts één metrische waarde wordt opgenomen in een rapport met een `Group by` en een `Time Interval` van `None` , is de standaardvolgorde in `Visual Report Builder` het weergeven van de bovenste waarden op basis van de metrische waarde. In dit geval is de functie `Show Top/Bottom` mogelijk niet nodig als dit aan uw behoeften voldoet.

In dit voorbeeld wordt bekeken hoeveel mogelijkheden uw vertegenwoordigers hebben gesloten. Deze tabel wordt automatisch gesorteerd van hoogste naar laagste op basis van de metrische waarde, in dit geval `Won Opportunities` .

![ die door metrisch wordt bevolen.](../../assets/Ordered_by_metric.png)

Wanneer u echter een tweede metrische waarde toevoegt, wordt de bovenste waarde standaard op basis van de groepering ingesteld. Als metriek en groepen worden toegevoegd, wordt de standaardsortering gebaseerd op de eerste groepering, daarna op de tweede groepering, enzovoort.

![ die door de groepering wordt bevolen.](../../assets/Ordered_by_grouping.png)

## Omloop {#wrapup}

Hoewel een aantal basisfuncties hier wordt behandeld, is deze functie voor veel interessante toepassingen geschikt.

Denk aan de vorige verkoopvertegenwoordiger en het voorbeeld van kansen. Door `Time Interval` te verwijderen, een `Group By` toe te passen en de gegevens op basis van de groepering te sorteren, konden we een gedetailleerd beeld krijgen van het aantal gewonnen kansen van elke vertegenwoordiger. Met de functie `Show Top/Bottom` kunnen we ook zien wie de beste uitvoerders zijn.
