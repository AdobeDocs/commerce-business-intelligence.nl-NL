---
title: Een rapport gebruiken
description: Leer hoe u uw rapportgegevens gebruikt.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Een rapport gebruiken

Rapporten gebruiken in [!DNL MBI] om u te helpen bedrijfsvragen beantwoorden - of u eenvoudig de inkomsten van deze maand vergeleken bij vorig jaar wilt zien of uw aanschafkosten voor uw recentste begrijpen [!DNL Google AdWords] campagne.

Hoe ziet dat pad van vraag tot antwoord er precies uit?

Om u te helpen dit proces visualiseren, wordt die route hieronder in kaart gebracht. Dit onderwerp werpt licht op zowel hoe u een analytische vraag benadert, als de achterste logistiek die wordt vereist om u de gegevens te krijgen u nodig hebt.

## Beginnen met de vraag

U weet dat u constant vragen stelt om uw zaken te verbeteren, van het verhogen van klantentevredenheid aan het drukken van leveringskosten. U richt zich op hoe te om uw vragen in analyses te vertalen die u helpen besluiten drijven.

In dit voorbeeld gaat u ervan uit dat u de volgende vraag wilt beantwoorden:

* Hoe snel converteren mijn nieuwe registranten?

## Een meting identificeren

Het wordt tijd om een lijst van mogelijke analyses en metingen te identificeren om de vraag te helpen beantwoorden. Voor dit voorbeeld, nadruk op volgende metrisch:

* Gemiddelde tijd van registratie tot eerste aankoopdatum per gebruik.

Dit onthult de gemiddelde tijd die tussen registratiedatum en de eerste aankoopdatum van de gebruikers vervalt en geeft een idee over hoe de gebruikers zich in deze laatste stap in de conversietrechter gedragen.

## De gegevens zoeken

Begrijpen wat je moet meten, brengt ons slechts een deel van de weg naar daar. Om de gemiddelde tijd van registratie aan eerste aankoopdatum per gebruiker te beoordelen, moet u alle gegevenspunten identificeren die uw maatregel van wordt samengesteld.

Verdeel uw maatstaf in de kerncomponenten. U moet het aantal personen weten dat zich heeft geregistreerd, het aantal personen dat een aankoop heeft gedaan en de tijd die is verstreken tussen deze twee gebeurtenissen.

Op een hoger niveau, moet u weten waar te om deze gegevens in het gegevensbestand te vinden, specifiek:

* De lijst die een rij gegevens registreert telkens als iemand registreert
* De lijst die een gegevensrij registreert die telkens als iemand een aankoop maakt
* De kolom die kan worden gebruikt om verbinding te maken of van verwijzingen te voorzien `purchase` aan de `customer` tabel - hiermee kunnen we zien wie een aankoop heeft gedaan

Op een meer korrelig niveau, moet u de nauwkeurige gegevensgebieden identificeren die voor deze analyse worden gebruikt:

* De gegevenslijst en de kolom die de registratiedatum van een klant bevatten: bijvoorbeeld `user.created\_at`
* De gegevenstabel en de kolom die een aankoopdatum bevatten: bijvoorbeeld `order.created\_at`

## Gegevenskolommen maken voor analyse

Naast de bovenstaande native gegevenskolommen hebt u ook een set berekende gegevensvelden nodig om deze analyse mogelijk te maken, waaronder:

* `Customer's first purchase date` die een specifieke gebruiker terugkeert `MIN(order.created_at`)

Dat wordt dan gebruikt om tot stand te brengen:

* `Time between a customer's registration date and first purchase date`, die de tijd retourneert die een specifieke gebruiker heeft tussen de registratie en de eerste aankoopdatum verstreken. Dit is de basis voor metrisch later.

Beide velden moeten op gebruikersniveau worden gemaakt (bijvoorbeeld op de `user` tabel). Hierdoor kan de gemiddelde analyse door de gebruikers worden genormaliseerd (met andere woorden, de noemer in deze gemiddelde berekening is het aantal gebruikers).

