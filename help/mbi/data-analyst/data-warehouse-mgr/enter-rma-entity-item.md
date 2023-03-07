---
title: Enterprise_RAM_Item_Entity table
description: Leer hoe u informatie over een specifiek item kunt analyseren op basis van een gevraagde return.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# enterprise_map_item_entiteitstabel

Elke rij in de `enterprise_rma_item_entity` table (vaak `magento_rma_item_entity` in Handel 2.x, maar de naam kan worden aangepast) bevat informatie over een specifiek punt van een gevraagde terugkeer.

>[!NOTE]
>
>Deze tabel wordt alleen standaard geleverd met uw Commerce-account als u een `Enterprise Edition` of `Enterprise Cloud Edition` klant.

## Algemene native kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `entity\_id` | Unieke id voor de tabel. Elk `entity\_id` vertegenwoordigt een item dat is aangevraagd voor retournering. |
| `rma\_entity\_id` | Buitenlandse sleutel gekoppeld aan de `enterprise\_rma` tabel. |
| `status` | De status van de geretourneerde waarde van het item. Waarden zijn onder andere &#39;receive&#39;, &#39;pending&#39;, &#39;authorised&#39;. De waarden in deze status komen mogelijk niet overeen met de waarde van de status van de algemene return. |
| `qty\_requested` | De hoeveelheid die de klant vraagt om terug te keren. |
| `qty\_approved` | De voor terugzending goedgekeurde hoeveelheid. |
| `qty\_returned` | De geretourneerde hoeveelheid. |
| `order\_item\_id` | Buitenlandse sleutel gekoppeld aan de `sales\_flat\_order\_item` tabel. |
| `product\_sku` | De sku die wordt geretourneerd. |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `Return date\_requested` | Dit is de datum die de klant om het terugkomen vroeg. |
| `Item price` | De prijs van het object. |
| `Return item's total value (qty\_returned * price)` | Dit is de totale monetaire waarde van de items die worden geretourneerd. Dit wordt gebruikt om het totale opbrengstbedrag op het `enterprise\_rma` tabel. |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische naam** | **Beschrijving** | **Constructie** |
|---|---|---|
| `Number of items returned` | Het aantal geretourneerde items. | Bewerkingskolom: hoeveelheid geretourneerd<br>Bewerking: som<br>Tijdstempelkolom: Datum van terugkeer aangevraagd |
| `Returned items' total value` | Het geldbedrag dat is geretourneerd. | Bewerkingskolom: Totale waarde van retourpost (geretourneerde hoeveelheid * prijs)<br>Bewerking: Som<br>Tijdstempelkolom: Datum van terugkeer aangevraagd |

{style="table-layout:auto"}

## Verbindingen met Andere Lijsten

`enterprise_rma`

* Samengevoegde kolommen maken, zoals `Return date\_requested` op de `enterprise_rma_item_entity` tabel via de volgende samenvoeging:
* Handel 1.x: `enterprise_rma_item_entity.rma_entity_id ` (veel) => `enterprise_rma.entity_id` (1)
* Handel 2.x: `magento_rma_item_entity.rma_entity_id ` (veel) => `magento_rma.entity_id` (1)

`sales_flat_order_item`

* Gemengde kolommen maken op het tabblad  `enterprise_rma_item_entity` tabel via de volgende samenvoeging:

* Handel 1.x: `enterprise_rma_item_entity.order_item_id ` (veel) => `sales_flat_order_item.item_id` (1)
* Handel 2.x: `magento_rma_item_entity.order_item_id ` (veel) => `sales_order_item.item_id` (1)
