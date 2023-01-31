---
title: Inventarisniveaus analyseren
description: Leer hoe u inventarisniveaus kunt analyseren.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Inventarisniveaus analyseren

In dit onderwerp ziet u hoe u een dashboard instelt dat inzichten verschaft in uw huidige inventaris. Dit onderwerp bevat instructies voor cliënten op zowel de erfenisarchitectuur als de nieuwe architectuur. U bevindt zich op de oude architectuur als u niet beschikt over de **[!UICONTROL Data Warehouse Views]** optie onder de **[!UICONTROL Manage Data]** ). Als u zich op de oudere architectuur bevindt, dient u een [nieuwe supportaanvraag](../../guide-overview.md) met het onderwerp **[!UICONTROL INVENTORY ANALYSIS]** zodra u de aangewezen sectie in _Berekende kolommen_ onderstaande instructies.

## Kolommen die moeten worden bijgehouden:

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

### Nieuwe architectuur

* **[!UICONTROL catalog_product_entity]** tabel:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * Selecteren [!UICONTROL DATETIME column]: `Product's most recent order date`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] inputs:
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * Definitie:
         * case when A is null or B is null then null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end





* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] inputs:
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * Definitie:
         * case als A null of B null is of B = 0,0 en null else round(A::decimal/B,2) end





### Verouderde architectuur

* **[!UICONTROL catalog_product_entity]** tabel:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * Selecteer de kolom DATETIME: **`Product's most recent order date`**
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Selecteer een [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * Wordt gemaakt door een analist wanneer u uw bestand verzendt **[INVENTARISCHE ANALYSE]** supportverzoek





* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Selecteer een [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * Wordt gemaakt door een analist wanneer u uw bestand verzendt **[!UICONTROL INVENTORY ANALYSIS]** supportverzoek





## Metrisch

### Metrische instructies

* **[!UICONTROL cataloginventory_stock_item]** tabel:
   * **`Inventory on hand`**: deze metrische waarde voert een
      * **Som** op de
      * **`qty`** kolom geordend door de
      * [Geen] kolom

## Rapporten

### Instructies rapporteren

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Tijdinterval: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 

      [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`
   * [!UICONTROL Time period]: `All time`
   * Tijdinterval: `None`
   * 
      [!UICONTROL Group door]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`
   * [!UICONTROL Time period]: `All time`
   * Tijdinterval: `None`
   * 
      [!UICONTROL Group door]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


Als u op vragen loopt terwijl u deze analyse bouwt, of eenvoudig ons professionele de dienstenteam wilt in dienst nemen, [contactondersteuning](../../guide-overview.md).
