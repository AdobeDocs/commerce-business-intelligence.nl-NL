---
title: Een kwalitatieve cohortanalyse maken
description: Leer wat een kwalitatief cohort is, waarom je geïnteresseerd bent in het maken van deze analyse, en hoe je het kunt maken in Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Een `Qualitative Cohort Analysis` maken

Weet u hoe uw [!DNL Google Adwords]-verworven klantensegmenten hun LTV in vergelijking met die klanten kweken die van biologisch onderzoek worden verworven? Hebt u er ooit aan gedacht om een `cohort` analyse op verschillende klantensegmenten naast elkaar in het zelfde rapport uit te voeren? Als dat het geval is, kunt u deze vragen met een `qualitative cohort analysis` beantwoorden.

Dit onderwerp duikt in wat een kwalitatieve cohort is, waarom u in het bouwen van deze analyse zou kunnen geinteresseerd zijn, en hoe u het in [!DNL Commerce Intelligence] kunt tot stand brengen.

## Wat zijn `qualitative cohorts` toch? {#whatare}

In het algemeen kan de analyse van `Cohort` globaal worden gedefinieerd als de analyse van gebruikersgroepen die gedurende hun levenscyclus vergelijkbare kenmerken delen. Hiermee kunt u gedragstrends in verschillende gebruikersgroepen identificeren.

Zie [ cohortanalyse ](https://www.cohortanalysis.com/).

De meeste `cohort` analyses in [!DNL Commerce Intelligence] groeperen gebruikers samen door een gemeenschappelijke datum (bijvoorbeeld, de reeks alle klanten die hun eerste aankoop in een bepaalde maand maakten). Een `qualitative cohort` is iets anders: het is een gebruikersgroep die wordt gedefinieerd door een kenmerk dat niet op tijd is gebaseerd. Voorbeelden zijn:

* De set met alle gebruikers die zijn aangeschaft via een advertentiecampagne
* De set van alle gebruikers voor wie de eerste aankoop een coupon bevatte (of niet)
* De set van alle gebruikers die een bepaalde leeftijd hebben

## Hoe verschilt dat van de normale `cohort` builder? {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) is geoptimaliseerd voor het groeperen van cohorten met behulp van een op tijd gebaseerde eigenschap. Dit is ideaal voor analyses die zijn toegespitst op een specifiek gebruikerssegment (bijvoorbeeld alle gebruikers die zijn aangeschaft via een betaalde zoekcampagne). In `Cohort Analysis Builder` kunt u (1) zich op die specifieke gebruikersgroep richten, en (2) `cohort` op een datum (zoals hun eerste ordedatum).

Als u echter het cohortgedrag van meerdere gebruikerssegmenten in hetzelfde cohortrapport wilt analyseren (`paid` zoeken in plaats van `organic` zoeken in plaats van rechtstreeks verkeer, bijvoorbeeld?), kunt u deze geavanceerdere analyse maken in het `Report Builder` .

## Welke informatie moet ik verstrekken om mijn analyse te ondersteunen? {#support}

Creërend een `qualitative cohort` rapport in `Report Builder` impliceert het de analistenteam van Adobe die sommige [ geavanceerde berekende kolommen ](../data-warehouse-mgr/creating-calculated-columns.md) creëren op de noodzakelijke lijsten.

Om deze te bouwen, voorleg a [ steunkaartje ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (en verwijzing dit artikel!). Dit is wat u moet weten:

* De `metric` waarmee u de cohortanalyse wilt uitvoeren en de tabel waarin deze wordt gebruikt (bijvoorbeeld: `Revenue` , gebaseerd op de tabel `orders` ).

* De `user segments` die u wilt definiëren en de locatie van die informatie in uw database (bijvoorbeeld: verschillende waarden van `User's referral source` , native aan de tabel `users` en verplaatst naar de tabel `orders` ).

* De `cohort date` die u voor de analyse wilt gebruiken (bijvoorbeeld: de `User's first order date` tijdstempel). In dit voorbeeld kunnen we elk segment bekijken en vragen naar `How does a user's revenue grow in the months following their first order date?` .

* De `time interval` waarover u de analyse wilt weergeven (bijvoorbeeld: `weeks` , `months` of `quarters` na de `User's first order date` ).

Als het Adobe-analistenteam op het bovenstaande reageert, hebt u een paar nieuwe, geavanceerd berekende kolommen om uw rapport op te bouwen! Vervolgens kunt u de onderstaande aanwijzingen volgen.

## De kwalitatieve cohortanalyse maken {#create}

Eerst wilt u de metrische waarde toevoegen die u interesseert voor cohoring, eenmaal voor elke `cohort` die u analyseert. In dit voorbeeld wilt u dat cumulatief `Revenue` wordt gemaakt in de maanden na de eerste bestelling van een klant, gesegmenteerd door `User's referral source` . Dit betekent dat u voor elk segment één `Revenue` metrische waarde en filter voor het specifieke segment toevoegt:

![ Geanimeerde demonstratie van het creëren van een kwalitatieve cohortanalyse ](../../assets/qualcohort1.gif)

Ten tweede moet u twee wijzigingen aanbrengen in de tijdopties van het rapport:

1. Stel de waarde `time interval` in op `None` . Dit is omdat u uiteindelijk tegen het tijdinterval als dimensie in plaats van het gebruiken van de gebruikelijke tijdopties groepeert.

1. Stel `time range` in op het tijdvenster dat door het rapport moet worden bedekt.

In dit voorbeeld bekijkt u een `all time` weergave van `Revenue` . Daarna, zou u met een reeks punten moeten eindigen:

![ Geanimeerde demonstratie van cohort groepering en analyseopties ](../../assets/qualcohort2.gif)

Ten derde past u zich aan om de `cohorts` in te stellen. Op basis van de `cohort date` en `time interval` die u hebt opgegeven voor het Adobe-analistteam, hebt u een dimensie in uw account die de `cohort` -bewerking uitvoert. In dit voorbeeld wordt die aangepaste dimensie `Months between this order and customer's first order date` genoemd. Met deze dimensie moet u:

* `Group by` de dimensie met de optie `group by`

* Selecteer alle gewenste waarden in de `dimension`

* Selecteer met de `Show top/bottom option` de bovenste X-maanden waarin u geïnteresseerd bent en sorteer op de `Months between this order and customer's first order date` -dimensie

U kunt nu één regel zien voor elke `cohort` die u hebt opgegeven. Bekijk nu het voorbeeld — u ziet de `Revenue` bijdrage van gebruikers van elke verwijzingsbron, `grouped by` het aantal maanden tussen hun eerste orde en om het even welke verdere orde. In het voorbeeld is ook een `Cumulative perspective` toegevoegd om de `cohorts'` geaggregeerde groei weer te geven. Kijk in de tabel met resultaten voor meer granulariteit.

Wat zegt dit ons? Hier, is de specifieke verwijzingsbron `Paid search` waardevol in de eerste maand van het de aankoopleven van een klant, maar handhaaft zijn klantenbasis met herhaalde opbrengst niet. Hoewel `Direct Traffic` met een lager bedrag begint, worden de inkomsten in de daaropvolgende maanden in een vergelijkbaar tempo geaccumuleerd.

Ongeacht hoe u deze dikt, `cohort` -analyse is een krachtig hulpmiddel in de gereedschapset voor analyse. Dit type analyse kan wat interessante inzichten over uw zaken opleveren die traditioneel `time-based cohorts` misschien niet, toelatend u om betere gegevens-gedreven besluiten te maken.
