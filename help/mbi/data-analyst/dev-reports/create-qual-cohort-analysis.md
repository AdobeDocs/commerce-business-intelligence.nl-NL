---
title: Een kwalitatieve cohortanalyse maken
description: Leer wat een kwalitatief cohort is, waarom je geïnteresseerd zou kunnen zijn in het maken van deze analyse, en hoe je het kunt maken in de Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Een `Qualitative Cohort Analysis`

Weet u hoe uw [!DNL Google Adwords]- de verworven klantensegmenten hun LTV in vergelijking met die klanten kweken die van biologisch onderzoek worden verworven? Heb je ooit gedacht aan het uitvoeren van een `cohort` analyse van verschillende klantensegmenten naast elkaar in hetzelfde rapport? Zo ja, `qualitative cohort analysis` helpt u deze vragen te beantwoorden.

Dit onderwerp duikt in wat een kwalitatieve cohort is, waarom je geïnteresseerd zou kunnen zijn in het bouwen van deze analyse en hoe je het kunt maken in [!DNL Commerce Intelligence].

## Wat is `qualitative cohorts`, toch? {#whatare}

`Cohort` de analyse in het algemeen kan globaal worden gedefinieerd als de analyse van gebruikersgroepen die gedurende hun levenscyclus vergelijkbare kenmerken delen . Hiermee kunt u gedragstrends in verschillende gebruikersgroepen identificeren.

Zie [cohortanalyse](https://www.cohortanalysis.com/).

Meeste `cohort` analyses in [!DNL Commerce Intelligence] groepeer gebruikers samen door een gemeenschappelijke datum (bijvoorbeeld, de reeks alle klanten die hun eerste aankoop in een bepaalde maand maakten). A `qualitative cohort` is iets anders: het is een gebruikersgroep die door een eigenschap wordt bepaald die niet op tijd-gebaseerd is. Voorbeelden zijn:

* De set met alle gebruikers die zijn aangeschaft via een advertentiecampagne
* De set van alle gebruikers voor wie de eerste aankoop een coupon bevatte (of niet)
* De set van alle gebruikers die een bepaalde leeftijd hebben

## Hoe verschilt dat van normaal `cohort` bouwer? {#different}

De [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) is geoptimaliseerd voor het groeperen van cohorten met behulp van een tijdgebonden kenmerk. Dit is ideaal voor analyses die zijn toegespitst op een specifiek gebruikerssegment (bijvoorbeeld alle gebruikers die zijn aangeschaft via een betaalde zoekcampagne). In de `Cohort Analysis Builder`, kunt u (1) zich op die specifieke gebruikersgroep concentreren, en (2) `cohort` op een datum (zoals de datum van de eerste bestelling).

Nochtans, als u het cohortgedrag van veelvoudige gebruikerssegmenten in het zelfde cohortrapport wilt analyseren (`paid` zoeken versus `organic` zoek of direct verkeer, misschien?), kan deze geavanceerdere analyse in het `Report Builder`.

## Welke informatie moet ik verstrekken om mijn analyse te ondersteunen? {#support}

Een `qualitative cohort` in het `Report Builder` Hierbij wordt het Adobe-analist-team betrokken bij het maken van [geavanceerd berekende kolommen](../data-warehouse-mgr/creating-calculated-columns.md) betreffende de nodige tabellen.

Als u deze wilt bouwen, dient u een [ondersteuningsticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (en verwijs naar dit artikel!) Dit is wat u moet weten:

* De `metric` u wilt uw cohortanalyse uitvoeren met en welke lijst het gebruikt (voorbeeld: `Revenue`op basis van de `orders` tabel).

* De `user segments` u wilt bepalen en waar die informatie in uw gegevensbestand leeft (voorbeeld: verschillende waarden van `User's referral source`, die in de `users` tabel en verplaatst naar de `orders`).

* De `cohort date` u wilt dat uw analyse wordt gebruikt (voorbeeld: de `User's first order date` tijdstempel). Dit voorbeeld stelt ons in staat elk segment te bekijken en `How does a user's revenue grow in the months following their first order date?`.

* De `time interval` dat u de analyse wilt zien over (voorbeeld: `weeks`, `months`, of `quarters` na de `User's first order date`).

Zodra het Adobe analyst team aan het bovenstaande antwoordt, hebt u een paar nieuwe geavanceerde berekende kolommen om uw rapport uit te bouwen! Hieronder volgt u de aanwijzingen.

## De kwalitatieve cohortanalyse maken {#create}

Eerst, wilt u metrisch toevoegen u in het cohorteren geinteresseerd bent, eens voor elk `cohort` u analyseert. In dit voorbeeld wilt u cumulatief weergeven `Revenue` gemaakt in de maanden na de eerste bestelling van een klant, gesegmenteerd door de `User's referral source`. Dit betekent dat u voor elk segment één segment toevoegt `Revenue` Metrisch en filter voor het specifieke segment:

![](../../assets/qualcohort1.gif)

Ten tweede moet u twee wijzigingen aanbrengen in de tijdopties van het rapport:

1. Stel de `time interval` tot `None`. Dit is omdat u uiteindelijk tegen het tijdinterval als dimensie in plaats van het gebruiken van de gebruikelijke tijdopties groepeert.

1. Stel de `time range` aan het tijdvenster dat u het rapport wilt behandelen.

In dit voorbeeld ziet u een `all time` weergave van `Revenue`. Daarna, zou u met een reeks punten moeten eindigen:

![](../../assets/qualcohort2.gif)

Ten derde past u zich aan om het `cohorts`. Op basis van de `cohort date` en `time interval` u hebt opgegeven aan het team van Adobe-analisten, hebt u een dimensie in uw account die het `cohort` dateren. In dit voorbeeld wordt die aangepaste dimensie aangeroepen `Months between this order and customer's first order date`. Gebruikend deze afmeting, zou u moeten:

* `Group by` de dimensie met de `group by` option

* Selecteer alle waarden van het dialoogvenster `dimension` waarin u geïnteresseerd bent

* Met de `Show top/bottom option`, selecteert u de bovenste X-maanden waarin u geïnteresseerd bent en sorteert u op de `Months between this order and customer's first order date` dimensie

Nu kunt u één regel voor elke regel zien `cohort` opgegeven. Kijk nu eens naar het voorbeeld — zie je de `Revenue` bijdragen van gebruikers van elke verwijzingsbron; `grouped by` het aantal maanden tussen hun eerste bestelling en elke volgende bestelling. In het voorbeeld is ook een `Cumulative perspective` om de `cohorts'` totale groei - bekijk de resultatentabel voor meer granulariteit .

Wat zegt dit ons? Hier, de specifieke verwijzingsbron `Paid search` is waardevol in de eerste maand van het de aankoopleven van een klant, maar slaagt er niet in zijn klantenbasis met herhaalde opbrengst te behouden. while `Direct Traffic` begint met een lager bedrag , de inkomsten in de daaropvolgende maanden worden in een vergelijkbaar tempo geaccumuleerd .

Hoe je het ook maakt, `cohort` analyse is een krachtig hulpmiddel in uw analyse toolbox. Dit soort analyse kan wat interessante inzichten over uw zaken opleveren die traditioneel `time-based cohorts` misschien niet, waardoor u betere gegevensgestuurde beslissingen kunt nemen.
