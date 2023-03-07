---
title: Visual Report Builder
description: Leer hoe te om Visual Report Builder te gebruiken.
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# `Visual Report Builder`

`Visual Report Builder` maakt het gemakkelijk om snelle rapporten tot stand te brengen die op vooraf bepaalde metriek worden gebaseerd. Elke metrisch omvat een vraag die de reeks gegevens voor het rapport bepaalt.

Het volgende voorbeeld toont hoe te om een eenvoudig rapport tot stand te brengen, groepeert de gegevens door een extra afmeting, plaatst het datum en tijdinterval, verandert het grafiektype, en bewaart het rapport aan een dashboard.

## Een eenvoudig rapport maken:

1. In de [!DNL MBI] menu, klikt u op **[!UICONTROL Report Builder]**.

1. Onder `Visual Report Builder`, klikt u op **[!UICONTROL Create Report]** en voer de volgende handelingen uit:

   * Klikken **[!UICONTROL Add Metric]**.

      De beschikbare metriek kan alfabetisch of door lijst worden vermeld.

      ![Visual Report Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * Kies de optie [metrisch](../../data-user/reports/ess-manage-data-metrics.md) dat beschrijft de reeks gegevens die u voor het rapport wilt gebruiken.

      De `New Customers` Metrisch die in dit voorbeeld wordt gebruikt telt alle klanten, en sorteert de lijst door de datum de klant die voor een rekening wordt aangemeld. Het eerste rapport bevat een eenvoudige lijngrafiek, gevolgd door de tabel met gegevens.

      Het overzicht op de linkerzijde toont de naam van huidige metrisch, die door het resultaat van om het even welke berekeningen op kolomgegevens wordt gevolgd die in metrisch worden gespecificeerd. In dit voorbeeld geeft het overzicht het totale aantal klanten weer.

      ![Visual Report Builder](../../assets/magento-bi-report-builder-untitled.png)

1. Houd de muisaanwijzer boven elk gegevenspunt op de regel in het diagram. Elk gegevenspunt toont het totale aantal nieuwe klanten die zich tijdens die maand hebben aangemeld.

1. Volg deze instructies om de gegevens te groeperen, de datumwaaier, en grafiektype te veranderen.

   **`Group By`**

   De `Group By` Met besturingselementen kunt u meerdere afmetingen per groep of segment toevoegen. Dimension zijn kolommen in de tabel die kunnen worden gebruikt om de gegevens te groeperen.

   * Kies een van de beschikbare afmetingen in de lijst met `Group By` opties.

      In dit voorbeeld heeft het systeem vijf couponcodes gevonden die door klanten werden gebruikt bij het plaatsen van hun eerste bestelling.

      ![Groeperen op](../../assets/magento-bi-report-builder-group-by-dimensions.png)

      De `Group By` Elke coupon die door klanten wordt gebruikt, wordt in detail weergegeven. De coupons die zijn gebruikt om de eerste bestelling te plaatsen, zijn gemarkeerd met een selectievakje. Het diagram bevat nu meerdere gekleurde lijnen die elke coupon vertegenwoordigen die voor een eerste bestelling is gebruikt. De legenda heeft een kleurcode die overeenkomt met elke gegevensrij.

   * Klikken **[!UICONTROL Apply]** om Group By detail te sluiten.

      ![Meerdere Dimension](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * Houd de muisaanwijzer boven een paar gegevenspunten op elke regel om het aantal klanten te zien dat de coupon tijdens het plaatsen van de eerste bestelling heeft gebruikt.

   * De tabel met gegevens heeft nu een extra dimensie, met een kolom voor elke maand en een rij voor elke couponcode.

      ![Groeperen op tabelgegevens](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * Klik op Omwisselen (![](../../assets/magento-bi-btn-transpose.png)) in de rechterbovenhoek van de tabel om de richting van de gegevens te wijzigen.

      De as van de gegevens wordt gespiegeld en de tabel heeft nu een kolom voor elke couponcode en een rij voor elke maand. Deze richting is misschien beter leesbaar.

      ![Omgezette gegevens](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)
   **`Date Range`**

   De `Date Range` De controle toont de huidige montages van het datumwaaier en tijdinterval, en wordt gevestigd net boven de grafiek aan het recht.

   * Klik op de knop `Date Range` besturingselement, dat in dit voorbeeld is ingesteld op `All-Time by Month`.

      ![Datumbereik](../../assets/magento-bi-report-builder-date-range.png)

   * Breng de volgende wijzigingen aan:

      * Als u wilt inzoomen voor een betere weergave, wijzigt u het datumbereik in `Last Full Quarter`.
      * Onder `Select Time Interval`kiest u `Week`.
      * Klik op **[!UICONTROL Save]**.

      Het verslag bevat nu alleen de gegevens voor het laatste kwartaal, per week.

      ![Rapport voor vorige kwartaal per week](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)
   **Type diagram**

   * Klik op de besturingselementen in de rechterbovenhoek om het beste diagram voor de gegevens te zoeken.

      Sommige diagramtypen zijn niet compatibel met multidimensionale gegevens.

      |  |  |
      |-----|-----|
      | ![](../../assets/magento-bi-btn-chart-line.png) | Lijngrafiek |
      | ![](../../assets/magento-bi-btn-chart-horz-bar.png) | Horizontale balk |
      | ![](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | Horizontale gestapelde balk |
      | ![](../../assets/magento-bi-btn-chart-vert-bar.png) | Verticale balk |
      | ![](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | Verticale gestapelde balk |
      | ![](../../assets/magento-bi-btn-chart-pie.png) | Schijf |
      | ![](../../assets/magento-bi-btn-chart-area.png) | Gebied |
      | ![](../../assets/magento-bi-btn-chart-funnel.png) | Trechter |

      {style="table-layout:auto"}




1. Om het verslag `title`, vervangt de `Untitled Report` tekst boven aan de pagina met een beschrijvende titel.

1. Klik in de rechterbovenhoek op **[!UICONTROL Save]** en voer de volgende handelingen uit:

   * Voor `Type`, accepteert u de standaardinstelling, `Chart`.

   * Kies de optie `Dashboard` waar het verslag beschikbaar moet zijn.

   * Klikken **[!UICONTROL Save to Dashboard]**.

      ![Opslaan naar dashboard](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. Voer een van de volgende handelingen uit om de grafiek in een dashboard weer te geven:

   * Klikken **[!UICONTROL Go to Dashboard]** in het bericht boven aan de pagina.

   * Kies in het menu de optie `Dashboards` en klik op de naam van het huidige dashboard om de lijst weer te geven. Klik vervolgens op de naam van het dashboard waar het rapport is opgeslagen.

      ![Rapport in dashboard](../../assets/magento-bi-report-builder-my-dashboard.png)
