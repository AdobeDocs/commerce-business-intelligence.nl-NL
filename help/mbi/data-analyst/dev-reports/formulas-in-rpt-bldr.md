---
title: Formules in de Report Builder
description: Leer hoe formules kunnen worden gebruikt in de Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Formulieren in de `Report Builder`

In [`Report Builder`](../../tutorials/using-visual-report-builder.md), kunt u krachtige visualisaties tot stand brengen gebruikend de [ bepaalde metriek ](../../data-user/reports/ess-manage-data-metrics.md) in uw rekening. Door deze meetgegevens in een formule te combineren, kunt u extra inzichten van uw gegevens genereren. Dit onderwerp duikt in hoe formules in `Report Builder` kunnen worden gebruikt - laat springen binnen!

## Wat is een `formula` ? {#what}

In de `Report Builder` is een `formula` alleen een combinatie van een of meer meetgegevens op basis van een wiskundige logica. Een typisch voorbeeld ziet er als volgt uit:

![](../../assets/formula-example.png)

In dit voorbeeld gebruikt u een `Number of orders metric (A)` en een `Distinct buyers metric (B)` . Het doel is om de vraag te beantwoorden: wat is het gemiddelde aantal bestellingen dat mijn kopers elke maand maken? De parameters van de formule zijn:

* `Definition`: hier past u wiskunde op de inputmetriek toe. In dit voorbeeld geeft het delen van het aantal orders door het aantal afzonderlijke kopers het gemiddelde aantal orders aan. Daarom is de definitie (A/B).

* `Format`: Geeft uw formule een getal, een tijdsperiode of een valutabedrag? Naast de definitie van de formule is een vervolgkeuzelijst, die u kunt gebruiken om de indeling van de geretourneerde waarde op te geven. In dit geval is het een getal.

* `Miscellaneous`: De tijdstempel, groeperingen, perspectieven en filters van de formule worden allemaal overgeërfd door de invoermeetgegevens. Er is hier niets te doen!

## Hoe kan ik `formulas` gebruiken in mijn rapporten? {#how}

Nu u de grondbeginselen hebt behandeld, bekijk een paar voorbeelden.

### Voorbeeld: Ik wil weten welk percentage van mijn inkomsten kan worden toegeschreven aan eerste bestellingen.

![ Gebruikend formules om het percentage van opbrengst te vinden die aan eerste-tijdorden wordt toegewezen ](../../assets/first_time_orders.gif)

In dit voorbeeld hebt u de metriek `Revenue` en `Revenue (first time orders)` gebruikt. Door `Revenue (first time orders)(B)` metrisch door `Revenue metric (A)` te delen en het terugkeerformaat aan `Percent` te plaatsen, kunt u het percentage van opbrengst vinden dat aan eerste orde kan worden toegeschreven.

### Voorbeeld: ik wil weten wat de gemiddelde opbrengst per orde is wanneer ik doe en geen `promo code` aanbiedt.

![ Gebruikend formules om de gemiddelde opbrengst per orde met en zonder promotiecodes te vinden ](../../assets/promo_code.gif)

In dit voorbeeld hebt u de metriek `Revenue` en `Number of orders` gebruikt. Het antwoord op deze vraag bestaat uit twee stappen: `Revenue (A)` wordt gedeeld door `Number of orders (B)` en de retournotatie wordt ingesteld op `Currency` . Vervolgens hebt u alleen het resultaat van de formule (`Avg. Revenue per order`) toegestaan om de resultaten weer te geven en te groeperen met `Promo code` .

### Voorbeeld: Ik wil de distributie van de UTM-bronnen van mijn nieuwe klanten kennen.

![ Gebruikend formules om de distributie van de bronnen van UTM van nieuwe klanten te vinden ](../../assets/distro.gif)

Het vinden van het antwoord op deze vraag omvat een paar stappen:

1. Eerst hebt u de metrische waarde `New Customers` toegevoegd en vervolgens gegroepeerd op `utm_source - all` . Dit is metrisch `A` of `New Customers (grouped)` .

1. Vervolgens hebt u de `New Customers (grouped)` -metrische waarde gedupliceerd en ingesteld op het gebruik van een onafhankelijke dimensie. Metrisch `B` - `New customers (ungrouped)` - geeft het totale aantal nieuwe klanten weer.

1. Nadat u beide meetgegevens hebt verborgen, stelt u de definitie van de formule in op `A/B` . Hiermee verdeelt u de `New customers (grouped)` door de `New Customers (ungrouped)` .

1. Vervolgens stelt u de indeling van de resultaten in op `Percent` .

In dit voorbeeld hebt u het perspectief `Stacked Columns` gebruikt om de resultaten per maand weer te geven. Op die manier kunnen we de verdeling van nieuwe klanten per maand vergelijken.

## Omloop {#wrapup}

Hebt u in de bovenstaande voorbeelden gemerkt dat de formules `timestamp` , `groupings` , `perspectives` en `filters` worden overgeërfd van de invoermeetgegevens? Houd in mening dat de formules kunnen worden gebruikt om `perspectives` en [ onafhankelijke tijdopties ](../../tutorials/time-options-visual-rpt-bldr.md){: target="_blank"} te gebruiken, enkel als metriek kan.

Als u om het even welke extra vragen over het gebruiken van formules in `Report Builder` hebt, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
