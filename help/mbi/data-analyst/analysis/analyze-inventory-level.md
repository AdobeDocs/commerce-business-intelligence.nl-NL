---
title: Inventarisniveaus analyseren
description: Leer hoe u inventarisniveaus kunt analyseren.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Inventarisniveaus analyseren

In dit onderwerp ziet u hoe u een dashboard instelt dat inzichten verschaft in uw huidige inventaris en instructies bevat voor klanten op zowel de oudere architectuur als de nieuwe architectuur. U bevindt zich op de oude architectuur als u niet over de optie **[!UICONTROL Data Warehouse Views]** in het menu **[!UICONTROL Manage Data]** beschikt. Als u op de erfenisarchitectuur bent, voorlegt a [ nieuw steunverzoek ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) met het onderwerp **[!UICONTROL INVENTORY ANALYSIS]** zodra u de aangewezen sectie in de _Berekende kolommen_ hieronder instructies bereikt.

## Te traceren kolommen:

### Kolommen voor het bijhouden van instructies

* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** tabel:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Berekende kolommen:

+++ Nieuwe architectuur

* **[!UICONTROL catalog_product_entity]** tabel:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [ A ] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [ A ] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `AGE`
      * Selecteren [!UICONTROL DATETIME column]: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [ A ] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] invoer:
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * &#x200B;

        [!UICONTROL Datatype]: `Decimal`
      * Definitie:
         * case when A is null or B is null then null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] invoer:
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * &#x200B;

        [!UICONTROL Datatype]: `Decimal`
      * Definitie:
         * case als A null of B null is of B = 0,0 en null else round(A::decimal/B,2) end

+++
+++ Verouderde architectuur

* **[!UICONTROL catalog_product_entity]** tabel:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [ A ] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [ A ] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;

        [!UICONTROL Column equation]: `AGE`
      * Selecteer DATETIME-kolom: **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;

        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Selecteer een [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [ A ] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Gemaakt door een analist wanneer u uw **[INVENTORY ANALYSE]** steunverzoek voorlegt

* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;

        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Gemaakt door een analist wanneer u een **[!UICONTROL INVENTORY ANALYSIS]** -supportverzoek indient

+++

## Metrisch

### Metrische instructies

* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`Inventory on hand`**: deze metrische waarde voert een
      * **Som** op
      * **`qty`** kolom geordend door de
      * [ niets ] kolom

## Rapporten

### Instructies rapporteren

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Tijdinterval: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * &#x200B;

     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [ A ] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * Tijdinterval: `None`
   * &#x200B;

     [!UICONTROL Group door]: `Sku`
   * &#x200B;

     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [ A ] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * Tijdinterval: `None`
   * &#x200B;

     [!UICONTROL Group door]: `Sku`
   * &#x200B;

     [!UICONTROL Chart type]: `Table`

Als u in om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten in dienst willen nemen, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL).
