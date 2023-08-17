---
title: Teruggestuurde bestellingen analyseren
description: Leer hoe u een dashboard instelt met een gedetailleerde analyse van de geretourneerde bedragen van uw winkel.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Teruggestuurde bestellingen

Dit onderwerp toont aan hoe te opstelling een dashboard dat een gedetailleerde analyse van de terugkeer van uw opslag verstrekt.

![](../../assets/detailed-returns-dboard.png)

Voordat u aan de slag gaat, moet u [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) klant en zou ervoor moeten zorgen dat uw bedrijf gebruikt `enterprise\_rma` tabel voor geretourneerde waarden.

Deze analyse bevat [geavanceerd berekende kolommen](../data-warehouse-mgr/adv-calc-columns.md).

## Aan de slag

Te traceren kolommen

* **`enterprise_rma`** of **`rma`** table
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** of **`rma_item_entity`** table
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Filtersets die moeten worden gemaakt

* **`enterprise_rma`** table
* Naam filterset: `Returns we count`
* Filtersetlogica:
   * Tijdelijke aanduiding - voer hier uw aangepaste logica in

* **`enterprise_rma_item_entity`** table
* Naam filterset: `Returns items we count`
* Filtersetlogica:
   * Tijdelijke aanduiding - voer hier uw aangepaste logica in

### Berekende kolommen

Te maken kolommen

* **`enterprise_rma`** table
* **`Order's created at`**
* Selecteer een definitie: `Joined Column`
* [!UICONTROL Create Path]:
* 
  [!UICONTROL Many]: `enterprise_rma.order_id`
* 
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Selecteer een [!UICONTROL table]: `sales_flat_order`
* Selecteer een [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Selecteer een definitie: `Joined Column`
* Selecteer een [!UICONTROL table]: `sales_flat_order`
* Selecteer een [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** wordt gemaakt door een analist als onderdeel van uw `[RETURNS ANALYSIS]` kaartje

* **`enterprise_rma_item_entity`** table
* **`return_date_requested`**
* Selecteer een definitie: `Joined Column`
* [!UICONTROL Create Path]:
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Selecteer een [!UICONTROL table]: `enterprise_rma`
* Selecteer een [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** wordt gemaakt door een analist als onderdeel van uw `[RETURNS ANALYSIS]` kaartje

* **`sales_flat_order`** table
* **`Order contains a return? (1=yes/0=No)`**
* Selecteer een definitie: `Exists`
* Selecteer een [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** wordt gemaakt door een analist als onderdeel van uw `[RETURNS ANALYSIS]` kaartje
* **`Customer's previous order contains return? (1=yes/0=no)`** wordt gemaakt door een analist als onderdeel van uw `[RETURNS ANALYSIS]` kaartje

>[!NOTE]
>
>Als u alleen de kantooruren voor Seconden naar resolutie of Seconden naar eerste reactie wilt analyseren, geeft u dit door aan de analist wanneer u het ticket aanvraagt.

### Metrisch

* **Retourneert**
* In de **`enterprise_rma`** table
* Deze maatstaf voert een **Aantal**
* Op de **`entity_id`** kolom
* Besteld door de **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Teruggestuurde objecten**
* In de **`enterprise_rma_item_entity`** table
* Deze maatstaf voert een **Som**
* Op de **`qty_approved`** kolom
* Besteld door de **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Totale waarde van geretourneerd object**
* In de **`enterprise_rma_item_entity`** table
* Deze maatstaf voert een **Som**
* Op de **`Returned item total value (qty_returned * price)`** kolom
* Besteld door de **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Gemiddelde tijd tussen bestelling en terugkeer**
* In de **`enterprise_rma`** table
* Deze maatstaf voert een **Gemiddeld**
* Op de **`Time between order's created_at and date_requested`** kolom
* Besteld door de **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

### Rapporten

* **Herhaal de waarschijnlijkheid van de volgorde na het maken van een return**
* Metrisch `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Metrisch `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule: waarschijnlijkheid van herhalingsvolgorde
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
  [!UICONTROL Chart Type]: `Bar`

* **Gemiddelde tijd om terug te keren (alle tijd)**
* Metrisch `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Number`

* **Percentage van bestellingen met een rendement**
* Metrisch `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Metrisch `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule: % van bestellingen met rendement
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Inkomsten per maand**
* Metrisch `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 
  [!UICONTROL Chart Type]: `Line`

* **Klanten die een rendement hebben behaald en niet opnieuw zijn aangeschaft**
* Metrisch `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Group door]: `Customer_email`
* 
  [!UICONTROL Chart Type]: `Table`

* **Retourneringspercentage per object**
* Metrisch `A`: `Returned items` (Verbergen)
* [!UICONTROL Metric]: geretourneerde objecten

* Metrisch `B`: `Items sold` (Verbergen)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
  [!UICONTROL Chart Type]: `Table`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan er als het bovenstaande voorbeelddashboard uitzien.

Als u op om het even welke vragen terwijl het bouwen van deze analyse loopt of het Professionele team van de Diensten wilt in dienst nemen, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
