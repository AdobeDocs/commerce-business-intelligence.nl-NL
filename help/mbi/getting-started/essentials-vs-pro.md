---
title: MBI Essentials vs. Pro
description: Leer hoe de Hoofdzaak MBI van MBI Pro verschilt.
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
source-git-commit: dcd02693b3ca060ecdc47cbee189428ce157dd58
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 4%

---

# [!DNL MBI Essentials] vs [!DNL MBI Pro]

>[!NOTE]
>
>Dit is gearchiveerde documentatie voor [!DNL MBI].

In de volgende tabel wordt beschreven wat wordt opgenomen met Essentiële elementen en Pro.

|  | **`MBI Essentials`** | **`MBI Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | Tot 100 | Aangepast |
| `Pre-Defined Dashboards` | 5-6 | Aangepast |
| `New Custom Report Creation` | Ja | Ja |
| `Commerce Tables` | 4-6 | Onbeperkt |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | Ja | Ja |
| `Data Warehouse Manager` | Niet beschikbaar | Beschikbaar |
| `Email Reports` | Ja | Ja |
| `Cohort Report Builder` | Ja | Ja |
| `Google Analytics Live Integration` | Ja | Onbeperkt |
| `3rd Party Integrations` | Niet beschikbaar | Beschikbaar |
| `Full API Access` | Nee | Ja |
| `Access to CS, AM, or Analysts` | Nee | Ja |
| `Professional Services` | Beschikbaar | Beschikbaar |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Het aantal tabellen is afhankelijk van uitchecken door gasten.

**Opgenomen tabellen**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## Kolommen opgenomen in Essentiële elementen

Items in _cursief_ zijn berekende velden.

* `sales_order` table
   * `entity_id`
   * `base_grand_total`
   * `customer_id`
   * `status`
   * `customer_email`
   * `store_id`
   * `base_currency_code`
   * `billing_address_id`
   * `shipping_address_id`
   * `base_shipping_amount`
   * `base_tax_amount`
   * `coupon_code`
   * `created_at`
   * `updated_at`
   * `base_subtotal`
   * `customer_group_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `increment_id`
   * `Customer's order number`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Is customer's last order?`
   * `Billing address region`
   * `Shipping address country`
   * `Customer's lifetime revenue`
   * `Seconds between customer's first order date and this order`
   * `Seconds since previous order`
   * `Store name`
   * `Customer's lifetime number of coupons`
   * `Customer's order number (previous-current)`
   * `Shipping address region`
   * `Number of items in order`
   * `Billing address city`
   * `Shipping address city`
   * `Customer's group code`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's creation date`
   * `Billing address country`

* `sales_order_item` table
   * `item_id`
   * `qty_ordered`
   * `base_price`
   * `name`
   * `order_id`
   * `sku`
   * `product_type`
   * `product_id`
   * `created_at`
   * `updated_at`
   * `parent_item_id`
   * `store_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `Order's coupon_code`
   * `Order item total value (quantity * price)`
   * `Order's increment_id`
   * `Customer's email`
   * `Customer's lifetime number of orders`
   * `Store name`
   * `Customer's order number`
   * `Order's status`
   * `Customer's lifetime revenue`

* `sales_order_address` table
   * `entity_id`
   * `city`
   * `region`
   * `country_id`

* `customer_entity` table
   * `entity_id`
   * `email`
   * `group_id`
   * `created_at`
   * `updated_at`
   * `store_id`
   * `Customer's lifetime revenue`
   * `Customer's lifetime number of coupons`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Seconds since customer's first order date`
   * `Customer's first 30 day revenue`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's group code`
   * `Store name`

* `customer_group` table
   * `customer_group_id`
   * `customer_group_code`

* `store` table
   * `store_id`
   * `name`

