---
title: Formules in de Report Builder
description: Leer hoe formules in de Report Builder kunnen worden gebruikt.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Formules in de `Report Builder`

In de [`Report Builder`](../../tutorials/using-visual-report-builder.md)kunt u krachtige visualisaties maken met de [gedefinieerde meetwaarden](../../data-user/reports/ess-manage-data-metrics.md) in uw account. Door deze meetgegevens in een formule te combineren, kunt u extra inzichten van uw gegevens genereren. In dit artikel duiken we diep in hoe formules kunnen worden gebruikt in de `Report Builder` - laten we erin springen!

## Wat is een `formula`? {#what}

In de `Report Builder`, `formula` is slechts een combinatie van één of meerdere metriek die op één of andere wiskundige logica wordt gebaseerd. Een typisch voorbeeld ziet er als volgt uit:

![](../../assets/formula-example.png)

In dit voorbeeld gebruiken we een `Number of orders metric (A)` en `Distinct buyers metric (B)`en ons doel is de vraag te beantwoorden: wat is het gemiddelde aantal bestellingen dat mijn kopers maandelijks maken ? De parameters van de formule zijn:

* `Definition`: Hier past u wiskunde op de inputmetriek toe. In dit voorbeeld wordt het gemiddelde aantal bestellingen weergegeven door het aantal afzonderlijke kopers te delen. Daarom is de definitie (A/B).

* `Format`: Retourneert uw formule een getal, een tijdsperiode of een valutabedrag? Naast de definitie van de formule is een vervolgkeuzelijst, die u kunt gebruiken om de indeling van de geretourneerde waarde op te geven. In dit geval is het een getal.

* `Miscellaneous`: De tijdstempel, groeperingen, perspectieven en filters van de formule worden allemaal overgeërfd door de invoermeetgegevens. Er is hier niets te doen!

## Hoe kan ik gebruiken? `formulas` in mijn verslagen? {#how}

Nu we de basisbeginselen hebben besproken, laten we een aantal voorbeelden bekijken.

### Voorbeeld: Ik wil weten welk percentage van mijn inkomsten kan worden toegeschreven aan eerste bestellingen.

![Het gebruiken van formules om het percentage van opbrengst te vinden die aan eerste-tijdorden wordt toegeschreven](../../assets/first_time_orders.gif)

In dit voorbeeld hebben we de `Revenue` en `Revenue (first time orders)` metriek. Door de `Revenue (first time orders)(B)` metrisch met de `Revenue metric (A)` en het plaatsen van het terugkeerformaat aan `Percent`We kunnen het percentage van de inkomsten vinden dat aan eerste bestellingen kan worden toegeschreven.

### Voorbeeld: Ik wil weten wat de gemiddelde inkomsten per bestelling zijn wanneer ik doe en geen `promo code`.

![Het gebruiken van formules om de gemiddelde opbrengst per orde met en zonder bevorderingscodes te vinden](../../assets/promo_code.gif)

In dit voorbeeld hebben we de `Revenue` en `Number of orders` metriek. Het antwoord op deze vraag bestaat uit twee stappen: opdelen `Revenue (A)` door de `Number of orders (B)` en het plaatsen van het terugkeerformaat aan `Currency`. Vervolgens hebben we alleen het resultaat van de formule toegestaan (`Avg. Revenue per order`) om de resultaten weer te geven en te groeperen met `Promo code`.

### Voorbeeld: Ik wil de distributie van de UTM-bronnen van mijn nieuwe klanten kennen.

![Formules gebruiken om de distributie van UTM-bronnen van nieuwe klanten te vinden](../../assets/distro.gif)

Het vinden van het antwoord op deze vraag omvat een paar stappen:

1. Eerst hebben we de `New Customers` metrisch, en dan gegroepeerd door `utm_source - all`. Dit is metrisch `A`, of `New Customers (grouped)`.

1. Vervolgens dupliceren we de `New Customers (grouped)` en instellen dat een onafhankelijke dimensie wordt gebruikt. Metrisch `B` - `New customers (ungrouped)` - het totale aantal nieuwe klanten.

1. Na het verbergen van beide metriek, plaatsen wij de formules definitie aan `A/B`. Hiermee verdeelt u de `New customers (grouped)` door de `New Customers (ungrouped)`.

1. Vervolgens wordt de resultatenindeling ingesteld op `Percent`.

In ons voorbeeld hebben we de `Stacked Columns` perspectief om de resultaten per maand weer te geven. Op die manier kunnen we de verdeling van nieuwe klanten per maand vergelijken.

## Omloop {#wrapup}

Merkte u in de bovenstaande voorbeelden op dat de formule `timestamp`, `groupings`, `perspectives`, en `filters` worden overgeërfd van zijn inputmetriek? Houd er rekening mee dat formules kunnen worden gebruikt `perspectives` en [onafhankelijke tijdopties](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, net als metriek.

Als u nog vragen hebt over het gebruik van formules in het dialoogvenster `Report Builder`, [contactondersteuning](../../guide-overview.md).
