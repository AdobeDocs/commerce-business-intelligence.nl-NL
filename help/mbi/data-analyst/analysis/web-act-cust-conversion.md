---
title: De activiteiten van de Website en de Conversietarieven van de Klant analyseren
description: Leer hoe u een dashboard instelt waarmee uw websiteactiviteit (inclusief paginaweergaven, sessies en gebruikers) en de conversiesnelheid van uw klant in de loop van de tijd worden bijgehouden.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Website-activiteit analyseren

Met [!DNL Adobe Commerce Intelligence] kunt u uw gegevens over de advertentiekosten eenvoudig integreren met de rest van uw gegevens. Hierdoor kunt u niet alleen de activiteiten van uw website begrijpen, maar kunt u ook het percentage bezoekers op uw website afleiden dat een geregistreerde gebruiker wordt of een aankoop doet.

In dit onderwerp ziet u hoe u een dashboard instelt waarmee uw websiteactiviteit (inclusief paginaweergaven, sessies en gebruikers) en de conversiesnelheid van uw klant in de loop van de tijd worden bijgehouden.

## Vereisten

**de Invoer uw reclame kostengegevens** - verbindt [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md) met [!DNL Adobe Commerce Intelligence] - dit synchroniseert automatisch uw [!DNL AdWords] uitgaven in Commerce Intelligence.

**gegevens van het kanaal van de gebruikersverwerving van het Spoor** - om uw [!DNL Google AdWords] gegevens aan specifieke orden in uw gegevensbestand te binden, moet u [ gebruikersverwerving ](../analysis/google-track-user-acq.md) volgen via [!DNL Google Analytics E-commerce]. Hierdoor kunt u elke bestelling verbinden met een utm-bron en een medium.

## Aankoopcampagnes voor gebruikers

Deze inzameling van rapporten wordt gebouwd gebruikend het volgende:

* Metriek die automatisch worden gegenereerd wanneer u de [!DNL Google AdWords] -gegevens aansluit
* Standaardwaarden die al beschikbaar moeten zijn voor uw account, zoals `Number of orders` en `New users`
* Dimensies die worden gemaakt wanneer u uw [!DNL Google Analytics Ecommerce] -gegevens koppelt aan uw database, zoals de utm-bron van de order en het utm-medium van de order. Neem contact op met het ondersteuningsteam als deze velden momenteel niet beschikbaar zijn in uw account

## Uw rapporten samenstellen

**Begin door een rapport te creëren dat het aantal paginameningen, zittingen, en gebruikers in tijd toont:**

1. Maak een rapport.
1. Klik op **[!UICONTROL Add Metric]**, klik vervolgens met de muis over de [!DNL Google Analytics] -sectie onder aan het vervolgkeuzemenu en selecteer `Page Views` .
1. Voeg nog een metrische waarde toe, waarbij u opnieuw de muis boven de sectie [!DNL Google Analytics] houdt en nu `Sessions` selecteert.
1. Voeg een derde metrische waarde toe, waarbij u opnieuw de muis boven de sectie [!DNL Google Analytics] houdt en nu `Users` selecteert.
1. Wijzig nu de tijdsperiode in een bewegend bereik, van 31 dagen geleden tot 1 dag geleden, en wijzig het tijdsinterval in `by day` .
1. Geef uw rapport een naam (bijvoorbeeld `Page views, sessions and users by day` ) en klik op **[!UICONTROL Save]** .

**het tweede rapport kijkt naar het aantal paginameningen over het afgelopen jaar:**

1. Maak een rapport.
1. Klik **[!UICONTROL Add Metric]**, muis over de [!DNL Google Analytics] sectie bij de bodem van dropdown en selecteer _de Mening van de Pagina_.
1. Wijzig de tijdsperiode in een bewegend bereik, van 13 maanden geleden tot 1 maand geleden, en pas het tijdsinterval aan `by month` .
1. Geef uw rapport een naam, zoals `Page views by month,` en klik **[!UICONTROL Save]**.

**de derde grafiek bekijkt het stuitpercentage over het afgelopen jaar:**

