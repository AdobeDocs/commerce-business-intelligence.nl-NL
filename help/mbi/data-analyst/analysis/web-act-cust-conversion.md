---
title: De activiteiten van de Website en de Conversietarieven van de Klant analyseren
description: Leer hoe u een dashboard instelt waarmee uw websiteactiviteit (inclusief paginaweergaven, sessies en gebruikers) en de conversiesnelheid van uw klant in de loop van de tijd worden bijgehouden.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Website-activiteit analyseren

[!DNL MBI] kunt u uw gegevens over de advertentiekosten eenvoudig integreren met de rest van uw gegevens. Hierdoor kunt u niet alleen de activiteiten van uw website begrijpen, maar kunt u ook het percentage bezoekers op uw website afleiden dat een geregistreerde gebruiker wordt of een aankoop doet.

Dit artikel laat zien hoe u een dashboard instelt waarmee uw websiteactiviteit (inclusief paginaweergaven, sessies en gebruikers) en de conversiesnelheid van uw klant in de loop van de tijd worden bijgehouden.

## Vereisten

**Je gegevens over advertentiekosten importeren** - Verbinden [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) tot [!DNL MBI] - hiermee worden uw [!DNL AdWords] uitgaven in MBI.

**Kanaalgegevens van verwervingskanalen bijhouden** - Als u uw [!DNL Google AdWords] gegevens aan specifieke orden in uw gegevensbestand, moet u [traceringsgebruikersovername](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. Hierdoor kunt u elke bestelling verbinden met een utm-bron en een medium.

## Aankoopcampagnes voor gebruikers

Deze inzameling van rapporten wordt gebouwd gebruikend het volgende:

* Metriek die automatisch worden gegenereerd wanneer u uw [!DNL Google AdWords] data
* Standaardwaarden die al beschikbaar moeten zijn voor uw account, zoals `Number of orders` en `New users`
* Dimension die zijn gemaakt toen u uw [!DNL Google Analytics Ecommerce] gegevens aan uw gegevensbestand, zoals de utm bron van de orde en het utm middel van de orde. Neem contact op met het ondersteuningsteam als deze velden momenteel niet beschikbaar zijn in uw account

## Uw rapporten samenstellen

**Begin door een rapport te creëren dat het aantal paginameningen, zittingen, en gebruikers in tijd toont:**

1. Maak een rapport.
1. Klikken **[!UICONTROL Add Metric]** en vervolgens met de muis over de [!DNL Google Analytics] onder aan het vervolgkeuzemenu selecteert u `Page Views`.
1. Voeg nog een metrische waarde toe, waarbij u de muis weer boven de metrische waarde houdt [!DNL Google Analytics] deze keer selecteren `Sessions`.
1. Voeg een derde metrisch toe, opnieuw beweegt over [!DNL Google Analytics] deze keer selecteren `Users`.
1. Wijzig nu uw tijdsperiode in een bewegend bereik, van 31 dagen geleden tot 1 dag geleden, en pas het tijdsinterval aan `by day`.
1. Geef uw rapport een naam (bijvoorbeeld `Page views, sessions and users by day`) en klik op **[!UICONTROL Save]**.

**In het tweede rapport wordt gekeken naar het aantal paginaweergaven in het afgelopen jaar:**

1. Maak een rapport.
1. Klikken **[!UICONTROL Add Metric]**, muisaanwijzer over de [!DNL Google Analytics] onder aan het vervolgkeuzemenu selecteert u _Paginaweergaven_.
1. Verander uw tijdspanne in een bewegende waaier, van 13 maanden geleden tot 1 maand geleden, en pas het tijdinterval aan `by month`.
1. Geef uw rapport een naam, zoals `Page views by month,` en klik op **[!UICONTROL Save]**.

**In de derde grafiek wordt gekeken naar de stuitingsgraad in het afgelopen jaar:**

1. Maak een rapport.
1. Klikken **[!UICONTROL Add Metric]**, muisaanwijzer over de [!DNL Google Analytics] onder aan het vervolgkeuzemenu selecteert u _Stuitpercentage_.
1. Verander uw tijdspanne in een bewegende waaier, van 13 maanden geleden tot 1 maand geleden, en pas het tijdinterval aan `by month`.
1. Geef uw rapport een naam, zoals `Bounce rate by month`en klik op **[!UICONTROL Save]**.

**Nu, bekijk de gemiddelde zittingslengte van nieuwe bezoekers in vergelijking met terugkerende bezoekers:**

1. Maak een rapport.
1. Klikken **UICONTROL metrisch toevoegen**, muisaanwijzer over de [!DNL Google Analytics] onder aan het vervolgkeuzemenu selecteert u `Average Session Length`.
1. Verander uw tijdspanne in een bewegende waaier, van 13 maanden geleden tot 1 maand geleden, en pas het tijdinterval aan `by month`?
1. Voeg een `Group by` en selecteert u `New or returning visitor`.  Controleer de `Show All` vak; klik vervolgens op **[!UICONTROL Apply]**.
1. Geef uw rapport een naam, zoals `Average session length`en klik op **[!UICONTROL Save]**.

**Kijk vervolgens in de afgelopen 30 dagen naar uw belangrijkste verwijzingsdomeinen:**

1. Maak een rapport.
1. Klikken **[!UICONTROL Add Metric]**, muisaanwijzer over de [!DNL Google Analytics] onder aan het vervolgkeuzemenu selecteert u `Sessions`.
1. Verander uw tijdspanne in een bewegende waaier, van 31 dagen geleden tot 1 dag geleden, en pas het tijdinterval aan `none`.
1. Voeg een `Group by` en selecteert u `ga:source`.  Controleer de _Alles tonen_ vak; klik vervolgens op **[!UICONTROL Apply]**.
1. Nog een toevoegen `group by` en selecteert u `ga:medium`. Controleer nogmaals de `Show All` vak; klik vervolgens op **[!UICONTROL Apply]**.
1. Geef uw rapport een naam, zoals `Top 20 Referring Domains, 30 Days`en klik op **[!UICONTROL Save]**.

**Kijk tot slot naar de conversie:**

1. Maak een rapport.
1. Voeg de volgende metriek toe:

* `New users`
   * Klikken **[!UICONTROL Hide]** onder de metrische naam

* `Number of orders`
   * Een filter toevoegen voor `Customer's order number` = 1 en klik **[!UICONTROL Apply]**
   * Wijzig de naam van de metrisch door op de naam van de metrische methode te klikken en deze aan te roepen `Number of first orders`en klik vervolgens op **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** de

* `Users`
   * **[!UICONTROL Hide]** de
   * De tijdsperiode wijzigen in `24 months ago to now`en pas het tijdsinterval aan `by month`.
   * Voeg de volgende formules toe door te klikken **[!UICONTROL Formula]**.
   * A/D en klik vervolgens op **[!UICONTROL Apply]**
   * De naam van de formule wijzigen `Registration conversion`
   * B/D en klik vervolgens op **[!UICONTROL Apply]**
   * De naam van de formule wijzigen `First order conversion`
   * C/D en klik vervolgens op **[!UICONTROL Apply]**
   * De naam van de formule wijzigen `Any order conversion`

* Geef uw rapport nu een naam, zoals `Conversion by month`en klik vervolgens op **[!UICONTROL Save]**.

## Volgende stappen

Nu u toegang tot gegevens over uw Webverkeer en omzettingspercentages hebt, kunt u beginnen om dit te ontginnen om bedrijfsbesluiten, zoals te drijven welke plaatsen het best in het besturen van verkeer aan uw plaats zijn? of Welke van uw campagnes zijn het meest effectief in het verwerven van klanten met de hoge levenwaarde?

Als u de strategie voor uitgaven en marketing aanpast, kunt u de resultaten blijven bijhouden in [!DNL MBI], herhalend op dit dashboard om aan de evoluerende prioriteiten van uw bedrijf te voldoen.
