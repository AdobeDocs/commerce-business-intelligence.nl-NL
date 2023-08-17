---
title: Formules in de Report Builder
description: Leer hoe formules in de Report Builder kunnen worden gebruikt.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Formules in de `Report Builder`

In de [`Report Builder`](../../tutorials/using-visual-report-builder.md)kunt u krachtige visualisaties maken met de [gedefinieerde meetwaarden](../../data-user/reports/ess-manage-data-metrics.md) in uw account. Door deze meetgegevens in een formule te combineren, kunt u extra inzichten van uw gegevens genereren. Dit onderwerp duikt in hoe formules in kunnen worden gebruikt in `Report Builder` - laten we erin springen!

## Wat is een `formula`? {#what}

In de `Report Builder`, `formula` is slechts een combinatie van één of meerdere metriek die op één of andere wiskundige logica wordt gebaseerd. Een typisch voorbeeld ziet er als volgt uit:

![](../../assets/formula-example.png)

In dit voorbeeld gebruikt u een `Number of orders metric (A)` en `Distinct buyers metric (B)`en het doel is de vraag te beantwoorden: wat is het gemiddelde aantal bestellingen dat mijn kopers elke maand maken? De parameters van de formule zijn:

* `Definition`: Hier past u berekeningen toe op de invoermeetgegevens. In dit voorbeeld geeft het delen van het aantal orders door het aantal afzonderlijke kopers het gemiddelde aantal orders aan. Daarom is de definitie (A/B).

* `Format`: Geeft uw formule een getal, een tijdsperiode of een valutabedrag? Naast de definitie van de formule is een vervolgkeuzelijst, die u kunt gebruiken om de indeling van de geretourneerde waarde op te geven. In dit geval is het een getal.

* `Miscellaneous`: De tijdstempel, groeperingen, perspectieven en filters van de formule worden allemaal overgeërfd door de invoermeetgegevens. Er is hier niets te doen!

## Hoe kan ik gebruiken? `formulas` in mijn verslagen? {#how}

Nu u de grondbeginselen hebt behandeld, bekijk een paar voorbeelden.

### Voorbeeld: Ik wil weten welk percentage van mijn inkomsten kan worden toegeschreven aan eerste bestellingen.

![Het gebruiken van formules om het percentage van opbrengst te vinden die aan eerste-tijdorden wordt toegeschreven](../../assets/first_time_orders.gif)

In dit voorbeeld hebt u de opdracht `Revenue` en `Revenue (first time orders)` metriek. Door de `Revenue (first time orders)(B)` metrisch met de `Revenue metric (A)` en het plaatsen van het terugkeerformaat aan `Percent`, kunt u het percentage van opbrengst vinden dat aan eerste orde kan worden toegeschreven.

### Voorbeeld: ik wil weten wat de gemiddelde inkomsten per bestelling zijn wanneer ik doe en geen aanbod doe `promo code`.

![Het gebruiken van formules om de gemiddelde opbrengst per orde met en zonder bevorderingscodes te vinden](../../assets/promo_code.gif)

In dit voorbeeld hebt u de opdracht `Revenue` en `Number of orders` metriek. Het antwoord op deze vraag bestaat uit twee stappen - verdeeld `Revenue (A)` door de `Number of orders (B)` en het plaatsen van het terugkeerformaat aan `Currency`. Vervolgens hebt u alleen het resultaat van de formule toegestaan (`Avg. Revenue per order`) om de resultaten weer te geven en te groeperen met `Promo code`.

### Voorbeeld: Ik wil de distributie van de UTM-bronnen van mijn nieuwe klanten kennen.

![Formules gebruiken om de distributie van UTM-bronnen van nieuwe klanten te vinden](../../assets/distro.gif)

Het vinden van het antwoord op deze vraag omvat een paar stappen:

1. Eerst hebt u de `New Customers` metrisch, en dan gegroepeerd door `utm_source - all`. Dit is metrisch `A`, of `New Customers (grouped)`.

1. Vervolgens hebt u het `New Customers (grouped)` en instellen op een onafhankelijke dimensie. Metrisch `B` - `New customers (ungrouped)` - het totale aantal nieuwe klanten.

1. Nadat u beide metriek hebt verborgen, stelt u de formule in op `A/B`. Hiermee verdeelt u de `New customers (grouped)` door de `New Customers (ungrouped)`.

1. Vervolgens stelt u de indeling van de resultaten in op `Percent`.

In dit voorbeeld hebt u de opdracht `Stacked Columns` perspectief om de resultaten per maand weer te geven. Op die manier kunnen we de verdeling van nieuwe klanten per maand vergelijken.

## Omloop {#wrapup}

Merkte u in de bovenstaande voorbeelden op dat de formule `timestamp`, `groupings`, `perspectives`, en `filters` worden overgeërfd van zijn inputmetriek? Houd er rekening mee dat formules kunnen worden gebruikt `perspectives` en [onafhankelijke tijdopties](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, net als metriek kan.

Als u nog vragen hebt over het gebruik van formules in het dialoogvenster `Report Builder`, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
