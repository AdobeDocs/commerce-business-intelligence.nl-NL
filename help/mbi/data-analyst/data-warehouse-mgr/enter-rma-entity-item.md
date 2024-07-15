---
title: Enterprise_RAM_Item_Entity table
description: Leer hoe u informatie over een specifiek item kunt analyseren op basis van een gevraagde return.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_map_item_entiteitstabel

Elke rij in de tabel `enterprise_rma_item_entity` (wordt vaak `magento_rma_item_entity` in Commerce 2.x genoemd, maar de naam kan worden aangepast) bevat informatie over een specifiek item uit een gevraagde return.

>[!NOTE]
>
>Deze tabel wordt alleen standaard geleverd bij uw Commerce-account als u een `Enterprise Edition` - of `Enterprise Cloud Edition` -klant bent.

## Algemene native kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `entity\_id` | Unieke id voor de tabel. Elke `entity\_id` vertegenwoordigt een item dat is opgevraagd om terug te keren. |
| `rma\_entity\_id` | External key gekoppeld aan de tabel `enterprise\_rma` . |
| `status` | De status van de geretourneerde waarde van het item. Waarden zijn onder andere &#39;receive&#39;, &#39;pending&#39;, &#39;authorised&#39;. De waarden in deze status komen mogelijk niet overeen met de waarde van de status van de algemene return. |
| `qty\_requested` | De hoeveelheid die de klant vraagt om terug te keren. |
| `qty\_approved` | De voor terugzending goedgekeurde hoeveelheid. |
| `qty\_returned` | De geretourneerde hoeveelheid. |
| `order\_item\_id` | External key gekoppeld aan de tabel `sales\_flat\_order\_item` . |
| `product\_sku` | De sku die wordt geretourneerd. |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Return date\_requested` | Dit is de datum die de klant om het terugkomen vroeg. |
| `Item price` | De prijs van het object. |
| `Return item's total value (qty\_returned * price)` | Dit is de totale monetaire waarde van de geretourneerde items. Dit wordt gebruikt om het totale terugkeerbedrag op de `enterprise\_rma` lijst te berekenen. |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Number of items returned` | Het aantal geretourneerde items. | De Kolom van de verrichting: hoeveelheid teruggekeerde <br> Verrichting: Som <br> Tijdstempelkolom: Bezochte datum van de terugkeer |
| `Returned items' total value` | Het geldbedrag dat is geretourneerd. | De Kolom van de verrichting: De totale waarde van het punt van de terugkeer (teruggekeerde hoeveelheid * prijs) <br> Verrichting: Som <br> Tijdstempelkolom: Gevraagde datum van de terugkeer |

{style="table-layout:auto"}

## Verbindingen met Andere Lijsten

`enterprise_rma`

* Maak samengevoegde kolommen, zoals `Return date\_requested` in de `enterprise_rma_item_entity` -tabel via de volgende samenvoeging:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (many) => `enterprise_rma.entity_id` (one)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (veel) => `magento_rma.entity_id` (één)

`sales_flat_order_item`

* Gemengde kolommen maken op het tabblad  `enterprise_rma_item_entity` tabel via de volgende samenvoeging:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (many) => `sales_flat_order_item.item_id` (one)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (veel) => `sales_order_item.item_id` (één)