1. Maak een rapport.
1. Klik **[!UICONTROL Add Metric]**, muis over de [!DNL Google Analytics] sectie bij de bodem van dropdown en selecteer _Stuitsnelheid_.
1. Wijzig de tijdsperiode in een bewegend bereik, van 13 maanden geleden tot 1 maand geleden, en pas het tijdsinterval aan `by month` .
1. Geef uw rapport een naam, zoals `Bounce rate by month`, en klik **[!UICONTROL Save]**.

**nu, bekijk de gemiddelde zittingslengte van nieuwe bezoekers vergeleken met het terugkeren bezoekers:**

1. Maak een rapport.
1. Klik **UICONTROL toevoegen Metrisch**, muis over de [!DNL Google Analytics] sectie bij de bodem van dropdown en selecteren `Average Session Length`.
1. Wijzig de tijdsperiode in een bewegend bereik, van 13 maanden geleden tot 1 maand geleden, en wijzig het tijdinterval in `by month`?
1. Voeg een `Group by` toe en selecteer `New or returning visitor` .  Schakel het selectievakje `Show All` in en klik op **[!UICONTROL Apply]** .
1. Geef uw rapport een naam, zoals `Average session length`, en klik **[!UICONTROL Save]**.

**daarna, bekijk uw hoogste verwijzende domeinen in de laatste 30 dagen:**

1. Maak een rapport.
1. Klik op **[!UICONTROL Add Metric]** , houd de muis boven de [!DNL Google Analytics] -sectie onder aan het vervolgkeuzemenu en selecteer `Sessions` .
1. Verander uw tijdsperiode in een bewegend bereik, van 31 dagen geleden tot 1 dag geleden, en pas het tijdinterval aan `none` aan.
1. Voeg een `Group by` toe en selecteer `ga:source` .  Controleer _tonen Al_ doos; dan klik **[!UICONTROL Apply]**.
1. Voeg nog een `group by` toe en selecteer `ga:medium` . Schakel nogmaals het selectievakje `Show All` in en klik op **[!UICONTROL Apply]** .
1. Geef uw rapport een naam, zoals `Top 20 Referring Domains, 30 Days`, en klik **[!UICONTROL Save]**.

**tot slot, kijk omzetting:**

1. Maak een rapport.
1. Voeg de volgende metriek toe:

* `New users`
   * Klik op **[!UICONTROL Hide]** onder de metrische naam

* `Number of orders`
   * Voeg een filter voor `Customer's order number` = 1 toe en klik **[!UICONTROL Apply]**
   * Wijzig de naam van de metrische waarde door op de naam van de metrische waarde te klikken, deze aan te roepen `Number of first orders` en vervolgens op **[!UICONTROL Hide]** te klikken.

* `Number of orders`
   * **[!UICONTROL Hide]** de metrische waarde

* `Users`
   * **[!UICONTROL Hide]** de metrische waarde
   * Wijzig de tijdsperiode in `24 months ago to now` en pas het tijdinterval aan in `by month` .
   * Voeg de volgende formules toe door op **[!UICONTROL Formula]** te klikken.
   * A/D en vervolgens op **[!UICONTROL Apply]**
   * Naam van de formule wijzigen `Registration conversion`
   * B/D en vervolgens op **[!UICONTROL Apply]**
   * Naam van de formule wijzigen `First order conversion`
   * C/D en klik vervolgens op **[!UICONTROL Apply]**
   * Naam van de formule wijzigen `Any order conversion`

* Geef uw rapport nu een naam, zoals `Conversion by month`, en klik dan **[!UICONTROL Save]**.

## Volgende stappen

Nu u toegang tot gegevens over uw Webverkeer en omzettingspercentages hebt, kunt u beginnen om dit te ontginnen om bedrijfsbesluiten, zoals te drijven welke plaatsen het best in het besturen van verkeer aan uw plaats zijn? of Welke van uw campagnes zijn het meest effectief in het verwerven van klanten met de hoge levenwaarde?

Terwijl u de strategie voor advertentie-uitgaven en marketing aanpast, kunt u de resultaten in [!DNL Commerce Intelligence] blijven volgen en op dit dashboard blijven herhalen om aan de veranderende prioriteiten van uw bedrijf te voldoen.
