---
title: Naamrapporten en -elementen in de handelsinlichtingendienst
description: Leer beste praktijken voor noemende rapporten en elementen in [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Naamrapporten en -elementen

Voordat u aan de slag gaat met het[!DNL Adobe Commerce Intelligence]Adobe wil wat geheimen delen om te slagen. Het is belangrijk om te weten hoe u metriek, filters, enzovoort kunt maken, maar al uw werk kan onverwacht zijn als u niet kunt vinden wat u nodig hebt of als er dubbelzinnigheid is.

## Waarom is nomenclatuur belangrijk? {#why}

De manier u uw berekende kolommen, metriek, en rapporten noemt dicteert het gemak waarin de verschillende gebruikers door uw kunnen navigeren [!DNL Commerce Intelligence] account. Houd bij de naamgeving van deze functies rekening met de volgende drie instellingen:

* **DUIDELIJKHEID** - Je kan dus in één oogopslag zien wat een rapport toont, wat een metrisch doet, enzovoort.
* **CONSISTENTIE** - zodat u (en het Adobe-ondersteuningsteam) eenvoudig elementen en rapporten in uw account kunt vinden en begrijpen.
* **GELOOFWAARDIGHEID** - Om andere gegevensgestuurde elementen te inspireren en te versterken [!DNL Commerce Intelligence] gebruikers, moet u vertrouwen in hoe zij de gegevens begrijpen en gebruiken!

Lees verder voor beproefde en ware nomenclatuurtips!

## Algemene beste praktijken {#general}

### Zich zinvol maken {#meaningful}

Wees waar mogelijk specifiek! Als het bijvoorbeeld het land is, weet u of het de scheepvaart of het factureringsland is? Is het de stad van de gebruiker, of is het de stad van de deal?

**Onjuist voorbeeld:**
Ontvangsten

Dat is onduidelijk en zegt ons niet veel.

**Goede voorbeelden:**
Inkomsten (totaal basisbedrag + kosten) Verzendland van gebruiker

Deze voorbeelden zijn specifiek, wat de kans op verwarring vermindert.

### Verenigbaar zijn met hoofdletters {#capitalize}

[!DNL Adobe] raadt aan om de eerste letter in hoofdletters te plaatsen met de rest van de tekens, tenzij de eigenlijke naamstijl van hoofdletters wordt gebruikt. Bijvoorbeeld: **Volgnummer van de gebruiker** eerder dan **Volgnummer van gebruiker.**

Dit is echt een kwestie van voorkeur, maar het punt om zich te herinneren is om met wat te verenigbaar te zijn u kiest.

### Consistentie van entiteiten {#entity}

U hebt waarschijnlijk al een nomenclatuur bij uw bedrijf. Houd de metriek en de afmetingen die u op zijn plaats zet verenigbaar met wat in andere gegevensbestanden en hulpmiddelen wordt gebruikt. Bijvoorbeeld:

* Gebruiker versus klant vs. lid vs. account
* Bedrijf vs. account vs. organisatie
* Registratie versus ontwerp

### Spelling en grammatica {#spelling}

Controleer de spelling nogmaals en vergeet deze plakbezittingen niet!

## Grafieken {#charts}

Bij naamgeving [grafieken](../tutorials/using-visual-report-builder.md), is het zeer nuttig om deze formule te volgen: **(Gegevensperspectief) + (Metrisch) + (Tijdsperiode) + (Tijdinterval)**

**Onjuist voorbeeld:**
Ontvangsten

Dat vertelt ons niets over het verslag, wat slecht is.

**Goed voorbeeld:**
Gecumuleerde inkomsten van de laatste 30 dagen per maand

Dit vertelt ons **exact** wat staat er in het verslag, wat fantastisch is.

## Dashboards {#dashboards}

De dashboards zouden op manieren moeten worden genoemd die thematisch de rapporten vertegenwoordigen binnen hen. Als het dashboard bijvoorbeeld alleen informatie bevat die betrekking heeft op inkomsten en bestellingen, kunt u het bijvoorbeeld een naam geven die lijkt op **Winkelnaam - Opbrengsten en bestellingen.**

Als het dashboard daarentegen een plaats is waar u experimenteert met verschillende rapporten, kunt u het een naam geven **Sandbox van uw naam** u weet dus dat de verslagen in kwestie concepten zijn .

## Dimension (Berekende kolommen) {#dimensions}

Nieuwe naamgeving [afmetingen](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), is het zeer nuttig om deze formule te volgen: **(Entiteit) + (Nde) + (tijdkader) + (berekening) + (opmerkingen)**. Bijvoorbeeld:

Eerste 30-daagse inkomsten van gebruiker
* Volgnummer van de gebruiker
* bestelnummer van gebruiker (in afwachting van controle)

## Filtersets {#filterset}

[Filtersets](../data-user/reports/ess-manage-data-filters.md) worden gewoonlijk genoemd op manieren die de informatie verklaren zij omvatten of uitsluiten. Een filterset bijvoorbeeld een naam geven **Objecten bestellen die we tellen** staat om het even welke gebruiker toe om binnen te gaan, de logica van de filterreeks te bekijken, en te begrijpen welke ordeinformatie bepaalt wat over de zaken wordt geteld. Vergeet niet dat filtersets op zowel berekende kolommen als metriek kunnen worden toegepast en eenvoudig te begrijpen moeten zijn.

## Metrisch {#metrics}

[Metrisch](../data-user/reports/ess-manage-data-metrics.md) Dit zijn hoofdzakelijk vragen die u regelmatig wilt beantwoorden. Wat was het aantal bestellingen in de afgelopen maand? Wat is de gemiddelde levenwaarde van uw klanten? Het wordt aanbevolen om metriek een naam te geven die het antwoord aangeeft dat gebruikers krijgen. Als u dezelfde maateenheid hebt gefilterd voor een specifieke winkel of afdeling, moet u deze als zodanig labelen. Bijvoorbeeld:

Gemiddelde LTV-winkel van klant (eerste 30 dagen) - Opbrengst

Tot slot kan zelfde metrisch soms door verschillende timestamps worden georganiseerd, afhankelijk van hoe de individuele gebruikers het berekenen. Zo ja, zorg ervoor dat u de tijdstempel in de naam opneemt:

Ontvangsten (verscheept\_at) (gemaakt\_at)

## Omloop omhoog {#wrapup}

Door de stijl- en naamconventies in een vroeg stadium te definiëren, kunt u uw werk sneller uitvoeren [!DNL Commerce Intelligence] account. Denk aan de drie CS&#39;s: duidelijkheid, consistentie en geloofwaardigheid.
