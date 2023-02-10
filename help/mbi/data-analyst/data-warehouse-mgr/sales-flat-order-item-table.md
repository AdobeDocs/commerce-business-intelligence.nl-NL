---
title: sales_order_item, tabel
description: Leer hoe u met de tabel sales_order_item werkt.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# `sales_order_item` Tabel

De `sales_order_item` tabel (`sales_flat_order_item` op M1 1) een register bevat van alle producten die in een bestelling zijn aangeschaft. Elke rij vertegenwoordigt een unieke `sku` opgenomen in een bestelling. De hoeveelheid eenheden die voor een specifieke `sku` wordt het vaakst vertegenwoordigd door `qty_ordered` veld.

## Producttypen

De `sales_order_item` legt details vast op alle [productsoorten](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) die zijn gekocht. In de handel wordt vaak gebruikgemaakt van configureerbare producten, met andere woorden een product dat kan worden aangepast op basis van grootte, kleur en andere productkenmerken. Hoewel een configureerbaar product zijn eigen `sku`, kan het op veelvoudige eenvoudige producten betrekking hebben, waar elk eenvoudig product een unieke productconfiguratie vertegenwoordigt. Zie [configureren, producten](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) voor meer informatie .

Neem bijvoorbeeld een configureerbaar product, zoals een t-shirt. Wanneer een klant uitcheckt, selecteert hij of zij opties om de kleur en de grootte te wijzigen. Als de klant een kleur selecteert van `blue`en een grootte van `small`, kopen ze uiteindelijk een eenvoudig product zoals `t-shirt-blue-small` die betrekking heeft op het moederproduct van `t-shirt`.

