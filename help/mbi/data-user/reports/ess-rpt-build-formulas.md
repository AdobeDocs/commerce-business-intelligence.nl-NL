---
title: Formulas
description: Leer hoe u formules kunt gebruiken.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Formulas

Een formule combineert meerdere meetgegevens en wiskundige logica om een vraag te beantwoorden. Bijvoorbeeld, hoeveel van de opbrengst per product tijdens het vakantieseizoen door nieuwe klanten werd geproduceerd?

![Verkoop vakantie in dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Stap 1: Het basisrapport maken

1. Kies in het menu de optie `Report Builder`.

1. Klikken **[!UICONTROL Add Metric]** en kies eerste metrisch voor het rapport.

   In dit voorbeeld wordt `Revenue by products ordered` wordt metrisch gebruikt.

1. Klikken **[!UICONTROL Add Metric]** opnieuw en kies tweede metrisch voor het rapport.

   In dit voorbeeld wordt `New Customers` wordt metrisch gebruikt.

1. Klik in de zijbalk op **[!UICONTROL Details]** om informatie over elke metrische waarde weer te geven.

   ![Ontvangsten per bestelde producten](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. Klik in het zijpaneel op de naam van elke metrische waarde om de instellingenpagina in een nieuw browsertabblad te openen. Schuif omlaag om elke component van metrisch, met inbegrip van de metrische vraag, de filter, en de afmetingen te zien.

   ![Metrische instellingen](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Klik op het vorige browsertabblad om terug te keren naar uw rapport.

1. Houd de muisaanwijzer in de grafiek boven een paar gegevenspunten op elke regel om de aan elke meting gekoppelde hoeveelheden weer te geven.

## Stap 2: Een formule toevoegen

1. Klik boven aan het zijpaneel op **[!UICONTROL Add Formula]**.

   In het vak Formules worden de meetgegevens weergegeven als beschikbare invoer `A` en `B`en bevat een invoervak waarin u de formule kunt invoeren.

   Ga als volgt te werk:

   * In de `Enter your Formul` invoervak, typ `A/B`.

      Dit zal de opbrengst door producten verdelen die door het aantal nieuwe klanten worden bevolen.

   * Set `Select format` tot `123Number`.

   * In de zijbalk vervangt u `Untitled` met een naam voor de formule.

   ![Formule-instellingen](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. Klik op **[!UICONTROL Apply]**.

   Het verslag heeft nu een nieuwe lijn voor de formule, `New Customer Revenue`en de zijbalk geeft het totale bedrag aan inkomsten weer dat nieuwe klanten genereren.

   ![Rapport met formule](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Stap 3: Datumbereik toevoegen

1. Klikken **[!UICONTROL Date Range]** in de rechterbovenhoek.

1. Op de `Fixed Date Range` doet u het volgende:

   * Kies in de kalenders het datumbereik.

      In dit voorbeeld loopt het vakantieseizoen van 1 november tot en met 31 december.

   * Onder `Select Time Interval`kiest u `Day`.

      ![Vast datumbereik](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * Klik op **[!UICONTROL Apply]**.

   Het verslag is nu beperkt tot het vakantieseizoen, met een datapunt voor elke dag.

   ![Vast datumbereik](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Stap 4: Het rapport opslaan

In deze stap, zult u het rapport als grafiek en ook als lijst bewaren.

1. Klikken `Untitled Report` boven aan de pagina en voer een beschrijvende titel in. Voor dit voorbeeld is de rapporttitel: `2017 Holiday Sales`.

   Voer vervolgens de volgende handelingen uit:

   * Klik in de rechterbovenhoek op **[!UICONTROL Save]**.

   * Voor `Type`, accepteert u de standaardinstelling `Chart` instellen.

   * Kies de optie `Dashboard` waar het verslag beschikbaar moet zijn.

   * Klikken **[!UICONTROL Save to Dashboard]**.

1. Klik op de rapporttitel en wijzig de naam. Voor dit voorbeeld wordt de rapporttitel gewijzigd in `2017 Holiday Sales Data`.

   Voer vervolgens de volgende handelingen uit:

   * Klik in de rechterbovenhoek op **[!UICONTROL Save a Copy]**.

   * Set `Type` tot `Table`.

   * Kies de optie `Dashboard` waar het verslag beschikbaar moet zijn.

   * Klikken **[!UICONTROL Save a Copy to Dashboard]**.

1. Voer een van de volgende handelingen uit om de rapporten in het dashboard weer te geven:

   * Klikken **[!UICONTROL Go to Dashboard]** in het bericht boven aan de pagina.

   * Kies in het menu de optie **[!UICONTROL Dashboards]**. Klik op de naam van het huidige dashboard om de lijst weer te geven. Klik vervolgens op de naam van het dashboard waar het rapport is opgeslagen.
