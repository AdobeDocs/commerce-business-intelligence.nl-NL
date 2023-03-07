---
title: quote_item, tabel
description: Leer hoe u met de tabel quote_item werkt.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# quote_item, tabel

De `quote_item` tabel (`sales_flat_quote_item` op M1) 1) bevat gegevens over elk artikel dat aan een winkelwagentje is toegevoegd, ongeacht of het winkelwagentje is verlaten of in een aankoop is omgezet. Elke rij staat voor één winkelwagentje. Vanwege de mogelijke grootte van deze tabel, raadt Adobe u aan om regelmatig records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes ouder zijn dan 60 dagen.

>[!NOTE]
>
>Het analyseren van historische, verlaten wortels is slechts mogelijk als u verslagen van niet schrapt `quote` en `quote_item` tabel. Als u wel records verwijdert, kunt u alleen de winkelwagentjes zien die nog niet uit de database zijn verwijderd.

## Algemene native kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `base_price` | Prijs van een afzonderlijke eenheid van een product op het moment dat het item aan een winkelwagentje werd toegevoegd, na [catalogusprijsregels, gedifferentieerde kortingen en speciale prijzen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) worden toegepast en voordat eventuele belastingen, verzendkosten of winkelkortingen worden toegepast. Dit wordt weergegeven in de basisvaluta van de winkel. |
| `created_at` | Tijdstempel maken van het winkelwagentje dat lokaal in UTC is opgeslagen. Afhankelijk van uw configuratie in [!DNL MBI]kan deze tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL MBI] die van uw streek van de gegevensbestandtijd verschilt |
| `item_id` (PK) | Unieke id voor de tabel |
| `name` | Tekstnaam van het orderitem |
| `parent_item_id` | `Foreign key` die een eenvoudig product met zijn ouderbundel of configureerbaar product verbindt. Verbinden met `quote_item.item_id` om de kenmerken van het bovenliggende product te bepalen die aan het eenvoudige product zijn gekoppeld. Voor bovenliggende winkelwagentjes (d.w.z. bundel- of configureerbare producttypen): `parent_item_id` is `NULL` |
| `product_id` | `Foreign key` in verband met de `catalog_product_entity` tabel. Verbinden met `catalog_product_entity.entity_id` om productkenmerken te bepalen die aan het orderitem zijn gekoppeld |
| `product_type` | Type product dat aan het karretje is toegevoegd. Potentieel [productsoorten](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) omvatten: eenvoudig, configureerbaar, gegroepeerd, virtueel, bundel en downloadbaar |
| `qty` | Hoeveelheid eenheden in het winkelwagentje voor het desbetreffende winkelwagentje |
| `quote_id` | `Foreign key` in verband met de `quote` tabel. Verbinden met `quote.entity_id` om de kenmerken van het winkelwagentje te bepalen |
| `sku` | Unieke identificatiecode voor het winkelwagentje |
| `store_id` | Buitenlandse sleutel gekoppeld aan de `store` tabel. Verbinden met `store.store_id` om te bepalen welke mening van de Winkel van de Handel met het kartelpunt wordt geassocieerd |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `Cart creation date` | Tijdstempel die is gekoppeld aan de aanmaakdatum van het winkelwagentje. Berekend door verbinding `quote_item.quote_id` tot `quote.entity_id` en de `created_at` tijdstempel |
| `Cart is active? (1/0)` | Een Booleaans veld dat &quot;1&quot; retourneert als het winkelwagentje door een klant is gemaakt en nog niet is omgezet in een bestelling. Retourneert &quot;0&quot; voor omgezette winkelwagentjes of winkelwagentjes die via de beheerder zijn gemaakt. Berekend door verbinding `quote_item.quote_id` tot `quote.entity_id` en de `is_active` field |
| `Cart item total value (qty * base_price)` | Totale waarde van een artikel op het moment dat het item aan een winkelwagentje werd toegevoegd, na [catalogusprijsregels, gedifferentieerde kortingen en speciale prijzen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) worden toegepast en voordat eventuele belastingen, verzendkosten of winkelkortingen worden toegepast. Berekend door vermenigvuldigen van `qty` door de `base_price` |
| `Seconds since cart creation` | Verlopen tijd tussen de aanmaakdatum van de wagen en nu. Berekend door verbinding `quote_item.quote_id` tot `quote.entity_id` en de `Seconds since cart creation` field |
| `Store name` | Naam van de opslag van de Handel verbonden aan het ordepunt. Berekend door verbinding `sales_order_item.store_id` tot `store.store_id` en de `name` field |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische naam** | **Beschrijving** | **Constructie** |
|---|---|---|
| `Number of abandoned cart items` | Totale hoeveelheid aan winkelwagentjes toegevoegde artikelen die voldoen aan specifieke voorwaarden voor &quot;verlaten&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, waarbij &quot;x&quot; overeenkomt met de verstreken tijd (in seconden) sinds het maken van een winkelwagentje waarna een winkelwagentje als verlaten wordt beschouwd |
| `Abandoned cart item value` | Som van de totale inkomsten uit winkelwagentjes die voldoen aan specifieke voorwaarden voor &quot;verlaten&quot; winkels | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, waarbij &quot;x&quot; overeenkomt met de verstreken tijd (in seconden) sinds het maken van een winkelwagentje waarna een winkelwagentje als verlaten wordt beschouwd |

{style="table-layout:auto"}

## Vreemde sleutelpaden verbinden

`catalog_product_entity`

* Verbinden met `catalog_product_entity` tabel om kolommen te maken die productkenmerken retourneren die zijn gekoppeld aan het winkelwagentje.
   * Pad: `quote_item.product_id` (veel) => `catalog_product_entity.entity_id` (1)

`quote`

* Verbinden met `quote` tabel voor het maken van nieuwe kolommen op cartniveau die aan het winkelwagentje zijn gekoppeld.
   * Pad: `quote_item.quote_id` (veel) => `quote.entity_id` (1)

`quote_item`

* Verbinden met `quote_item` om kolommen tot stand te brengen die details van de ouder configureerbaar of bundel SKU met het eenvoudige product associëren. [Contact opnemen met ondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) voor hulp bij het vormen van deze berekeningen, als het gebouw in de manager van de Data Warehouse.
   * Pad: `quote_item.parent_item_id` (veel) => `quote_item.item_id` (1)

`store`

* Verbinden met `store` tabel voor het maken van kolommen die details retourneren die betrekking hebben op de winkel Commerce die is gekoppeld aan het winkelwagentje.
   * Pad: `quote_item.store_id` (veel) => `store.store_id` (1)
