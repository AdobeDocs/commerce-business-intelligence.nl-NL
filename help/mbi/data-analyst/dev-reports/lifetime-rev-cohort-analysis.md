---
title: Lifetime-inkomstencohortanalyse
description: Ontdek de kracht van de Commerce Intelligence-cohortanalyse.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# [!DNL Lifetime Revenue Cohort] Analyse

Er zijn verschillende manieren om naar uw gegevens in [!DNL Adobe Commerce Intelligence] te kijken, en u weet dat interpretatie en begrip net zo belangrijk zijn als berekening en visualisatie. In dit onderwerp wordt de kracht van [!DNL Commerce Intelligence] `cohort` -analyse onderzocht.

## Wat betekent `lifetime revenue cohort` analyse?

De onderstaande grafiek geeft de cumulatieve uitgaven per gebruiker weer gedurende een periode nadat deze zijn verworven. `Cohorts` van gebruikers wordt opgesplitst op basis van hun maand van overname.

Bijvoorbeeld, toont de oranje lijn hierboven het gemiddelde voor gebruikers die in November 2011 werden verworven. Het eerste gegevenspunt houdt in dat gebruikers die in november zijn opgehaald, in de eerste maand gemiddeld ongeveer `$200` hebben doorgebracht. Het tweede gegevenspunt houdt in dat deze gebruikers aan het einde van hun tweede maand gemiddeld ongeveer `$240` hadden doorgebracht. Hun gemiddelde uitgaven in maand twee waren ongeveer `$40 (240 - 200)`. De verschillende regels vertegenwoordigen verschillende cohorten van gebruikers. De groene lijn geeft de gebruikers weer die in december zijn aangeschaft. Het blauwe is de gebruikers die in oktober zijn aangeschaft.

## Waarom is dit belangrijk?

Dit soort `cohort` -analyse kan nuttig zijn voor verschillende doeleinden, maar het meest directe voordeel is vaak betere beslissingen over het aanschaffen van klanten. Vele bedrijven beperken hun marketinguitgaven tot kanalen die rentabiliteit op de eerste aankoop van een klant opbrengen. Deze bedrijven betalen om klanten via een bepaald kanaal aan te schaffen zolang hun gemiddelde eerste aankoop meer `gross margin` oplevert dan de aanschaf ervan.

Het probleem met deze aanpak is dat het vaak leidt tot een onderinvestering in groei. Als uw concurrenten marketing gebaseerd op een dieper inzicht in het koopgedrag zijn, overstijgen zij u. De `lifetime revenue cohort` analyse helpt u om de gevolgen te begrijpen van het uitbreiden van uw uitgaven van de klantenverwerving, en het verstrekt een gemakkelijke manier om dit aan de rest van uw team over te brengen. Als toekomstige klanten zich als bestaande klanten gedragen, dan het verwerven van klanten voor een hogere CPA resulteert in een voorspelbare terugbetalingsperiode. Afhankelijk van de kaspositie van de onderneming, kunt u bepalen welke terugbetalingsperiode u met comfortabel bent, de relevante vlek op de grafiek vindt, en dienovereenkomstig besteedt.

U kunt deze analyse ook gebruiken om te zien of wordt u beter in het aan boord gaan van, het in dienst nemen van, en het produceren van opbrengst van de gebruikers u verwerft. Deze `cohort` -analyse is bijvoorbeeld een goede manier om te zien of een gratis verzendpromotie voor nieuwe gebruikers heeft geresulteerd in herhaalde kopers of eenmalige kopers die nooit meer terugkomen.

## Hoe zal dit voor verschillende bedrijfsmodellen variëren?

Voor de meeste bedrijven geeft het `lifetime revenue cohort` -analysediagram een grote hoeveelheid uitgaven in de eerste periode weer en neemt het vervolgens langzamer toe in de loop van de tijd. Die eerste piek is omdat klanten eerder geneigd zijn om hun eerste aankoop te doen kort nadat ze zijn aangeschaft dan op enig ander moment. In gevallen waarin de overnamegebeurtenis zelf een aankoop is, doet 100% van de klanten een aankoop in de eerste periode. In gevallen waarin registratie vóór aankopen kan plaatsvinden, is dit effect minder drastisch.

Als voorbeeld zou [!DNL Groupon] waarschijnlijk een veel lagere eerste sprong hebben dan [!DNL Amazon] , omdat veel van de personen die zich aanmelden voor [!DNL Groupon] niet meteen een aankoop doen. Als er geen hoog aantal restituties is, zal dit diagram na de eerste sprong omhoog en naar rechts hellen. De groeisnelheid neemt in de loop der tijd doorgaans af, omdat klanten het meest actief zijn wanneer ze zich voor het eerst aanmelden. Dit zorgt ervoor dat het gemiddelde daalt omdat het aantal mensen in de cohort constant blijft, ongeacht het aantal dat terugkomt om meer te kopen. In abonnementsbedrijven zal de helling minder agressief afnemen dan in bedrijven waar mensen eenmalige aankopen doen.

Af en toe, zal een abonnementszaken eigenlijk een helling hebben die in tijd stijgt. Het komt zelden voor dat dit gebeurt, maar het is een groot signaal voor het bedrijfsleven wanneer het gebeurt. Dit betekent niet dat er geen klanten zijn die wensen, maar eerder dat upgrades voor klanten die meer blijven dan de klanten die vertrekken compenseren.

## Hoe wordt dit berekend?

Er zijn twee eenvoudige input aan deze berekening: hoeveel leden in `cohort` (die nooit verandert) zijn, en hoeveel opbrengst die leden in de bepaalde periode produceerden. Om de leden in `cohort` te bepalen, telt u het aantal gebruikers die in de periode in kwestie werden verworven. Een overname kan een eerste aankoop, het aanmaken van een account, aanmelding voor nieuwsbrief of een andere gebeurtenis zijn. De `revenue` -berekening is iets gecompliceerder. U wilt de som van de opbrengsten optellen voor orders die door leden van deze `cohort` zijn geplaatst en die binnen een vaste tijdsperiode vanaf de aanschafdatum zijn uitgevoerd (bijvoorbeeld de eerste drie maanden). Tot slot verdeelt u de opbrengst door het aantal leden in `cohort` voor elke tijdspanne in de grafiek en voegt u deze waarde cumulatief in tijd toe.

## Wat zijn de variaties van dit diagram?

Er zijn veel verschillende soorten nuttige `cohort` analyses. De gemeenschappelijkste variatie is [ filtrerend door bron van de gebruikersverwerving ](../analysis/most-value-source-channel.md). U kunt dit diagram bijvoorbeeld bekijken voor klanten die afkomstig zijn van `organic` search, `paid` search of een partnerprogramma. Dit helpt u begrijpen als de klanten van één aanschafbron loyaler of waardevoller zijn dan een andere. U kunt ook filteren op demografie of andere gebruikerskenmerken.

Een andere manier om naar de gegevens te kijken is met een incrementeel, eerder dan cumulatief, gegevensperspectief. Dit toont het stijgende bedrag dat een gemiddelde gebruiker in elke maand besteedt nadat zij worden verworven. Dit is handig als u wilt voorspellen hoeveel herhaalde aankopen u van bestaande gebruikers ontvangt. U kunt hier ook naar kijken met andere dingen dan inkomsten. Sommige voorbeelden omvatten marge en niet - financiële metriek zoals uitnodigingen, stemmen, of berichten.
