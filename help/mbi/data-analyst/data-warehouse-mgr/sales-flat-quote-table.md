---
title: Offertetabel
description: Leer hoe u met de prijsopgave werkt.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Offertetabel

De tabel `quote` (`sales_flat_quote` op M1) bevat gegevens over elk winkelwagentje dat in uw winkel is gemaakt, ongeacht of deze zijn verlaten of zijn omgezet in een aankoop. Elke rij vertegenwoordigt één kar. Vanwege de mogelijke grootte van deze tabel raadt Adobe u aan om regelmatig records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes ouder zijn dan 60 dagen.

>[!NOTE]
>
>Het analyseren van historische, verlaten wortels is slechts mogelijk als u geen verslagen van de `quote` lijst schrapt. Als u wel records verwijdert, kunt u alleen de winkelwagentjes zien die nog niet uit de database zijn verwijderd.

## Algemene native kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `base_currency_code` | Valuta voor alle waarden die zijn vastgelegd in `base_*` -velden (dat wil zeggen `base_grand_total` , `base_subtotal` , enzovoort). Dit is doorgaans de standaardvaluta van de Commerce Store. |
| `base_grand_total` | De uiteindelijke prijs die aan de klant voor het winkelwagentje wordt aangeboden, nadat alle belastingen, verzendkosten en kortingen zijn toegepast. Hoewel de exacte berekening aanpasbaar is, wordt de waarde van `base_grand_total` doorgaans berekend als `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Bruto-handelswaarde van alle in het winkelwagentje opgenomen artikelen. Belastingen, verzendkosten, kortingen enzovoort zijn niet inbegrepen |
| `created_at` | Tijdstempel maken van het winkelwagentje dat lokaal in UTC is opgeslagen. Afhankelijk van uw configuratie in [!DNL Commerce Intelligence] kan dit tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL Commerce Intelligence] die afwijkt van de tijdzone van uw database |
| `customer_email` | E-mailadres van de klant die de winkelwagen heeft gemaakt |
| `customer_id` | `Foreign key` die aan de tabel `customer_entity` is gekoppeld, als de klant is geregistreerd. Sluit u aan bij `customer_entity.entity_id` om de klantkenmerken te bepalen die zijn gekoppeld aan de gebruiker die de winkelwagen heeft gemaakt. Als de winkelwagen is gemaakt via uitchecken door gasten, is dit veld `NULL` |
| `entity_id` (PK) | Unieke id voor de tabel en wordt doorgaans gebruikt in verbindingen met andere tabellen binnen de Commerce-instantie |
| `is_active` | Een Booleaans veld dat &quot;1&quot; retourneert als het winkelwagentje door een klant is gemaakt en nog niet is omgezet in een bestelling. Hiermee wordt &quot;0&quot; geretourneerd voor omgezette winkelwagentjes of winkelwagentjes die via de beheerder zijn gemaakt |
| `items_qty` | Som van de totale hoeveelheid van alle in het winkelwagentje opgenomen artikelen |
| `reserved_order_id` | `Foreign key` die aan de tabel `sales_order` is gekoppeld. Verbind met `sales_order.increment_id` om orderdetails te bepalen verbonden aan een omgezette kar. Voor winkelwagentjes die niet aan een geconverteerde volgorde zijn gekoppeld, blijft de waarde `reserved_order_id` behouden `NULL` |
| `store_id` | `Foreign key` die aan de tabel `store` is gekoppeld. Verbinden met `store` .`store_id` om te bepalen welke Commerce-winkelweergave is gekoppeld aan de winkelwagentje |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Order date` | Tijdstempel die de aanmaakdatum van de volgorde van omgezette winkelwagentjes aangeeft. Berekend door `quote.reserved_order_id` met `sales_order.increment_id` te verbinden en het veld `sales_order.created_at` te retourneren |
| `Seconds between cart creation and order` | Verlopen tijd tussen het maken van winkelwagentjes en het maken van bestellingen. Berekend door `created_at` af te trekken van `Order date` , geretourneerd als een geheel getal van seconden |
| `Seconds since cart creation` | Verlopen tijd tussen de aanmaakdatum van de wagen en nu. Berekend door `created_at` af te trekken van de tijdstempel van de server op het moment dat de query wordt uitgevoerd, geretourneerd als een geheel getal van seconden. Meestal gebruikt om de leeftijd van een winkelwagen te bepalen |
| `Store name` | De naam van de Commerce-winkel die aan deze bestelling is gekoppeld. Berekend door `quote.store_id` met `store.store_id` te verbinden en het veld `name` te retourneren |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Number of abandoned carts` | Aantal kartels die voldoen aan specifieke &quot;voorwaarden voor stopzetting&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/> Filters:<br><br> - \ [`A` \] `is_active` = 1 <br> - \ [`B` \] `items_count` > 0 <br> - \ [`C` \] `Seconds since cart creation` > x, waar &quot;x&quot;aan de verstreken tijd (in seconden) sinds de verwezenlijking van het karretje beantwoordt waarwaarvoorbij een karretje als verlaten wordt beschouwd |
| `Avg time to cart conversion` | De gemiddelde tijd tussen het creëren van karretjes en ordeverwezenlijking voor omgezette karretjes | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | De som van de totale potentiële inkomsten uit verlaten winkelwagentjes, waarbij inkomsten worden gedefinieerd als het veld `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br> Filters:<br><br> - \ [A\] `is_active` = 1 <br> - \ [`B` \] `items_count` > 0 <br> - \ [`C` \] `Seconds since cart creation` > x, waar &quot;x&quot;aan de verstreken tijd (in seconden) sinds de verwezenlijking van de kar beantwoordt waarwaarvoorbij een kar als verlaten wordt beschouwd |

{style="table-layout:auto"}

## Vreemde sleutel die Wegen verbindt

`customer_entity`

* Sluit u aan bij de tabel `customer_entity` om nieuwe kolommen op klantniveau te maken die zijn gekoppeld aan de klant die het winkelwagentje heeft gemaakt.
   * Pad: `quote.customer_id` (veel) => `customer_entity.entity_id` (één)

`sales_order`

* Verbind met `sales_order` lijst om kolommen tot stand te brengen die ordedetails verbonden aan een omgezette kar terugkeren.
   * Pad:`quote.reserved_order_id` (veel) => `sales_order.increment_id` (één)

`store`

* Verbind met `store` lijst om kolommen tot stand te brengen die details met betrekking tot de opslag van Commerce verbonden aan het karretje terugkeren.
   * Pad: `quote.store_id` (veel) => `store.store_id` (één)
