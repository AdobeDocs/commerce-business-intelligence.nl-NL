---
title: De Opties van de Tijd van het gebruik in Visuele Report Builder
description: Leer de gegevens in uw rapport gedurende een bepaalde periode te analyseren.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---

# Gebruiken `Time` Opties in `Visual Report Builder`

Een van de kenmerken van de `Visual Report Builder` is de wereld `Time Range` en `Interval` instellingen. Met deze instellingen kunt u de gegevens in uw rapport gedurende een bepaalde periode analyseren.

Voor sommige analyses moet u echter rekening houden met verschillende tijdsintervallen of tijdsintervallen in hetzelfde rapport. Dat is waar `Time` Er zijn opties. U krijgt een beter idee hoe u `Time` Deze zelfstudie bevat opties in uw rapporten die betrekking hebben op de volgende gebruiksgevallen:

* [Metrische gegevens analyseren zonder tijdstempels](#notimestamp)
* [Eén metrische waarde een onafhankelijk tijdinterval geven](#independenttimeinterval)
* [Dezelfde metrische waarde vergelijken over verschillende tijdbereiken](#difftimerange)

Als u samen met sommige steekproefrapporten wilt volgen die in dit onderwerp worden besproken, open [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) voordat u verdergaat.

## Metrische gegevens analyseren zonder tijdstempels {#notimestamp}

Sommige metriek kan zich eenvoudig niet in tijd aangezien de gegevens niet met een bijbehorende timestamp worden verzameld of worden opgeslagen. Bijvoorbeeld, bevat een inventarislijst vaak slechts één rij voor elke SKU. In dat geval moet u [de metrisch maken](../data-user/reports/ess-manage-data-metrics.md) zonder een tijdstempel op te geven.

Wanneer het gebruiken van zulk metrisch in uw rapportering, merkt u dat het toevoegen van dit metrisch aan een rapport automatisch een onafhankelijke plaatst `Time Interval` van `None` en `Time Range` van `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Eén metrische waarde een onafhankelijk tijdinterval geven {#independenttimeinterval}

`Time` Met de opties kunt u op tijd gebaseerde 100%-grafieken maken om te bepalen welke dag, week, maand of jaar tijdens een bepaald tijdbereik de meeste waarde heeft bijgedragen. In deze sectie, creeert u een grafiek die u het percentage van opbrengst toont die in elke kalendermaand van een jaar wordt geproduceerd.

Dit soort verslagen kan nuttig zijn als u de opbrengst over jaar wilt vergelijken. Bijvoorbeeld, heb u een grafiek voor 2015 onthulde dat Januari 18 percenten van opbrengst voor het jaar bijdroeg en een grafiek voor 2016 toonde slechts 8 percenten. Je zou kunnen beginnen te onderzoeken wat er mogelijk gebeurd is.

1. Voeg uw `Revenue` metrisch aan het rapport.
1. Klikken **[!UICONTROL Duplicate]** om een kopie van de metrische waarde te maken.
1. Klik op de algemene **[!UICONTROL Time Range]** optie, dan **[!UICONTROL Moving Time Range]**. Stel deze in op `Last Year`.
1. Klik op de algemene **[!UICONTROL Time Interval]** en instellen op `Monthly`.
1. Report Builder voegt automatisch een tweede Y-as toe voor een tweede meting. Schakel de optie `Multiple Y-Axes` doos.
1. Vervolgens past u een onafhankelijke `Time Interval` naar de eerste metrieke waarde. Klikken **[!UICONTROL Time Options]** (klokpictogram) rechts van `first Revenue metric`.
1. Klikken **[!UICONTROL Time Options]** in het uitgebreide venster dat boven het rapport wordt weergegeven.
1. Stel in de vervolgkeuzelijst het volgende in:

   * `Time Interval`: instellen op `None`.

   * `Time Range`: instellen op `Last Year` door eerst te klikken **[!UICONTROL Custom]** vervolgens **[!UICONTROL Moving Range]** en tot slot de `Last Year` optie.

   * Klikken **[!UICONTROL Apply]** om de interval- en bereikinstellingen op te slaan. Dit leidt tot een metrisch die de totale inkomsten voor het vorige jaar berekent. Vervolgens gebruikt u deze metrische waarde als noemer in een formule.

   * Om het percentage van opbrengst voor elke maand te zien, moet u een formule aan het rapport toevoegen. Klikken **[!UICONTROL Add Formula]**.

   * Enter `B/A` in het veld Formulier en selecteer `% Percent` in de vervolgkeuzelijst naast het tekstveld. Deze formule verdeelt het bedrag van de ontvangsten van een bepaalde maand van het afgelopen jaar door het totale bedrag van de inkomsten van het afgelopen jaar.

   * Klikken **[!UICONTROL Apply Changes]**.

   * Verberg beide invoermeetgegevens en wijzig de naam van de formule.

Nu kun je zien hoe impact elke maand vorig jaar was:

![](../assets/Independent_Time_Int.png)

## Dezelfde metrische waarde vergelijken over verschillende tijdbereiken {#difftimerange}

In dit voorbeeld wordt een aangepaste dimensie gebruikt, de zogenaamde `Day number of the month`. Als u dit rapport wilt maken en deze dimensie nog niet in uw Data Warehouse hebt, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) voor hulp.

De twee meest voorkomende voorbeelden in deze categorie zijn (1) het vergelijken van groeicijfers (omzet jaar-over-jaar of maand-over-maand) en (2) het beter begrijpen van recente trends in voorraden of verkoop van artikelen.

Om dit geval van gebruik aan te tonen, bekijk de dagelijkse inkomsten voor de vorige maand vergeleken met dezelfde maand van het voorgaande jaar. Stel dat u naar de inkomsten voor elke dag van januari 2016 wilt kijken en die vervolgens wilt vergelijken met januari 2015, januari 2014, enzovoort. Dit verslag zou ons dat laten zien.

1. Voeg uw `Revenue` metrisch aan het rapport.
1. Klikken **[!UICONTROL Duplicate]** om een kopie van de metrische waarde te maken.
1. De naam van de eerste metrische waarde wijzigen in `Items sold last 7 days` en de tweede metrische waarde tot `Items sold last 28 days`.
1. Klikken **[!UICONTROL Time Range]** vervolgens **[!UICONTROL Moving Time Range]**. Stel deze in op `Last Month`.
1. Klikken **[!UICONTROL Time Interval]** en stel deze in op `None`.
1. Klikken **[!UICONTROL Time Options]** (klokpictogram) naast de tweede `Revenue` metrisch.
1. Klikken **[!UICONTROL Time Options]** in het uitgebreide venster dat boven het rapport wordt weergegeven.
1. Stel in de vervolgkeuzelijst het volgende in:

   * `Time Interval`: instellen op `None`.

   * `Time Range`: instellen op `From 14 Months Ago To 13 Months Ago` door eerst te klikken **[!UICONTROL Custom]** dan **[!UICONTROL Moving Range]**. Gebruik de velden en vervolgkeuzelijsten boven aan het menu om het bereik in te stellen. Op die manier kunnen we de inkomsten van de vorige maand zien, maar in het voorgaande jaar.
   Maak zich geen zorgen als metrisch uit het rapport verdwijnt - plaatsend een onafhankelijke tijdoptie verbergt automatisch metrisch van het rapport. Klik op **[!UICONTROL Show]** naast de metrische waarde.

   ![](../assets/Different_Time_Ranges.gif)

   * Klikken **[!UICONTROL Apply]** om de interval- en bereikinstellingen op te slaan.

   * Vervolgens voegt u uw aangepaste `Day number of the month` dimensie door te klikken **[!UICONTROL Group By]** en het selecteren van de dimensie. Dit zal het dagaantal van de maand van een orde terugkeren - bijvoorbeeld een orde die op 2 Maart wordt geplaatst zal terugkeren `2`.

   * In de `Group By` vervolgkeuzelijst, selecteren `Show All` en klik op **[!UICONTROL Apply]**. Dit leidt tot de x-aswaarden voor het rapport:

   ![](../assets/TO4.png)

   * Wijzig de naam van de metriek. In het voorbeeld is de eerste metrische waarde `Revenue - 2015` en de tweede `Revenue - 2014`.



Een ander veelvoorkomend gebruik van aangepaste `Time Options` wordt gebruikt om de leverweken te bepalen. Vooral tijdens de vakantieperiode of een speciale promotieperiode, kunt u punten overwegen die in de afgelopen week, maand, en vorige promotieperiode worden verkocht om geïnformeerde aankoopbesluiten te nemen.

Herinner me om de tijdwaaiers aan te plaatsen wat u wanneer het bouwen van dit rapport zelf nodig hebt.

1. Voeg uw `Items Sold` metrisch aan het rapport.
1. Klikken **[!UICONTROL Duplicate]** om een kopie van de metrische waarde te maken.
1. Wijzig de naam van de metriek. U kunt dezelfde namen gebruiken of iets gelijkaardigs gebruiken:
   1. De naam van de eerste metrische waarde wijzigen in `Items sold last 7 days`.
   1. De naam van de tweede metrieke waarde wijzigen in `Items sold last 28 days`.
1. Op de `Items sold last 7 days` metrisch, klik globale **[!UICONTROL Time Range]** optie dan **[!UICONTROL Moving Time Range]**. In dit voorbeeld stelt u het in op `Last 7 Days`.
1. Klikken **[!UICONTROL Time Interval]** en stel deze in op `None`.
1. Vervolgens definieert u de `Time Options` voor de `Items sold last 28 days` metrisch. Klikken **[!UICONTROL Time Options]** (klokpictogram) rechts van `second Items sold` metrisch.
1. Klikken **[!UICONTROL Time Options]** in het uitgebreide venster dat boven het rapport wordt weergegeven.
1. Stel in de vervolgkeuzelijst het volgende in:

   * `Time Interval`: instellen op `None`.
   * `Time Range`: instellen op `From 29 days to 1 day ago` door eerst te klikken **[!UICONTROL Custom]** vervolgens **[!UICONTROL Moving Range]**. Gebruik de velden en vervolgkeuzelijsten boven aan het menu om het bereik in te stellen.
   * Klikken **[!UICONTROL Apply]** om de interval- en bereikinstellingen op te slaan.
   * Dupliceer de `Items sold last 28 days` metrisch en open nieuwe metrisch `Time Options`. Stel de opties als volgt in:

      * `Time Interval`: dit als `None`.
      * `Time Range`: dit wijzigen in het datumbereik dat overeenkomt met de aanbieding waarin je bent geïnteresseerd door op **[!UICONTROL Specific Date Range]** en vervolgens de passende data in te voeren.
      * De naam van de metrisch wijzigen `Items sold during last promotion` of iets dergelijks.
      * Voeg uw `Units on hand` metrisch.
      * Vervolgens moet u de berekeningen toevoegen die ons de weken tonen, rekening houdend met de verkooptrends, voor de tijdsperioden (`last 7 days`, `last 28 days`, en `last promo` punt) die u in het rapport opneemt. Dit moet u voor elke tijdsperiode doen.

Als u de formules wilt maken, klikt u op **[!UICONTROL Add Formula]**. Voer de onderstaande formules in en klik op **[!UICONTROL Apply Changes]** wanneer gereed. Herhaal dit voor elk van de drie tijdsperioden:

* Voor de `last 7 days time period`, enter `D / A` in de `Formula` veld.
* Voor de `last 28 days time period`, enter `D / (B/4)` in de `Formula` veld.

   >[!NOTE]
   >
   >Het is belangrijk dat u de geselecteerde tijdbereiken hier normaliseert. Breek 28 dagen in vier weken in dit voorbeeld. U moet mogelijk verschillende logica op de formule toepassen.

* Voor de `last promo period`, enter `D / C` in de `Formula` veld.

   ![](../assets/Different_Time_Ranges_2.png)

* Pas ten slotte het rapport aan door de metriek te verbergen en een `SKU` of een vergelijkbare dimensie `Group By`.

Dit voorbeeld toont aan dat de huidige voorraadniveaus goed waren gesitueerd voor een productbrede verkoop van 14 dagen. De toevoeging van een vergelijkbare promotieperiode suggereert echter dat de onderneming enkele wijzigingen moet doorvoeren - hetzij door meer voorraden aan te schaffen en alleen de producten met voldoende eenheden in voorraad te promoten.

Omdat uw klanten zich in tijd verschillend gedragen, kunt u variaties in gegevens verwachten te zien wanneer het uitvoeren van analyses. Door aangepaste tijdopties in te stellen, kunt u snel complexe analyses maken, zodat u gegevensgestuurde beslissingen kunt nemen die van invloed zijn op historische trends.