Wanneer een configureerbaar product in een orde wordt omvat, worden twee rijen geproduceerd in `sales_order_item` tabel: een voor de [eenvoudig](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`en een voor de [configureerbaar](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) bovenliggend element. Deze twee records in de `sales_order_item` de lijst kan met elkaar door het volgende verbinden worden verwant:

* (eenvoudig) `sales_order_item.parent_item_id` => (configureerbaar) `sales_order_item.item_id`

Daarom is het mogelijk om op het eenvoudige niveau of op het configureerbare niveau verslag uit te brengen over de verkoop van producten. Standaard worden alle standaard `order-item-level` maatstaven in [!DNL MBI] zijn geconfigureerd om de eenvoudige producten uit te sluiten, en *alleen* rapport over de configureerbare versies. Dit wordt verwezenlijkt door `Ordered products we count` filterset, die op de voorwaarde filtert waar `parent_item_id` is `NULL`.

## Algemene kolommen

| **Kolomnaam** | **Beschrijving** |
|----|----|
| `base_price` | Prijs van een individuele eenheid van een product op het tijdstip van de verkoop na [catalogusprijsregels, gedifferentieerde kortingen en speciale prijzen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) worden toegepast en voordat belastingen, verzendkosten of winkelwagenkortingen worden toegepast, weergegeven in de basisvaluta van de winkel |
| `created_at` | Tijdstempel maken van het orderitem, meestal lokaal opgeslagen in UTC. Afhankelijk van uw configuratie in [!DNL MBI]kan deze tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL MBI] die van uw streek van de gegevensbestandtijd verschilt |
| `item_id` (PK) | Unieke id voor de tabel |
| `name` | Tekstnaam van het orderitem |
| `order_id` | `Foreign key` in verband met de `sales_order` tabel. Verbinden met `sales_order.entity_id` om ordekenmerken te bepalen verbonden aan het orde punt |
| `parent_item_id` | `Foreign key` die een eenvoudig product met zijn ouderbundel of configureerbaar product verbindt. Verbinden met `sales_order_item.item_id` om de kenmerken van het bovenliggende product te bepalen die aan het eenvoudige product zijn gekoppeld. Voor bovenliggende orderitems (d.w.z. bundel- of configureerbare producttypen) wordt de `parent_item_id` wordt `NULL` |
| `product_id` | `Foreign key` in verband met de `catalog_product_entity` tabel. Verbinden met `catalog_product_entity.entity_id` om productkenmerken te bepalen die aan het orderitem zijn gekoppeld |
| `product_type` | Soort product dat is verkocht. Potentieel [productsoorten](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) omvatten: eenvoudig, configureerbaar, gegroepeerd, virtueel, bundel en downloadbaar |
| `qty_ordered` | Hoeveelheid eenheden die op het moment van verkoop in het winkelwagentje voor het specifieke orderartikel is opgenomen |
| `sku` | Unieke id voor het aangeschafte orderitem |
| `store_id` | `Foreign key` in verband met de `store` tabel. Verbinden met `store.store_id` om te bepalen welke de opslagmening van de Handel verbonden aan het ordepunt |

{style=&quot;table-layout:auto&quot;}

## Gemeenschappelijke berekende kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `Customer's email` | E-mailadres van de klant die de bestelling plaatst. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `customer_email` field |
| `Customer's lifetime number of orders` | Totaal aantal orders geplaatst door deze klant. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `Customer's lifetime number of orders` field |
| `Customer's lifetime revenue` | Som totaal van opbrengsten voor alle orders geplaatst door deze klant. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `Customer's lifetime revenue` field |
| `Customer's order number` | Volgorde in volgorde voor bestelling van deze klant. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `Customer's order number` field |
| `Order item total value (quantity * price)` | Totale waarde van een orderitem op het moment van verkoop na [catalogusprijsregels, gedifferentieerde kortingen en speciale prijzen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) worden toegepast en voordat eventuele belastingen, verzendkosten of winkelkortingen worden toegepast. Berekend door vermenigvuldigen van `qty_ordered` door de `base_price` |
| `Order's coupon_code` | Coupon toegepast op de bestelling. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `coupon_code` field |
| `Order's increment_id` | Unieke id van de bestelling. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `increment_id` field |
| `Order's status` | Status van de bestelling. Berekend door verbinding `sales_order_item.order_id` tot `sales_order.entity_id` en de `status` field |
| `Store name` | Naam van de opslag van de Handel verbonden aan het ordepunt. Berekend door verbinding `sales_order_item.store_id` tot `store.store_id` en de `name` field |

{style=&quot;table-layout:auto&quot;}

## Algemene cijfers

| **Metrische naam** | **Beschrijving** | **Constructie** |
|---|---|---|
| `Products ordered` | De totale hoeveelheid producten die bij de verkoop in de winkelwagentjes was opgenomen | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Totale waarde van de producten die in de winkelwagentjes zijn opgenomen op het moment van de verkoop nadat de catalogusprijsregels, gedifferentieerde kortingen en speciale prijzen zijn toegepast en voordat eventuele belastingen, verzendingen of winkelkortingen worden toegepast | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` Paden samenvoegen

`catalog_product_entity`

* Verbinden met `catalog_product_entity` tabel voor het maken van nieuwe kolommen die productkenmerken retourneren die zijn gekoppeld aan het orderitem.
   * Pad: `sales_order_item.product_id` (veel) => `catalog_product_entity.entity_id` (1)

`sales_order`

* Verbinden met `sales_order` tabel voor het maken van nieuwe kolommen op ordeniveau die aan het orderitem zijn gekoppeld.
   * Pad: `sales_order_item.order_id` (veel) => `sales_order.entity_id` (1)

`sales_order_item`

* Verbinden met `sales_order_item` om nieuwe kolommen tot stand te brengen die details van de ouder configureerbaar of bundel SKU met het eenvoudige product associëren. Let op: u moet [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) voor hulp bij het vormen van deze berekeningen, als het gebouw in de manager van de Data Warehouse.
   * Pad: `sales_order_item.parent_item_id` (veel) => `sales_order_item.item_id` (1)

`store`

* Verbinden met `store` tabel voor het maken van nieuwe kolommen die details retourneren met betrekking tot de winkel Commerce die is gekoppeld aan het orderitem.
   * Pad: `sales_order_item.store_id` (veel) => `store.store_id` (1)
