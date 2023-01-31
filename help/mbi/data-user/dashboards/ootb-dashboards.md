---
title: Opgenomen dashboards
description: Leer hoe u de gezondheid van essentiële gegevens kunt controleren, zoals inkomsten tijdens de levensduur van de gebruiker, het aantal herhaalde aankopen en meer, en zo een solide basis voor toekomstige exploratie kunt leggen.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Opgenomen dashboards

Als onderdeel van onze services bieden we eCommerce en `SaaS` Startpakketten. Deze pakketten, die door onze analisten worden gecreeerd, bevatten een aangepaste reeks dashboards en rapporten voor uw dataset. Met de analyses in deze pakketten kunt u de gezondheid van essentiële gegevens controleren, zoals inkomsten tijdens de levensduur van de gebruiker, het aantal herhaalde aankopen en nog veel meer. Op die manier wordt een solide basis gelegd voor toekomstige exploratie.

>[!NOTE]
>
>De beschikbaarheid van sommige dashboards hangt van uw dataset af.

Als u vragen hebt of als u een pakket aan uw account wilt toevoegen, dient u een [ondersteuningsticket](../../guide-overview.md) voor hulp.

## Uitvoerend overzicht

De `executive overview` het dashboard wordt gebouwd van grafieken die op andere dashboards bestaan. Dit dashboard is een overzicht op hoog niveau van uw gegevens en bevat grafieken die dagelijks worden gecontroleerd, terwijl andere dashboards meer gedetailleerde informatie bevatten. In eerste instantie wordt deze ingesteld als het standaarddashboard in elke account.

Hoewel we een algemene set grafieken voor u hebben opgenomen, raden we u aan dit dashboard aan uw wensen aan te passen door andere grafieken toe te voegen die u het vaakst gebruikt.

## Cohortanalyse

