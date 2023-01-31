---
title: Een rapport gebruiken
description: Leer hoe u uw rapportgegevens gebruikt.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Een rapport gebruiken

Rapporten gebruiken in [!DNL MBI] om u te helpen bedrijfsvragen beantwoorden - of u eenvoudig de inkomsten van deze maand vergeleken bij vorig jaar wilt zien of uw aanschafkosten voor uw recentste begrijpen [!DNL Google AdWords] campagne.

Hoe ziet dat pad van vraag tot antwoord er precies uit?

Om u te helpen dit proces visualiseren, hebben wij die route hieronder in kaart gebracht. Dit onderwerp zal wat licht op zowel hoe wij een analytische vraag benaderen als de achterste logistiek die wordt vereist om u de gegevens te krijgen u nodig hebt.

## Beginnen met de vraag

Wij weten dat u constant vragen stelt om uw zaken te verbeteren, van het verhogen van klantentevredenheid aan het drukken van leveringskosten. We zullen ons concentreren op hoe u uw vragen kunt vertalen in analyses die u helpen beslissingen te nemen.

Wij gaan er bijvoorbeeld van uit dat wij de volgende vraag willen beantwoorden:

* Hoe snel converteren mijn nieuwe registranten?

## Een meting identificeren

Met onze vraag is het tijd om een lijst op te stellen van mogelijke analyses en metingen om de vraag te beantwoorden. Voor dit voorbeeld, nadruk op volgende metrisch:

* Gemiddelde tijd van registratie tot eerste aankoopdatum per gebruik.

Zo wordt de gemiddelde tijd weergegeven die verstrijkt tussen de registratiedatum en de eerste aankoopdatum van de gebruikers en wordt een idee gegeven van hoe gebruikers zich gedragen in deze laatste stap in de conversietrechter.

## De gegevens zoeken

Begrijpen wat je moet meten, brengt ons slechts een deel van de weg naar daar. Om de gemiddelde tijd van registratie aan eerste aankoopdatum per gebruiker te beoordelen, moeten wij alle gegevenspunten identificeren die onze maatregel omvat.

Verdeel onze maatstaf in zijn kernonderdelen: we moeten weten hoeveel mensen zich hebben geregistreerd , of hoeveel ; het aantal personen dat een aankoop heeft gedaan; en de tijd die is verstreken tussen deze twee gebeurtenissen.

Op een hoger niveau moeten we weten waar we deze gegevens in de database kunnen vinden, met name:

* De lijst die een rij gegevens registreert telkens als iemand registreert
* De tabel die een gegevensrij vastlegt telkens wanneer iemand een aankoop doet
* De kolom die kan worden gebruikt om verbinding te maken of van verwijzingen te voorzien `purchase` aan de `customer` tabel - hiermee kunnen we weten wie een aankoop heeft gedaan

Op een meer korrelig niveau moeten we de exacte gegevensvelden identificeren die voor deze analyse zullen worden gebruikt:

* De gegevenslijst en de kolom die de registratiedatum van een klant bevatten: bijvoorbeeld `user.created\_at`
* De gegevenstabel en de kolom die een aankoopdatum bevatten: bijvoorbeeld `order.created\_at`

## Gegevenskolommen maken voor analyse

Naast de bovenstaande native gegevenskolommen hebben we ook een reeks berekende gegevensvelden nodig om deze analyse mogelijk te maken, waaronder:

* `Customer's first purchase date` die een specifieke gebruiker terugkeert `MIN(order.created_at`)

Dat zal dan worden gebruikt om:

* `Time between a customer's registration date and first purchase date`, die de tijd van een specifieke gebruiker tussen registratie en eerste aankoopdatum verliest. Dit zal de basis voor onze metrische later zijn.

Beide velden moeten op gebruikersniveau worden gemaakt (bijvoorbeeld op de `user` tabel), zodat de gemiddelde analyse door de gebruikers kan worden genormaliseerd (met andere woorden, de noemer in deze gemiddelde berekening is het aantal gebruikers).

