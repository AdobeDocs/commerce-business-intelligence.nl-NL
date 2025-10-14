---
title: quote_item, tabel
description: Leer hoe u met de tabel quote_item werkt.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# quote_item, tabel

De tabel `quote_item` (`sales_flat_quote_item` op M1) bevat gegevens over elk artikel dat aan een winkelwagentje is toegevoegd, of de winkelwagentje is verlaten of is omgezet in een aankoop. Elke rij staat voor één winkelwagentje. Vanwege de mogelijke grootte van deze tabel raadt Adobe u aan om regelmatig records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes ouder zijn dan 60 dagen.

>[!NOTE]
>
>Het analyseren van historische, verlaten wortels is slechts mogelijk als u geen verslagen van de `quote` en `quote_item` lijst schrapt. Als u wel records verwijdert, kunt u alleen de winkelwagentjes zien die nog niet uit de database zijn verwijderd.

## Algemene native kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `base_price` | Prijs van een individuele eenheid van een product op het tijdstip dat het punt aan een karretje werd toegevoegd, nadat [&#x200B; de regels van de catalogusprijs, de gelaagde kortingen, en de speciale prijs &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=nl-NL) worden toegepast en alvorens om het even welke belastingen, de verscheping, of de wortelkortingen worden toegepast. Dit wordt weergegeven in de basisvaluta van de winkel. |
| `created_at` | Tijdstempel maken van het winkelwagentje dat lokaal in UTC is opgeslagen. Afhankelijk van uw configuratie in [!DNL Commerce Intelligence] kan dit tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL Commerce Intelligence] die afwijkt van de tijdzone van uw database |
| `item_id` (PK) | Unieke id voor de tabel |
| `name` | Tekstnaam van het orderitem |
| `parent_item_id` | `Foreign key` die een eenvoudig product koppelt aan zijn ouderbundel of configureerbaar product. Verbinden met `quote_item.item_id` om de kenmerken van het bovenliggende product te bepalen die aan het eenvoudige product zijn gekoppeld. Voor bovenliggende winkelwagentjes (dat wil zeggen bundel- of configureerbare producttypen) is de `parent_item_id` `NULL` |
| `product_id` | `Foreign key` die aan de tabel `catalog_product_entity` is gekoppeld. Verbinden met `catalog_product_entity.entity_id` om productkenmerken te bepalen die aan het orderitem zijn gekoppeld |
| `product_type` | Type product dat aan het karretje is toegevoegd. De potentiële [&#x200B; producttypes &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=nl-NL#product-types) omvatten: eenvoudig, configureerbaar, gegroepeerd, virtueel, bundel, en downloadbaar |
| `qty` | Hoeveelheid eenheden in het winkelwagentje voor het desbetreffende winkelwagentje |
| `quote_id` | `Foreign key` die aan de tabel `quote` is gekoppeld. Verbinden met `quote.entity_id` om de kenmerken van het winkelwagentje te bepalen die aan het winkelwagentje zijn gekoppeld |
| `sku` | Unieke identificatiecode voor het winkelwagentje |
| `store_id` | External key gekoppeld aan de tabel `store` . Verbinden met `store.store_id` om te bepalen welke Commerce-winkelweergave is gekoppeld aan het winkelwagentje |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Cart creation date` | Tijdstempel die is gekoppeld aan de aanmaakdatum van de wagen. Berekend door `quote_item.quote_id` samen te voegen met `quote.entity_id` en de `created_at` tijdstempel te retourneren |
| `Cart is active? (1/0)` | Een Booleaans veld dat &quot;1&quot; retourneert als het winkelwagentje door een klant is gemaakt en nog niet is omgezet in een bestelling. Retourneert &quot;0&quot; voor omgezette winkelwagentjes of winkelwagentjes die via de beheerder zijn gemaakt. Berekend door `quote_item.quote_id` met `quote.entity_id` te verbinden en het veld `is_active` te retourneren |
| `Cart item total value (qty * base_price)` | De totale waarde van een punt op het tijdstip dat het punt aan een karretje werd toegevoegd, nadat [&#x200B; de regels van de catalogusprijs, de gelaagde kortingen, en de speciale prijs &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=nl-NL) worden toegepast en alvorens om het even welke belastingen, de verscheping, of de wortelkortingen worden toegepast. Berekend door de `qty` te vermenigvuldigen met de `base_price` |
| `Seconds since cart creation` | Verlopen tijd tussen de aanmaakdatum van de wagen en nu. Berekend door `quote_item.quote_id` met `quote.entity_id` te verbinden en het veld `Seconds since cart creation` te retourneren |
| `Store name` | Naam van de Commerce-winkel die aan het orderitem is gekoppeld. Berekend door `sales_order_item.store_id` met `store.store_id` te verbinden en het veld `name` te retourneren |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Number of abandoned cart items` | Totale hoeveelheid aan winkelwagentjes toegevoegde artikelen die voldoen aan specifieke voorwaarden voor &quot;verlaten&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br> Filters:<br><br> - \ [`A` \] `Cart is active? (1/0)` = 1 <br> - \ [`B` \] `Seconds since cart creation` > x, waar &quot;x&quot;aan de verstreken tijd (in seconden) sinds de verwezenlijking van het karretje waarvoorbij een karretje als verlaten wordt beschouwd |
| `Abandoned cart item value` | Som van de totale inkomsten uit winkelwagentjes die voldoen aan specifieke voorwaarden voor &quot;verlaten&quot; winkels | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br> Filters:<br><br> - \ [`A` \] `Cart is active? (1/0)` = 1 <br> - \ [`B` \] `Seconds since cart creation` > x, waar &quot;x&quot;aan de verstreken tijd (in seconden) sinds de verwezenlijking van het karretje waarvoorbij een karretje als verlaten wordt beschouwd |

{style="table-layout:auto"}

## Vreemde sleutel die Wegen verbindt

`catalog_product_entity`

* Verbind met `catalog_product_entity` lijst om kolommen tot stand te brengen die productattributen verbonden aan het kartelpunt terugkeren.
   * Pad: `quote_item.product_id` (veel) => `catalog_product_entity.entity_id` (één)

`quote`

* Sluit u aan bij de tabel `quote` om nieuwe kolommen op tekenniveau te maken die aan het winkelwagentje zijn gekoppeld.
   * Pad: `quote_item.quote_id` (veel) => `quote.entity_id` (één)

`quote_item`

* Verbind met `quote_item` om kolommen tot stand te brengen die details van de ouder configureerbaar of bundel SKU met het eenvoudige product associëren. [&#x200B; de steun van het Contact &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) voor hulp in het vormen van deze berekeningen, als het bouwen in de manager van Data Warehouse.
   * Pad: `quote_item.parent_item_id` (veel) => `quote_item.item_id` (één)

`store`

* Verbind met `store` lijst om kolommen tot stand te brengen die details met betrekking tot de opslag van Commerce verbonden aan het wortelpunt terugkeren.
   * Pad: `quote_item.store_id` (veel) => `store.store_id` (één)
