---
title: sales_order_item, tabel
description: Leer hoe u met de tabel sales_order_item werkt.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item` Tabel

De tabel `sales_order_item` (`sales_flat_order_item` op M1) bevat gegevens over alle producten die in een bestelling zijn aangeschaft. Elke rij vertegenwoordigt een unieke `sku` die in een volgorde is opgenomen. Het aantal eenheden dat voor een specifieke `sku` is aangeschaft, wordt meestal weergegeven in het veld `qty_ordered` .

## Producttypen

`sales_order_item` vangt details op alle [ producttypes ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=nl-NL#product-types) die werden gekocht. In [!DNL Adobe Commerce] wordt vaak gebruikgemaakt van configureerbare producten, met andere woorden een product dat kan worden aangepast op basis van grootte, kleur en andere productkenmerken. Hoewel een configureerbaar product zijn eigen `sku` heeft, kan het betrekking hebben op meerdere eenvoudige producten, waarbij elk eenvoudig product een unieke productconfiguratie vertegenwoordigt. Verwijs naar [ vormend producten ](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) voor meer informatie.

Neem bijvoorbeeld een configureerbaar product, zoals een t-shirt. Wanneer een klant uitcheckt, selecteert hij of zij opties om de kleur en de grootte te wijzigen. Als de klant een kleur van `blue` en een grootte van `small` selecteert, kopen ze uiteindelijk een eenvoudig product als `t-shirt-blue-small` dat teruggaat naar het bovenliggende product van `t-shirt` .

Wanneer een configureerbaar product in een orde inbegrepen is, worden twee rijen geproduceerd in de `sales_order_item` lijst: voor [ eenvoudig ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html?lang=nl-NL) `sku` en voor [ configureerbare ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html?lang=nl-NL) ouder. Deze twee verslagen in de `sales_order_item` lijst kunnen met elkaar door het volgende verbinden worden verwant:

* (simple) `sales_order_item.parent_item_id` => (configureerbaar) `sales_order_item.item_id`

Daarom is het mogelijk om op het eenvoudige niveau of op het configureerbare niveau verslag uit te brengen over de verkoop van producten. Door gebrek, worden alle standaard `order-item-level` metriek in [!DNL Commerce Intelligence] gevormd om de eenvoudige producten uit te sluiten, en *slechts* rapport over de configureerbare versies. Dit wordt bereikt via de filterset `Ordered products we count` , die filtert op de voorwaarde waarbij `parent_item_id` is `NULL` .

## Algemene kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|----|----|
| `base_price` | Prijs van een individuele eenheid van een product op het tijdstip van verkoop nadat [ de regels van de catalogusprijs, de gelaagde kortingen, en de speciale prijs ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=nl-NL) worden toegepast en alvorens om het even welke belastingen, de verscheping, of de wortelkortingen worden toegepast. Dit wordt weergegeven in de basisvaluta van de winkel. |
| `created_at` | Tijdstempel maken van het orderitem, lokaal opgeslagen in UTC. Afhankelijk van uw configuratie in [!DNL Commerce Intelligence], kan dit timestamp in een rapporteringstijdzone in [!DNL Commerce Intelligence] worden omgezet die van uw streek van de gegevensbestandtijd verschilt. |
| `item_id` (PK) | Unieke id voor de tabel. |
| `name` | Tekstnaam van het orderitem. |
| `order_id` | `Foreign key` die aan de tabel `sales_order` is gekoppeld. Verbind met `sales_order.entity_id` om ordekenmerken te bepalen verbonden aan het orde punt. |
| `parent_item_id` | `Foreign key` die een eenvoudig product koppelt aan zijn ouderbundel of configureerbaar product. Verbinden met `sales_order_item.item_id` om de kenmerken van het bovenliggende product te bepalen die aan het eenvoudige product zijn gekoppeld. Voor bovenliggende orderitems (dat wil zeggen bundel- of configureerbare producttypen) is de `parent_item_id` `NULL` . |
| `product_id` | `Foreign key` die aan de tabel `catalog_product_entity` is gekoppeld. Verbind met `catalog_product_entity.entity_id` om productkenmerken te bepalen verbonden aan het orde punt. |
| `product_type` | Soort product dat is verkocht. De potentiële [ producttypes ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=nl-NL#product-types) omvatten: eenvoudig, configureerbaar, gegroepeerd, virtueel, bundel, en downloadbaar. |
| `qty_ordered` | Hoeveelheid eenheden die op het moment van verkoop in het winkelwagentje voor het desbetreffende orderartikel zijn opgenomen. |
| `sku` | Unieke id voor het orderitem dat is aangeschaft. |
| `store_id` | `Foreign key` die aan de tabel `store` is gekoppeld. Verbind met `store.store_id` om te bepalen welke Commerce-winkelweergave aan het orderitem is gekoppeld. |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Customer's email` | E-mailadres van de klant die de bestelling plaatst. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `customer_email` te retourneren. |
| `Customer's lifetime number of orders` | Totaal aantal orders geplaatst door deze klant. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `Customer's lifetime number of orders` te retourneren. |
| `Customer's lifetime revenue` | Som totaal van opbrengsten voor alle orders geplaatst door deze klant. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `Customer's lifetime revenue` te retourneren. |
| `Customer's order number` | Volgorde voor de orde van deze klant. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `Customer's order number` te retourneren. |
| `Order item total value (quantity * price)` | De totale waarde van een orde punt op het tijdstip van verkoop na [ catalogusprijsregels, gelaagde kortingen, en speciale tarifering ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=nl-NL) wordt toegepast en alvorens om het even welke belastingen, verschepen, of kartkortingen worden toegepast. Berekend door de `qty_ordered` te vermenigvuldigen met de `base_price` . |
| `Order's coupon_code` | Coupon toegepast op de bestelling. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `coupon_code` te retourneren. |
| `Order's increment_id` | Unieke id van de bestelling. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `increment_id` te retourneren. |
| `Order's status` | Status van de bestelling. Wordt berekend door `sales_order_item.order_id` samen te voegen met `sales_order.entity_id` en het veld `status` te retourneren. |
| `Store name` | Naam van de Commerce-winkel die aan het orderitem is gekoppeld. Wordt berekend door `sales_order_item.store_id` samen te voegen met `store.store_id` en het veld `name` te retourneren. |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Products ordered` | De totale hoeveelheid producten die bij de verkoop in de winkelwagentjes was opgenomen | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Totale waarde van de producten die in de winkelwagentjes zijn opgenomen op het moment van de verkoop nadat de catalogusprijsregels, gedifferentieerde kortingen en speciale prijzen zijn toegepast en voordat eventuele belastingen, verzendingen of winkelkortingen worden toegepast | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Paden samenvoegen

`catalog_product_entity`

* Verbind met `catalog_product_entity` lijst om kolommen tot stand te brengen die productattributen verbonden aan het orde punt terugkeren.
   * Pad: `sales_order_item.product_id` (veel) => `catalog_product_entity.entity_id` (één)

`sales_order`

* Verbind met `sales_order` lijst om nieuwe orde-vlakke kolommen tot stand te brengen verbonden aan het orde punt.
   * Pad: `sales_order_item.order_id` (veel) => `sales_order.entity_id` (één)

`sales_order_item`

* Verbind met `sales_order_item` om kolommen tot stand te brengen die details van de ouder configureerbaar of bundel SKU met het eenvoudige product associëren. [ de steun van het Contact ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) voor hulp in het vormen van deze berekeningen, als het bouwen in de manager van Data Warehouse.
   * Pad: `sales_order_item.parent_item_id` (veel) => `sales_order_item.item_id` (één)

`store`

* Verbind met `store` lijst om kolommen tot stand te brengen die details met betrekking tot de opslag van Commerce verbonden aan het orde punt terugkeren.
   * Pad: `sales_order_item.store_id` (veel) => `store.store_id` (één)
