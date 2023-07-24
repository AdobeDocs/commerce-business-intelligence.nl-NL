---
title: Coupon Code Analysis (basis)
description: Meer informatie over de couponprestaties van uw bedrijf is een interessante manier om uw bestellingen te segmenteren en de gewoonten van klanten beter te begrijpen.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Basissyntaxiscodeanalyse

Kennis van de couponprestaties van uw bedrijf is een interessante manier om uw bestellingen te segmenteren en de gewoonten van klanten beter te begrijpen.

Dit onderwerp documenteert de stappen die worden vereist om deze analyse tot stand te brengen om te begrijpen hoe de op coupon-verworven klanten presteren, trends, en het gebruik van individuele couponcode volgen.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Aan de slag

Eerst een opmerking over hoe couponcodes worden bijgehouden. Als een klant een coupon op een bestelling heeft toegepast, gebeuren er drie dingen:

* Een korting wordt weerspiegeld in de `base_grand_total` hoeveelheid (uw `Revenue` metrisch in de inlichtingen van de Handel)
* De couponcode wordt opgeslagen in het dialoogvenster `coupon_code` veld. Als dit veld NULL (leeg) is, is er geen coupon aan de order gekoppeld.
* Het gedisconteerde bedrag wordt opgeslagen in `base_discount_amount`. Afhankelijk van uw configuratie kan deze waarde negatief of positief lijken.

## Een metrisch object maken

De eerste stap bestaat uit het samenstellen van een nieuwe metrische code met de volgende stappen:

* Navigeren naar **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Selecteer `sales_order`.
* Deze maatstaf voert een **Som** op de **base_korting_amount** kolom, geordend door **created_at**.
   * [!UICONTROL Filters]:
      * Voeg de `Orders we count` (Opgeslagen filterset)
      * Voeg het volgende toe:
         * `coupon_code`**IS NIET**`[NULL]`
      * Geef metrisch een naam, zoals `Coupon discount amount`.

## Het dashboard maken

* Zodra metrisch is gecreeerd:
   * Navigeren naar [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Geef het dashboard een naam, zoals `_Coupon Analysis_`.

* Hier maakt u alle rapporten en voegt u deze toe.

## Rapporten samenstellen

* **Nieuwe rapporten:**

>[!NOTE]
>
>De [!UICONTROL Time Period]** voor elk rapport wordt vermeld als `All-time`. U kunt dit aanpassen aan uw analysebehoeften. Adobe raadt alle rapporten op dit dashboard aan dezelfde periode te bestrijken, zoals `All time`, `Year-to-date`, of `Last 365 days`.

* **Orders met coupons**
   * 
     [!UICONTROL Metric]: `Orders`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Orders zonder coupons**
   * 
     [!UICONTROL Metric]: `Orders`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Netto-inkomsten uit orders met coupons**
   * 
     [!UICONTROL Metric]: `Revenue`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Kortingen op coupons**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Gemiddelde inkomsten tijdens de levensduur: Door coupon aangekochte klanten**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Filter toevoegen:
         * [`A`] `Customer's first order's coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Gemiddelde inkomsten tijdens de levensduur: Klanten zonder coupon**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Filter toevoegen:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Gebruiksgegevens van coupon (eerste bestellingen)**
   * Metrisch `1`: `Orders`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET**`[NULL]`
         * [`B`] `Customer's order number` **Gelijk aan** `1`

   * Metrisch `2`: `Revenue`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET**`[NULL]`
         * [`B`] `Customer's order number` **Gelijk aan** `1`

      * Naam wijzigen:  `Net revenue`

   * Metrisch `3`: `Coupon discount amount`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET**`[NULL]`
         * [`B`] `Customer's order number` **Gelijk aan** `1`

   * Formule maken: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
        [!UICONTROL Format]: `Currency`

   * Formule maken:**% verdisconteerd**
      * Formule: `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * Formule maken: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Chart type]: `Table`

* **Gemiddelde levensopbrengsten per coupon voor eerste bestelling**
   * [!UICONTROL Metric]:**Gem. inkomsten**
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Gebruiksgegevens van coupon (eerste bestellingen)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Filter toevoegen:
         * [`A`] `Customer's first order's coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 
     [!UICONTROL Chart type]: **Column**

* **Nieuwe klanten door middel van couponaankopen/aankopen zonder coupon**
   * Metrisch `1`: `New customers`
      * Filter toevoegen:
         * [`A`] `Customer's first order's coupon_code` **IS NIET** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * Metrisch `2`: `New customers`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

Na het bouwen van de rapporten, verwijs naar het beeld bij de bovenkant van dit onderwerp voor hoe u de rapporten op uw dashboard kunt organiseren.
