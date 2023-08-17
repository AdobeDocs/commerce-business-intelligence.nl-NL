---
title: Rapportage over een retailkalender
description: Leer hoe u de structuur instelt voor het gebruik van een 4-5-4 handelskalender in uw [!DNL Commerce Intelligence] account.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Rapportage over een Retail-agenda

Dit onderwerp toont aan hoe te opstelling de structuur om te gebruiken [4-5-4 retailkalender](https://nrf.com/resources/4-5-4-calendar) binnen uw [!DNL Adobe Commerce Intelligence] account. De visuele rapportbouwer verstrekt ongelooflijk flexibele tijdwaaiers, intervallen, en onafhankelijke montages. Al deze instellingen werken echter met de traditionele maandkalender.

Omdat veel klanten hun kalender veranderen om winkels of boekhoudingsdata te gebruiken, illustreren de onderstaande stappen hoe te met uw gegevens te werken en rapporten tot stand te brengen gebruikend detailhandelsdata. Hoewel de onderstaande instructies verwijzen naar de kalender 4-5-4 Retail, kunt u deze wijzigen voor elke specifieke kalender die uw team gebruikt, of het nu om een financieel of gewoon een aangepast tijdkader gaat.

Voordat u aan de slag gaat, moet u controleren [De bestandsuploader](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) en zorg ervoor dat u de `.csv` bestand. Op deze manier zorgt u ervoor dat alle historische gegevens in de datums worden opgenomen en dat de datums in de toekomst worden opgenomen.

Deze analyse bevat [geavanceerd berekende kolommen](../data-warehouse-mgr/adv-calc-columns.md).

## Aan de slag

U kunt [downloaden](../../assets/454-calendar.csv) a `.csv` versie van de 4-5-4 retailkalender voor de detailhandelsjaren 2014 tot en met 2017. Mogelijk moet u dit bestand aanpassen op basis van uw interne agenda voor de detailhandel en het datumbereik uitbreiden ter ondersteuning van uw historisch en huidige tijdframe. Nadat u het bestand hebt gedownload, gebruikt u de File Uploader om een Retail Calendar-tabel te maken in uw [!DNL Commerce Intelligence] Data Warehouse. Als u een ongewijzigde versie van 4-5-4 detailhandelkalender gebruikt, zorg ervoor dat de structuur en de gegevenstypes van de gebieden in deze lijst het volgende aanpassen:

| Kolomnaam | Datatype kolom | Primaire sleutel |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Maximaal 255 tekens) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Te maken kolommen

* **sales\_order** table
   * `INPUT` `created\_at` (jjjj-mm-dd 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Detailagenda** bestands uploadtabel
   * **Huidige datum**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
        [!UICONTROL Datatype]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >De `now()` hierboven is specifiek voor PostSQL. Hoewel [!DNL Commerce Intelligence] de gegevenspakhuizen worden ontvangen op PostgreSQL, sommige kunnen op Redshift worden ontvangen. Als de bovenstaande berekening een fout retourneert, moet u mogelijk de functie Redshift gebruiken `getdate()` in plaats van `now()`.

   * **Huidig retailjaar** (Moet worden gemaakt door een ondersteuningsanalist)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Opgenomen in het lopende detailhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Opgenomen in het vorige detailhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Datatype]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** table
   * **Gemaakt\_at (kleinhandelsjaar)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Year Retail`
   * **Gemaakt\_at (handelsweek)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: verkoop\_order.\[INPUT\] gemaakt\_at (jjjj-mm-dd 00:00:00
         * [!UICONTROL One]: Retail Calendar.Date Retail
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Week Retail`
   * **Gemaakt\_at (handelsmaand)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Month Number Retail`
   * **Opnemen in het vorige detailhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Detailhandel `Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Opnemen in het huidige detailhandelsjaar? (Ja/Nee)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Pad -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Detailhandel `Calendar.Date Retail`
      * Selecteer een [!UICONTROL table]: `Retail Calendar`
      * Selecteer een [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Metrisch

Opmerking: er zijn geen nieuwe meetgegevens nodig voor deze analyse. Zorg er echter voor dat u [voeg de nieuwe kolommen toe u in de verkoop \_orde lijst als afmetingen bouwde](../data-warehouse-mgr/manage-data-dimensions-metrics.md) voor alle metriek op de verkoop \_ordetabel alvorens aan de rapporten verder te gaan.

## Rapporten

* **Wekelijkse bestellingen - retailkalender (YoY)**
   * Metrisch `A`: `2017`
      * [!UICONTROL Metric]: Aantal bestellingen
      * [!UICONTROL Filter]:
         * Gemaakt\_at (kleinhandelsjaar) = 2017
   * Metrisch `B`: `2016`
      * [!UICONTROL Metric]: Aantal bestellingen
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
      * Uitschakelen `multiple Y-axes`

* **Overzicht van de detailhandelkalender (huidig detailhandelsjaar per maand)**
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

* **Overzicht van de detailhandelkalender (vorige detailhandelsjaar per maand)**
   * Metrisch `A`: `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrisch `B`: `Orders`
      * [!UICONTROL Metric]: Aantal bestellingen
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

Hierboven wordt beschreven hoe u een detailhandelkalender configureert om compatibel te zijn met elke metrische code die op uw `sales\_order` tabel (zoals `Revenue` of `Orders`). U kunt dit ook uitbreiden om de detailhandelkalender voor metriek te steunen die op om het even welke lijst wordt gebouwd. Het enige vereiste is dat deze lijst een geldig datetime gebied heeft dat kan worden gebruikt om tot de Retail lijst van de Kalender toe te treden.

Als u bijvoorbeeld de maatstaven op klantniveau wilt weergeven in een 4-5-4-handelsagenda, maakt u een `Same Table` berekening in de `customer\_entity` tabel, vergelijkbaar met `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` hierboven beschreven. U kunt deze kolom dan gebruiken om het `One to Many` GEKOPPELDE\_KOLOMN berekeningen (zoals `Created_at (retail year)`) en `Include in previous retail year? (Yes/No)` door zich bij `customer\_entity` aan de `Retail Calendar` tabel.

Vergeet niet [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.