De `cohort analysis` het dashboard omvat een reeks grafieken die de gemiddelde de inkomstengroei van de gebruikersleven en de stijgende opbrengstgroei tonen gegroepeerd door registratiecolades. Dit onthult of de waarde van het klantenleven (LTV), de waarde van een klant aan een zaken, stijgt in tijd, en ook tendensen rond de groei van LTV identificeert. Merk op dat door gebrek, *we zijn verantwoordelijk voor alle geregistreerde gebruikers (kopers en niet-kopers)* in de gemiddelde LTV-berekening - zie de [onderwerp cohortanalyse](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Dit dashboard kan ook cohortgrafieken bevatten die de levensinkomsten van gebruikers van een specifieke aanschafbron, kanaal of demografisch (bijvoorbeeld New York of Californië) analyseren. Dit moet aantonen hoe u LTV voor zeer specifieke segmenten van uw gebruikersbasis kunt analyseren en zien of één groep of een andere hogere LTV in tijd opbrengt.

Zie voor meer informatie over cohorts [Cohortanalyse uitvoeren](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Als u momenteel de bron van de gebruikersverwerving niet bijhoudt, zie [Overzicht van gegevens van de aanschafbron van gebruikers bijhouden](../../data-analyst/analysis/google-track-user-acq.md).

## E-mailoverzicht

De `Email Summary` dashboard bevat een voorbeeldset grafieken die kunnen worden gebruikt in een geautomatiseerde dagelijkse e-mailsamenvatting. Zie [maken, geautomatiseerde e-mailoverzichten](../../data-user/export-data/email-summaries.md) voor meer informatie over het configureren van e-mailoverzichten.  

## Bewaring gezondheid

De `Retention health` dashboard onthult het herhaalde aankoopgedrag van uw gebruikersbasis.

De `Time between orders` De grafiek toont de gemiddelde en/of mediaan verstreken tijd tussen de eerste en tweede orde van een gebruiker, tweede en derde orde, etc. U kunt [denk na gebruikend deze gegevens om uw e-mailmarketing campagnes te vormen](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

De `Users by lifetime number of orders` In de grafiek wordt het totale aantal gebruikers voor elk levenslange aantal bestellingen weergegeven om een algemeen overzicht te geven van herhaald aankoopgedrag.  

De `Repeat order probability` De grafiek toont de waarschijnlijkheid dat een gebruiker met een bepaald orderaantal een herhaalde aankoop maakt. De waarschijnlijkheid van klanten die `x` bestellingen `(x+1)` bestellingen, verdeel eenvoudig het aantal mensen dat ten minste `(x+1)` aankopen door het aantal personen dat ten minste `x` aankopen.

### Voorbeeld

Aantal klanten dat 1 aankoop heeft gedaan tijdens hun levensduur: `90`

Aantal klanten dat twee aankopen heeft gedaan tijdens hun levensduur: `30`

Aantal klanten dat drie aankopen heeft gedaan tijdens hun levensduur: `10`

In dit voorbeeld is de kans dat klanten die tijdens hun levensduur één aankoop hebben gedaan, de volgende bestelling uitvoeren om een tweede aankoop te doen: `(30 + 10) / (30+10+90) = 30.77%`.

## LTV-groei van klanten

De `Customer LTV growth` dashboard bevat een aantal grafieken waarmee de gemiddelde omzet per gebruiker wordt gevonden. De grafieken worden gesegmenteerd op basis van de gemiddelde opbrengst die binnen of de eerste 30, 60, 90, of 365 dagen na registratie wordt geproduceerd.  

In de onderste rij grafieken worden deze gemiddelden opgesplitst naar aankoopbronnen of demografie om aan te geven welke groepen gebruikers in de loop der tijd de meeste inkomsten genereren.

## Productprestaties

De `Product Performance` het dashboard bevat grafieken die de algemene productprestaties weergeven door het aantal verkochte artikelen en de inkomsten per item weer te geven en de best presterende producten te identificeren .

## Recente activiteit

De `Recent Activity` op het dashboard worden de prestatiegegevens van de afgelopen 30 dagen weergegeven .

## Transactionele gezondheid

De `Transaction Health` het dashboard bevat overzichtsgrafieken van inkomsten , bestellingen en de gemiddelde waarde van bestellingen . Deze grafieken kunnen worden gesegmenteerd door marketingkanalen, demografie of door speciale couponcodes.

## Te gebruiken gebruikers

De `Users to target` Het dashboard bevat tabelachtige diagrammen waarin gebruikers met specifieke gemeenschappelijke aankoopgedragingen worden vermeld. Enkele voorbeelden:

* Lijst met eenmalige kopers die objecten kopen `X` maanden geleden (wie u mogelijk opnieuw wilt activeren)

* Lijst van topspenders (die je misschien gelukkig wilt houden)

* Lijst van hoogste spenders die in het verleden actief waren `X` dagen (wie je wilt belonen)

Met onze gereedschappen voor het exporteren van gegevens is het eenvoudig [e-maillijsten maken van gebruikers met een vergelijkbaar aankoopgedrag voor doelmarketing](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Gebruikersactiviteit

De `User activity` het dashboard omvat grafieken die gebruikers door een verscheidenheid van gegevens, met inbegrip van verwervingsbron, demografie, en gemiddelde eerste keer aan orde segmenteren. Het omvat ook de analyse van de gebruikerscohort, met inbegrip van de algemene gemiddelde levensinkomsten door de registratiemaand van gebruikers.

De `% of cohort members who have purchased` Een grafiek is bijzonder waardevol, aangezien het de omzettingsverhouding (tussen 0 en 1) van gebruikers toont die wordt gebaseerd op wanneer zij registreren (elke lijn vertegenwoordigt een cohort van gebruikers) en wanneer zij hun eerste aankoop maken (bijvoorbeeld, in maand 1, 2, 3... na registratie). Dit kan u tonen dat 10% van gebruikers in maand 1 activeerde, terwijl dit aantal in maand 2, 3, 4.. groeit. en kan later plateau worden.

Doorgaans worden de lijnen in dit diagram horizontaal na een bepaalde periode, wat erop wijst dat weinig extra cohortleden organisch na dat punt omzetten - i, de meeste gebruikers die een aankoop gaan maken hebben dit reeds gedaan. Op dit moment is het zeer onwaarschijnlijk dat deze leden zich zonder tussenkomst tot de kopers zullen wenden. [Het bereiken van hun kennis met aangepaste promoties of specifiek gerichte e-mails is een uiterst risicoloze manier om deze populatie snel om te zetten.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
