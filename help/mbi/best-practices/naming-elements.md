---
title: Naamrapporten en -elementen in Commerce Intelligence
description: Leer beste praktijken voor het noemen van rapporten en elementen in  [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Naamrapporten en -elementen

Voordat u begint te bouwen in [!DNL Adobe Commerce Intelligence] , wil Adobe enkele geheimen delen om succes te boeken. Het is belangrijk om te weten hoe u metriek, filters, enzovoort kunt maken, maar al uw werk kan onophoudelijk zijn als u niet kunt vinden wat u nodig hebt of als er dubbelzinnigheid is.

## Waarom is nomenclatuur belangrijk? {#why}

De manier waarop u de berekende kolommen, metriek, en rapporten noemt dicteert het gemak waarin de verschillende gebruikers door uw [!DNL Commerce Intelligence] rekening kunnen navigeren. Houd bij de naamgeving van deze functies rekening met de volgende drie instellingen:

* **DUIDELIJKHEID** - Zo kunt u bij een blik vertellen wat een rapport toont, wat metrisch doet, etc.
* **CONSISTENTIE** - zodat u (en het de steunteam van Adobe) elementen en rapporten in uw rekening gemakkelijk vinden en kunnen begrijpen.
* **CREDIBILITY** - om andere gegeven-gedreven [!DNL Commerce Intelligence] gebruikers te inspireren en te machtigen, moet u vertrouwen in verhogen hoe zij de gegevens begrijpen en gebruiken!

Lees verder voor beproefde en ware nomenclatuurtips!

## Algemene beste praktijken {#general}

### Zich zinvol maken {#meaningful}

Wees waar mogelijk specifiek! Als het bijvoorbeeld het land is, weet u of het de scheepvaart of het factureringsland is? Is het de stad van de gebruiker, of is het de stad van de deal?

**Slecht voorbeeld:**
Ontvangsten

Dat is onduidelijk en zegt ons niet veel.

**Goede voorbeelden:**
Ontvangsten (totaal basisbedrag + vergoeding)
Verzendland van gebruiker

Deze voorbeelden zijn specifiek, wat de kans op verwarring vermindert.

### Verenigbaar zijn met hoofdletters {#capitalize}

[!DNL Adobe] raadt aan eerste letter in hoofdletters te gebruiken met de rest van de tekens in kleine letters, tenzij de eigenlijke naamstijl van hoofdletters wordt gebruikt. Bijvoorbeeld, **de ordeaantal van de Gebruiker** eerder dan **Aantal van de Orde van de Gebruiker.**

Dit is echt een kwestie van voorkeur, maar het punt om zich te herinneren is om met wat te verenigbaar te zijn u kiest.

### Consistentie van entiteiten {#entity}

U hebt waarschijnlijk al een nomenclatuur bij uw bedrijf. Houd de metriek en de afmetingen die u op zijn plaats zet verenigbaar met wat in andere gegevensbestanden en hulpmiddelen wordt gebruikt. Bijvoorbeeld:

* Gebruiker versus klant vs. lid vs. account
* Bedrijf vs. account vs. organisatie
* Registratie versus ontwerp

### Spelling en grammatica {#spelling}

Controleer de spelling nogmaals en vergeet deze plakbezittingen niet!

## Grafieken {#charts}

Wanneer het noemen van [&#x200B; grafieken &#x200B;](../tutorials/using-visual-report-builder.md), is het nuttigst om deze formule te volgen: **(het Perspectief van Gegevens) + (Metrisch) + (de Periode van de Tijd) + (het Interval van de Tijd)**

**Slecht voorbeeld:**
Ontvangsten

Dat vertelt ons niets over het verslag, wat slecht is.

**Goed voorbeeld:**
Gecumuleerde inkomsten van de laatste 30 dagen per maand

Dit vertelt ons **precies** wat in het rapport is, wat fantastisch is.

## Dashboards {#dashboards}

De dashboards zouden op manieren moeten worden genoemd die thematisch de rapporten vertegenwoordigen binnen hen. Bijvoorbeeld, als uw dashboard slechts informatie met betrekking tot opbrengst en orden bevat, denk na noemend het iets als **Naam van de Opslag - Inkomsten en orden.**

Omgekeerd, als uw dashboard een plaats is waar u met verschillende rapporten experimenteert, denk na noemend het **Sandbox van Uw Naam** zodat u weet dat de rapporten bevat binnen concepten zijn.

## Afmetingen (berekende kolommen) {#dimensions}

Wanneer het noemen van nieuwe [&#x200B; dimensies &#x200B;](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), is het nuttigst om deze formule te volgen: **(Entiteit) + (Nde) + (tijdkader) + (berekening) + (commentaren)**. Bijvoorbeeld:

Eerste 30-daagse inkomsten van gebruiker
* Volgnummer van de gebruiker
* bestelnummer van gebruiker (in afwachting van controle)

## Filtersets {#filterset}

[&#x200B; de reeksen van de Filter &#x200B;](../data-user/reports/ess-manage-data-filters.md) worden typisch genoemd op manieren die de informatie verklaren zij of uitsluiten. Bijvoorbeeld, het noemen van de punten van de filterreeks **Orde wij tellen** staat om het even welke gebruiker toe om binnen te gaan, de logica van de filterreeks te bekijken, en te begrijpen welke ordeinformatie bepaalt wat over de zaken wordt geteld. Vergeet niet dat filtersets op zowel berekende kolommen als metriek kunnen worden toegepast en eenvoudig te begrijpen moeten zijn.

## Metrisch {#metrics}

[&#x200B; Metriek &#x200B;](../data-user/reports/ess-manage-data-metrics.md) zijn hoofdzakelijk vragen die u antwoorden aan regelmatig wilt. Wat was het aantal bestellingen in de afgelopen maand? Wat is de gemiddelde levenwaarde van uw klanten? Het wordt aanbevolen om metriek een naam te geven die het antwoord aangeeft dat gebruikers krijgen. Als u dezelfde maateenheid hebt gefilterd voor een specifieke winkel of afdeling, moet u deze als zodanig labelen. Bijvoorbeeld:

Gemiddelde LTV van klant (eerste 30 dagen)
Winkelnaam - Opbrengsten

Tot slot kan zelfde metrisch soms door verschillende timestamps worden georganiseerd, afhankelijk van hoe de individuele gebruikers het berekenen. Zo ja, zorg ervoor dat u de tijdstempel in de naam opneemt:

Opbrengst (verzonden\_bij)
Opbrengsten (gemaakt\_at)

## Omloop omhoog {#wrapup}

Als u al een begin maakt met het maken van stijl- en naamconventies, kunt u uw account instellen op succes in [!DNL Commerce Intelligence] . Denk aan de drie Cs: duidelijkheid, consistentie en geloofwaardigheid.
