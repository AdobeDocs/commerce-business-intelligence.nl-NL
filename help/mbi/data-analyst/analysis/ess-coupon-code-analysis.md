---
title: Coupon Code Analysis (basis)
description: Meer informatie over de couponprestaties van uw bedrijf is een interessante manier om uw bestellingen te segmenteren en de gewoonten van klanten beter te begrijpen.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Basissyntaxiscodeanalyse

Kennis van de couponprestaties van uw bedrijf is een interessante manier om uw bestellingen te segmenteren en de gewoonten van klanten beter te begrijpen.

Dit onderwerp documenteert de stappen die worden vereist om deze analyse tot stand te brengen om te begrijpen hoe de op coupon-verworven klanten presteren, trends, en het gebruik van individuele couponcode volgen.

![&#x200B; dashboard van de codeanalyse van de coupon die gebruik en prestatiesmetriek tonen &#x200B;](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Aan de slag

Eerst een opmerking over hoe couponcodes worden bijgehouden. Als een klant een coupon op een bestelling heeft toegepast, gebeuren er drie dingen:

* Een korting wordt weerspiegeld in de waarde `base_grand_total` (uw `Revenue` -metrische waarde in Commerce Intelligence)
* De couponcode wordt opgeslagen in het veld `coupon_code` . Als dit veld NULL (leeg) is, is er geen coupon aan de order gekoppeld.
* Het gedisconteerde bedrag wordt opgeslagen in `base_discount_amount` . Afhankelijk van uw configuratie kan deze waarde negatief of positief lijken.

Vanaf Commerce 2.4.7 kan een klant meer dan één couponcode op een bestelling toepassen. In dit geval:

* Alle toegepaste couponcodes worden opgeslagen in het veld `coupon_code` van `sales_order_coupons` . De eerste couponcode die wordt toegepast, wordt ook opgeslagen in het veld `coupon_code` van `sales_order` . Als dit veld NULL (leeg) is, is er geen coupon aan de order gekoppeld.

## Een metrisch object maken

De eerste stap bestaat uit het samenstellen van een nieuwe metrische code met de volgende stappen:

* Navigeer naar **[!UICONTROL Manage Data > Metrics > Create New Metric]** .

* Selecteer de `sales_order` .
* Dit metrisch voert a **Som** op de **base_disconto_amount** kolom uit, die door **wordt bevolen created_at**.
   * [!UICONTROL Filters]:
      * De `Orders we count` (Opgeslagen filterset) toevoegen
      * Voeg het volgende toe:
         * `coupon_code`**IS NIET**`[NULL]`
      * Geef de metrische waarde een naam, zoals `Coupon discount amount`.

## Het dashboard maken

* Zodra metrisch is gecreeerd:
   * Navigeer naar [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Geef het dashboard een naam, bijvoorbeeld `_Coupon Analysis_` .

* Hier maakt u alle rapporten en voegt u deze toe.

## Rapporten samenstellen

* **Nieuwe Rapporten:**

>[!NOTE]
>
>De [!UICONTROL Time Period]** voor elk rapport wordt weergegeven als `All-time` . U kunt dit aanpassen aan uw analysebehoeften. Adobe raadt alle rapporten op dit dashboard aan voor dezelfde periode, zoals `All time` , `Year-to-date` of `Last 365 days` .

* **Orders met coupons**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Orders zonder coupons**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Netto opbrengst van orden met coupons**
   * &#x200B;
     [!UICONTROL Metric]: `Revenue`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Kortingen van coupons**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Gemiddelde levensinkomsten: Coupon verworven klanten**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Filter toevoegen:
         * [`A`] `Customer's first order's coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Gemiddelde levensinkomsten: Niet-coupon verworven klanten**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Filter toevoegen:
         * [ A ] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **het gebruiksdetails van de coupon (eerste tijdorden)**
   * Metrisch `1`: `Orders`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET**`[NULL]`
         * [`B`] `Customer's order number` **Gelijk aan** `1`

   * Metrisch `2`: `Revenue`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET**`[NULL]`
         * [`B`] `Customer's order number` **Gelijk aan** `1`

      * Naam wijzigen: `Net revenue`

   * Metrisch `3`: `Coupon discount amount`
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS NIET**`[NULL]`
         * [`B`] `Customer's order number` **Gelijk aan** `1`

   * Formule maken: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * &#x200B;
        [!UICONTROL Format]: `Currency`

   * Create formule:**% disconted**
      * Formule: `(C / (B - C))`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * Formule maken: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **Gemiddelde levensinkomsten door eerste orde coupon**
   * [!UICONTROL Metric]:**Gem levensopbrengst**
      * Filter toevoegen:
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **het gebruiksdetails van de coupon (eerste tijdorden)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Filter toevoegen:
         * [`A`] `Customer's first order's coupon_code` **IS NIET** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * &#x200B;
     [!UICONTROL Chart type]: **Column**

* **Nieuwe klanten door coupon/niet-coupon verwerving**
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

>[!NOTE]
>
>Vanaf Adobe Commerce 2.4.7, kunnen de klanten **quote_coupons** en **sales_order_coupons** lijsten gebruiken om inzicht op te krijgen hoe de klant veelvoudige coupons gebruikt.

![&#x200B; de relatiediagram van de Lijst voor multi-coupon analyse &#x200B;](../../assets/multicoupon_relationship_tables.png)
