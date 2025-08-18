---
title: Teruggestuurde bestellingen analyseren
description: Leer hoe u een dashboard instelt met een gedetailleerde analyse van de geretourneerde bedragen van uw winkel.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Teruggestuurde bestellingen

Dit onderwerp toont aan hoe te opstelling een dashboard dat een gedetailleerde analyse van de terugkeer van uw opslag verstrekt.

![](../../assets/detailed-returns-dboard.png)

Alvorens begonnen te worden, moet u een [ Adobe Commerce ](https://business.adobe.com/products/magento/magento-commerce.html) klant zijn en zou moeten ervoor zorgen dat uw bedrijf de `enterprise\_rma` lijst voor terugkeer gebruikt.

Deze analyse bevat [ geavanceerde berekende kolommen ](../data-warehouse-mgr/adv-calc-columns.md).

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
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Selecteer een [!UICONTROL table]: `sales_flat_order`
* Selecteer een [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Selecteer een definitie: `Joined Column`
* Selecteer een [!UICONTROL table]: `sales_flat_order`
* Selecteer een [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** wordt door een analist gemaakt als onderdeel van uw `[RETURNS ANALYSIS]` -ticket

* **`enterprise_rma_item_entity`** table
* **`return_date_requested`**
* Selecteer een definitie: `Joined Column`
* [!UICONTROL Create Path]:
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Selecteer een [!UICONTROL table]: `enterprise_rma`
* Selecteer een [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** wordt door een analist gemaakt als onderdeel van uw `[RETURNS ANALYSIS]` -ticket

* **`sales_flat_order`** table
* **`Order contains a return? (1=yes/0=No)`**
* Selecteer een definitie: `Exists`
* Selecteer een [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** wordt door een analist gemaakt als onderdeel van uw `[RETURNS ANALYSIS]` -ticket
* **`Customer's previous order contains return? (1=yes/0=no)`** wordt door een analist gemaakt als onderdeel van uw `[RETURNS ANALYSIS]` -ticket

>[!NOTE]
>
>Als u alleen de kantooruren voor Seconden naar resolutie of Seconden naar eerste reactie wilt analyseren, geeft u dit door aan de analist wanneer u het ticket aanvraagt.

### Metrisch

* **Keert** terug
* In de tabel **`enterprise_rma`**
* Deze metrisch voert a **Telling** uit
* Op de kolom **`entity_id`**
* Besteld door de **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **teruggekeerde punten**
* In de tabel **`enterprise_rma_item_entity`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`qty_approved`**
* Besteld door de **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **teruggekeerde punt totale waarde**
* In de tabel **`enterprise_rma_item_entity`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`Returned item total value (qty_returned * price)`**
* Besteld door de **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Gemiddelde tijd tussen orde en terugkeer**
* In de tabel **`enterprise_rma`**
* Deze metrisch voert een **Gemiddelde** uit
* Op de kolom **`Time between order's created_at and date_requested`**
* Besteld door de **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Zorg ervoor om [ alle nieuwe kolommen als afmetingen aan metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

### Rapporten

* **Herhaal orde waarschijnlijkheid na het maken van een terugkeer**
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
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* &#x200B;
  [!UICONTROL Chart Type]: `Bar`

* **Gem tijd om terug te keren (allen tijd)**
* Metrisch `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Number`

* **Percentage van orden met een terugkeer**
* Metrisch `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Metrisch `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Formule: % van bestellingen met rendement
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Inkomsten die door maand** zijn teruggekeerd
* Metrisch `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **Klanten die een terugkeer hebben gemaakt en niet opnieuw aangekocht**
* Metrisch `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Group door]: `Customer_email`
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

* **tarief van de terugkeer door punt**
* Metrisch `A`: `Returned items` (Verbergen)
* [!UICONTROL Metric]: geretourneerde items

* Metrisch `B`: `Items sold` (Verbergen)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan er als het bovenstaande voorbeelddashboard uitzien.

Als u in om het even welke vragen loopt terwijl het bouwen van deze analyse of het Professionele team van de Diensten in dienst wilt nemen, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