Dit is waar [!DNL MBI] stappen in! U kunt uw [!DNL MBI] Data Warehouse om de bovenstaande kolommen te maken. Neem contact op met het team van Adobe-analisten en geef ons de specifieke definitie van uw nieuwe kolommen voor het maken. U kunt ook de opdracht [Kolomeditor](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Het is aan te raden te vermijden dat u deze berekende gegevensvelden rechtstreeks in uw database maakt, aangezien dit een onnodige belasting voor uw productieservers betekent.

## Metrisch maken

Nu u de vereiste gegevensgebieden voor de analyse hebt, is het tijd om relevante metrisch te vinden of tot stand te brengen om uw analyse te construeren.

Hier wilt u de volgende berekening uitvoeren:


_[SUM van `Time between a customer's registration date and first purchase date`] / [Totaal aantal klanten dat zich heeft geregistreerd en aangeschaft]_

En u wilt deze berekening in tijd, of trending, volgens de registratiedatum van een klant in kaart brengen. En hier is hoe te [deze metrisch maken](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL MBI]:

1. Ga naar **[!UICONTROL Data]** en selecteert u de `Metrics` tab.
1. Klikken **[!UICONTROL Add New Metric]** en selecteert u de `user` tabel (waarin u de bovenstaande afmetingen hebt gemaakt).
1. Selecteer in het vervolgkeuzemenu de optie `Average` op de`Time between a customer's registration date and first purchase date` in de `user` tabel geordend door de `Customer's registration date`  kolom.
1. Voeg relevante filters of filtersets toe.

Deze metrische waarde is nu klaar.

## Het rapport maken

Met de nieuwe metrische opstelling, kunt u het gebruiken om over de gemiddelde tijd tussen registratie en eerste aankoopdatum door registratiedatum te melden.

Ga gewoon naar elk dashboard en [een rapport maken](../../data-user/reports/ess-manage-data-metrics.md) de hierboven gemaakte metrische waarde gebruiken.

### `Visual Report Builder` {#visualrb}

[De `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) is de eenvoudigste manier om uw gegevens te visualiseren. Als u niet vertrouwd met SQL bent of u een rapport wilt snel tot stand brengen, is Visual Report Builder uw beste weddenschap. Met slechts een paar klikken, kunt u metriek toevoegen, uw gegevens segmenteren, en rapporten tot stand brengen aan over uw organisatie. Deze optie is ideaal voor zowel beginners als deskundigen, aangezien hiervoor geen technische expertise vereist is.

|  |  |
|--- |--- |
| **Dit is perfect voor...** | **Dat is niet zo geweldig voor...** |
| - Alle niveaus van analyse/technische ervaring<br>- Snel rapporten maken<br>- Analyses maken om te delen met andere gebruikers | - Analyses die SQL-specifieke functies vereisen<br>- Het testen van nieuwe kolommen - de berekende kolommen hangen van updatecycli voor aanvankelijke gegevensbevolking af, terwijl die gecreeerd gebruikend SQL niet zijn. |

{style="table-layout:auto"}

### Beschrijvingen en afbeeldingen rapporteren

#### Beschrijvingen toevoegen aan rapporten

Bij het maken van rapporten die worden gedeeld met andere teamleden, raadt Adobe aan beschrijvingen toe te voegen waarmee andere gebruikers uw analyse beter kunnen begrijpen.

1. Klikken **[!UICONTROL i]** boven aan een rapport.
1. Voer in het tekstvak een beschrijving in.
1. Klikken **[!UICONTROL Save Description]**.

Zie hieronder:

![Grafiekbeschrijving](../../assets/Chart_Description.gif)

#### Rapporten exporteren als afbeeldingen

Wilt u een rapport opnemen in een presentatie of document? Elk rapport kan als een afbeelding worden opgeslagen (in de PNG-, PDF- of SVG-indeling) met de opdracht `Report Options` in de rechterbovenhoek van elk rapport.

1. Klik op het tandwielpictogram in de rechterbovenhoek van een willekeurig rapport.
1. Selecteer in het vervolgkeuzemenu de optie `Enlarge`.
1. Wanneer het rapport wordt vergroot, klikt u op **[!UICONTROL Download]** in de rechterbovenhoek van het rapport.
1. Selecteer de gewenste afbeeldingsindeling in het vervolgkeuzemenu. Het downloaden begint direct.

Zie hieronder:

![](../../assets/exp-rep-as-image.gif)
