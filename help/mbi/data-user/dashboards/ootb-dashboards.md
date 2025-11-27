---
title: Opgenomen dashboards
description: Leer hoe u de gezondheid van essentiële gegevens kunt controleren, zoals inkomsten tijdens de levensduur van de gebruiker, het aantal herhaalde aankopen en meer, en zo een solide basis voor toekomstige exploratie kunt leggen.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 3a7423c9dd0f957b77baa27b3447a715caad017b
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Opgenomen dashboards

[!DNL Adobe] biedt `eCommerce` en `SaaS` Starter Packages aan. Deze pakketten, die door analisten van Adobe worden gecreeerd, bevatten een aangepaste reeks dashboards en rapporten voor uw dataset. Met de analyses in deze pakketten kunt u de gezondheid van essentiële gegevens controleren, zoals inkomsten tijdens de levensduur van de gebruiker, het aantal herhaalde aankopen en nog veel meer. Op die manier wordt een solide basis gelegd voor toekomstige exploratie.

>[!NOTE]
>
>De beschikbaarheid van sommige dashboards hangt van uw dataset af.

Als u vragen hebt of u geinteresseerd in het toevoegen van een pakket aan uw rekening bent, leg a [&#x200B; steunkaartje &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) voor hulp voor.

## Uitvoerend overzicht

Het dashboard van `executive overview` wordt gebouwd van grafieken die op andere dashboards bestaan. Dit dashboard is een overzicht op hoog niveau van uw gegevens en bevat grafieken die dagelijks worden gecontroleerd, terwijl andere dashboards meer gedetailleerde informatie bevatten. In eerste instantie wordt deze ingesteld als het standaarddashboard in elke account.

Er is een algemene set grafieken voor u opgenomen. Adobe raadt u aan dit dashboard aan uw wensen aan te passen door andere grafieken toe te voegen die u het vaakst gebruikt.

## Cohortanalyse

Het dashboard van `cohort analysis` omvat een reeks grafieken die de gemiddelde de inkomstengroei van de gebruikersleven en de stijgende opbrengstgroei tonen gegroepeerd door registratiecolades. Dit onthult of de waarde van het klantenleven (LTV), de waarde van een klant aan een zaken, stijgt in tijd, en ook tendensen rond de groei van LTV identificeert. Door gebrek, *worden alle geregistreerde gebruikers (kopers en niet-kopers) rekenschap gegeven* in de gemiddelde berekening LTV - zie het [&#x200B; onderwerp van de cohortanalyse &#x200B;](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Dit dashboard kan ook cohortgrafieken bevatten die de levensinkomsten van gebruikers van een specifieke aanschafbron, kanaal of demografisch (bijvoorbeeld New York of Californië) analyseren. Dit moet aantonen hoe u LTV voor specifieke segmenten van uw gebruikersbasis kunt analyseren en zien of één groep of een andere hogere LTV in tijd opbrengt.

Voor meer informatie over cohorts, zie [&#x200B; Uitvoerend de Analyse van de Cohort &#x200B;](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Als u momenteel geen bron van de gebruikersverwerving volgt, zie het [&#x200B; Overzicht van de Gegevens van de Acquisitie Source van het Spoor &#x200B;](../../data-analyst/analysis/google-track-user-acq.md).

## Overzicht van e-mail

Het dashboard van `Email Summary` bevat een voorbeeldset met grafieken die kunnen worden gebruikt in een geautomatiseerde dagelijkse e-mailsamenvatting. Verwijs naar [&#x200B; het creëren van geautomatiseerde e-mailoverzichten &#x200B;](../../data-user/export-data/email-summaries.md) voor meer informatie bij het vormen van e-mailoverzichten.  

## Retentie gezondheid

Het dashboard van `Retention health` onthult het herhaalde aankoopgedrag van uw gebruikersbasis.

In het `Time between orders` -diagram wordt de gemiddelde en/of gemiddelde verstreken tijd weergegeven tussen de eerste en tweede volgorde van een gebruiker, de tweede en de derde volgorde, enzovoort. U zou kunnen overwegen gebruikend deze gegevens om uw e-mail marketing campagnes te vormen.

In de grafiek `Users by lifetime number of orders` wordt het totale aantal gebruikers voor elk levenslange aantal bestellingen weergegeven om een algemeen overzicht te geven van herhaald aankoopgedrag.  

In het `Repeat order probability` -diagram ziet u hoe waarschijnlijk het is dat een gebruiker met een bepaald ordernummer een herhaalde aankoop uitvoert. Als u wilt zien hoe groot de kans is dat klanten die `x` -orders hebben geplaatst, `(x+1)` -bestellingen kunnen uitvoeren, deelt u gewoon het aantal personen dat ten minste `(x+1)` -aankopen heeft gedaan door het aantal personen dat ten minste `x` -aankopen heeft gedaan.

### Voorbeeld

Aantal klanten dat een aankoop heeft gedaan tijdens hun levensduur: `90`

Aantal klanten dat twee aankopen heeft gedaan tijdens hun levensduur: `30`

Aantal klanten dat drie aankopen heeft gedaan tijdens hun levensduur: `10`

In dit voorbeeld is de waarschijnlijkheid dat klanten die in hun leven één aankoop hebben gedaan een tweede aankoop kunnen doen, als volgt: `(30 + 10) / (30+10+90) = 30.77%` .

## LTV-groei van klanten

Het dashboard van `Customer LTV growth` bevat een reeks grafieken die de gemiddelde opbrengst per gebruiker vindt. De grafieken worden gesegmenteerd op basis van de gemiddelde opbrengst die binnen of de eerste 30, 60, 90, of 365 dagen na registratie wordt geproduceerd.  

Uit de onderste rij grafieken blijkt dat deze gemiddelden zijn gesegmenteerd naar aankoopbronnen of demografie om aan te geven welke groepen gebruikers in de loop der tijd de meeste inkomsten genereren.

## Productprestaties

Het dashboard van `Product Performance` bevat grafieken die de algemene productprestaties weergeven door het aantal verkochte items en de omzet per item weer te geven en de producten die het meest presteren te identificeren.

## Recente activiteit

Op het dashboard van `Recent Activity` worden de prestatiegegevens van de afgelopen 30 dagen weergegeven.

## Transactionele gezondheid

Het dashboard van `Transaction Health` bevat overzichtsgrafieken van opbrengsten, bestellingen en gemiddelde orderwaarde. Deze grafieken kunnen worden gesegmenteerd door marketingkanalen, demografie of door speciale couponcodes.

## Te gebruiken gebruikers

Het dashboard van `Users to target` bevat tabellen met diagrammen waarin gebruikers met bepaalde gemeenschappelijke aankoopgedragingen worden vermeld. Enkele voorbeelden:

* Lijst met eenmalige kopers die `X` maanden geleden aanschaffen (wie je wellicht opnieuw wilt activeren)

* Lijst van topspenders (die je misschien gelukkig wilt houden)

* Lijst met topsponsors die de afgelopen `X` dagen actief waren (die u mogelijk wilt belonen)

Met de gereedschappen voor het exporteren van gegevens kunt u e-maillijsten maken van gebruikers met een vergelijkbaar aankoopgedrag voor de doelmarketing.

## Gebruikersactiviteit

Het dashboard van `User activity` omvat grafieken die gebruikers door diverse gegevens, met inbegrip van verwervingsbron, demografie, en gemiddelde eerste keer aan orde segmenteren. Het omvat ook de analyse van de gebruikerscohort, met inbegrip van de algemene gemiddelde levensinkomsten door de registratiemaand van gebruikers.

Het diagram `% of cohort members who have purchased` is waardevol omdat het de conversieverhouding (van 0 tot en met 1) van gebruikers weergeeft op basis van het tijdstip waarop ze zich registreren (elke regel vertegenwoordigt een cohort van gebruikers). Het toont ook wanneer zij hun eerste aankoop (bijvoorbeeld in maand 1, 2, 3... na registratie) maken. Dit kan u aantonen dat 10% van gebruikers geactiveerd in maand 1, terwijl dit aantal groeit in maand 2, 3, 4.. en kan later plateau.

Doorgaans worden de lijnen in dit diagram horizontaal na een bepaalde periode. Dit wijst erop dat weinig extra cohort leden organisch na dat punt omzetten - de meeste gebruikers die een aankoop gaan maken hebben reeds dit gedaan. Op dit moment is het zeer onwaarschijnlijk dat deze leden zich zonder tussenkomst tot de kopers zullen wenden. Het bereiken van naar hen met aangepaste promoties of gerichte e-mails is een manier met weinig risico om deze populatie snel om te zetten.
