---
title: Rapportage over een retailkalender
description: Leer hoe te opstelling de structuur om een 4-5-4 detailhandelkalender binnen uw  [!DNL Commerce Intelligence]  rekening te gebruiken.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Rapportage over een Retail-agenda

Dit onderwerp toont aan hoe te opstelling de structuur om a [ 4-5-4 kleinhandelskalender ](https://nrf.com/resources/4-5-4-calendar) binnen uw [!DNL Adobe Commerce Intelligence] rekening te gebruiken. De visuele rapportbouwer verstrekt ongelooflijk flexibele tijdwaaiers, intervallen, en onafhankelijke montages. Al deze instellingen werken echter met de traditionele maandkalender.

Omdat veel klanten hun kalender veranderen om winkels of boekhoudingsdata te gebruiken, illustreren de onderstaande stappen hoe te met uw gegevens te werken en rapporten tot stand te brengen gebruikend detailhandelsdata. Hoewel de onderstaande instructies verwijzen naar de kalender 4-5-4 Retail, kunt u deze wijzigen voor elke specifieke kalender die uw team gebruikt, of het nu om een financieel of gewoon een aangepast tijdkader gaat.

Alvorens begonnen te worden, zou u [ Uploader van het Dossier ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) moeten herzien en ervoor zorgen dat u het `.csv` dossier hebt verlengd. Op deze manier zorgt u ervoor dat alle historische gegevens in de datums worden opgenomen en dat de datums in de toekomst worden opgenomen.

Deze analyse bevat [ geavanceerde berekende kolommen ](../data-warehouse-mgr/adv-calc-columns.md).

## Aan de slag

U kunt [ downloaden ](../../assets/454-calendar.csv) a `.csv` versie van 4-5-4 detailhandelkalender voor kleinhandelsjaren 2014 door 2017. Mogelijk moet u dit bestand aanpassen op basis van uw interne agenda voor de detailhandel en het datumbereik uitbreiden ter ondersteuning van uw historisch en huidige tijdframe. Nadat u het bestand hebt gedownload, gebruikt u de File Uploader om een Retail Calendar-tabel in uw [!DNL Commerce Intelligence] -Data Warehouse te maken. Als u een ongewijzigde versie van 4-5-4 detailhandelkalender gebruikt, zorg ervoor dat de structuur en de gegevenstypes van de gebieden in deze lijst het volgende aanpassen:

| Kolomnaam | Datatype kolom | Primaire sleutel |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (maximaal 255 tekens) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Te maken kolommen

* **verkoop\_orde** lijst
   * `INPUT` `created\_at` (jjjj-mm-dd 00 :00: 00)
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Retail kalender** dossier uploadt lijst
   * **Huidige datum**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
        [!UICONTROL Datatype]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >De bovenstaande functie `now()` is specifiek voor PostSQL. Hoewel de meeste [!DNL Commerce Intelligence] data warehouses worden gehost op PostgreSQL, kunnen sommige worden gehost op Redshift. Als de bovenstaande berekening een fout retourneert, moet u mogelijk de functie Redshift `getdate()` gebruiken in plaats van `now()` .

   * **Huidige kleinhandelsjaar** (moet door steunanalist worden gecreeerd)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **inbegrepen in huidige detailhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **inbegrepen in vorige detailhandeljaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Datatype]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **verkoop\_orde** lijst
   * **Gemaakt \_at (kleinhandelsjaar)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Year Retail`
   * **Gemaakt \_at (kleinhandelsweek)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: verkoop\_order.\[INPUT \] creeerde \_at (jjjj-mm-dd 00 :00: 00
         * [!UICONTROL One]: Retail Calendar.Date Retail
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Week Retail`
   * **Gemaakt \_at (kleinhandelsmaand)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Month Number Retail`
   * **omvat in vorige kleinhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Retail `Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **omvat in huidige kleinhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Retail `Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Metrisch

Opmerking: er zijn geen nieuwe meetgegevens nodig voor deze analyse. Nochtans, zorg ervoor om [ de nieuwe kolommen toe te voegen u in de verkoop \_order lijst als afmetingen ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) voor alle metriek op de verkoop \_order lijst alvorens aan de rapporten verder te gaan.

## Rapporten

* **Wekelijkse orden - kleinhandelskalender (YoY)**
   * Metrisch `A`: `2017`
      * [!UICONTROL Metric]: aantal bestellingen
      * [!UICONTROL Filter]:
         * Gemaakt\_at (kleinhandelsjaar) = 2017
   * Metrisch `B`: `2016`
      * [!UICONTROL Metric]: aantal bestellingen
      * [!UICONTROL Filter]:
         * Gemaakt\_at (kleinhandelsjaar) = 2016
   * Metrisch `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
     [!UICONTROL Chart type]: `Line`
      * `multiple Y-axes` uitschakelen

* **het overzicht van de Kleinhandelkalender (huidig detailhandelsjaar door maand)**
   * Metrisch `A`: `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrisch `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrisch `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

* **het overzicht van de Kleinhandelkalender (vorig detailhandelsjaar door maand)**
   * Metrisch `A`: `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrisch `B`: `Orders`
      * [!UICONTROL Metric]: aantal bestellingen
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrisch `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

## Volgende stappen

In het bovenstaande ziet u hoe u een agenda voor handelsversies configureert die compatibel is met alle metrische elementen die op de tabel `sales\_order` zijn gebaseerd (zoals `Revenue` of `Orders` ). U kunt dit ook uitbreiden om de detailhandelkalender voor metriek te steunen die op om het even welke lijst wordt gebouwd. Het enige vereiste is dat deze lijst een geldig datetime gebied heeft dat kan worden gebruikt om tot de Retail lijst van de Kalender toe te treden.

Als u bijvoorbeeld de maatstaven op klantniveau wilt weergeven in een 4-5-4-handelsagenda, maakt u een `Same Table` -berekening in de `customer\_entity` -tabel, vergelijkbaar met `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` die hierboven wordt beschreven. Vervolgens kunt u deze kolom gebruiken om de berekeningen `One to Many` JOINED\_COLUMN (zoals `Created_at (retail year)` ) en `Include in previous retail year? (Yes/No)` te reproduceren door de tabel `customer\_entity` bij de tabel `Retail Calendar` te voegen.

Vergeet niet om alle nieuwe kolommen als afmetingen aan metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen. [