Dit is waar [!DNL MBI] stappen in! U kunt uw [!DNL MBI] data warepot om de bovengenoemde kolommen tot stand te brengen. Neem eenvoudig contact op met ons analyseteam en geef ons de specifieke definitie van uw nieuwe kolommen en wij zullen deze maken. U kunt ook gebruikmaken van onze [Kolomeditor](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Het is aan te raden te vermijden dat u deze berekende gegevensvelden rechtstreeks in uw database maakt, aangezien dit een onnodige belasting voor uw productieservers betekent.

## Metrisch maken

Nu wij de vereiste gegevensgebieden voor onze analyse hebben, is het tijd om relevante metrisch te vinden of te creëren om onze analyse te construeren.

Hier weten we dat we wiskundig de volgende berekening willen uitvoeren:


_[SUM van `Time between a customer's registration date and first purchase date`] / [Totaal aantal klanten dat zich heeft geregistreerd en aangeschaft]_

En we willen deze berekening uitgezet zien in de tijd, of trending, volgens de registratiedatum van een klant. En hier is hoe te [deze metrisch maken](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL MBI]:

1. Ga naar **[!UICONTROL Data]** en selecteert u de `Metrics` tab.
1. Klikken **[!UICONTROL Add New Metric]** en selecteert u de `user` tabel (waar we de bovenstaande afmetingen hebben gemaakt).
1. Selecteer in het vervolgkeuzemenu de optie `Average` op de`Time between a customer's registration date and first purchase date` in de `user` tabel geordend door de `Customer's registration date`  kolom.
1. Voeg relevante filters of filtersets toe.

Deze metrische waarde is nu klaar.

## Het rapport maken

Met de nieuwe metrische opstelling, kunnen wij het gebruiken om over de gemiddelde tijd tussen registratie en eerste aankoopdatum door registratiedatum te rapporteren.

Ga gewoon naar elk dashboard en [een nieuw rapport maken](../../data-user/reports/ess-manage-data-metrics.md) de hierboven gemaakte metrische waarde gebruiken.

### `Visual Report Builder` {#visualrb}

[De `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) is de eenvoudigste manier om uw gegevens te visualiseren. Als u niet vertrouwd met SQL bent of u enkel een rapport wilt snel tot stand brengen, is Visual Report Builder uw beste weddenschap. Met slechts een paar klikken, kunt u metriek toevoegen, uw gegevens segmenteren, en rapporten tot stand brengen aan over uw organisatie. Deze optie is ideaal voor zowel beginners als deskundigen, aangezien hiervoor geen technische expertise vereist is.

|  |  |
|--- |--- |
| **Dit is perfect voor...** | **Dat is niet zo geweldig voor...** |
| - Alle niveaus van analyse/technische ervaring<br>- Snel rapporten maken<br>- Analyses maken om te delen met andere gebruikers | - Analyses die SQL-specifieke functies vereisen<br>- Nieuwe kolommen testen - berekende kolommen zijn afhankelijk van updatecycli voor de initiële gegevenspopulatie, terwijl die welke met SQL worden gemaakt niet |

{style=&quot;table-layout:auto&quot;}

### Beschrijvingen en afbeeldingen rapporteren

#### Beschrijvingen toevoegen aan rapporten

Wanneer het creëren van rapporten die met andere leden van uw team zullen worden gedeeld, adviseren wij toevoegend beschrijvingen die andere gebruikers zullen toestaan om uw analyse beter te begrijpen.

1. Klikken **[!UICONTROL i]** boven aan een rapport.
1. Voer in het tekstvak een beschrijving in.
1. Klikken **[!UICONTROL Save Description]**.

Laten we eens kijken:

![Grafiekbeschrijving](../../assets/Chart_Description.gif)

#### Rapporten exporteren als afbeeldingen

Wilt u een rapport opnemen in een presentatie of document? Elk rapport kan als een afbeelding worden opgeslagen (in de PNG-, PDF- of SVG-indeling) met de opdracht `Report Options` in de rechterbovenhoek van elk rapport.

1. Klik op het tandwielpictogram in de rechterbovenhoek van een willekeurig rapport.
1. Selecteer in het vervolgkeuzemenu de optie `Enlarge`.
1. Wanneer het rapport wordt vergroot, klikt u op **[!UICONTROL Download]** in de rechterbovenhoek van het rapport.
1. Selecteer de gewenste afbeeldingsindeling in het vervolgkeuzemenu. Het downloaden begint direct.

Kijk eens:

![](../../assets/exp-rep-as-image.gif)
