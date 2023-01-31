---
title: prijsopgave
description: Leer hoe u met de prijsopgave werkt.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# prijsopgave

De `quote` tabel (`sales_flat_quote` op M1) bevat gegevens over elk winkelwagentje dat in uw winkel is gemaakt, ongeacht of de winkelwagentje is verlaten of is omgezet in een aankoop. Elke rij vertegenwoordigt één kar. Gezien de potentiële grootte van deze lijst, adviseren wij u periodiek verslagen te schrappen als bepaalde criteria worden voldaan, zoals als er om het even welke unconvert wortels ouder dan 60 dagen zijn.

>[!NOTE]
>
>Het analyseren van historische verlaten kaarten is alleen mogelijk als u geen records verwijdert uit de `quote` tabel. Als u records verwijdert, kunt u alleen de winkelwagentjes zien die nog niet uit de database zijn verwijderd.

## Algemene native kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `base_currency_code` | Valuta voor alle waarden die zijn vastgelegd in `base_*` velden (dat wil zeggen `base_grand_total`, `base_subtotal`, enzovoort). Dit weerspiegelt doorgaans de standaardvaluta van de Commerce Store |
| `base_grand_total` | De uiteindelijke prijs die aan de klant voor het winkelwagentje wordt aangeboden, nadat alle belastingen, verzendkosten en kortingen zijn toegepast. Hoewel de precieze berekening aanpasbaar is, wordt in het algemeen `base_grand_total` wordt berekend als `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Bruto-handelswaarde van alle in het winkelwagentje opgenomen artikelen. Belastingen, verzendkosten, kortingen enzovoort zijn niet inbegrepen |
| `created_at` | Tijdstempel van het ontwerp van het winkelwagentje, meestal lokaal opgeslagen in UTC. Afhankelijk van uw configuratie in [!DNL MBI]kan deze tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL MBI] die van uw streek van de gegevensbestandtijd verschilt |
| `customer_email` | E-mailadres van de klant die het winkelwagentje heeft gemaakt |
| `customer_id` | `Foreign key` in verband met de `customer_entity` tabel, als de klant is geregistreerd. Verbinden met `customer_entity.entity_id` om klantenattributen te bepalen verbonden aan de gebruiker die de kar creeerde. Als de winkelwagen is gemaakt via uitchecken door gasten, wordt dit veld weergegeven `NULL` |
| `entity_id` (PK) | Unieke id voor de tabel en wordt doorgaans gebruikt in combinatie met andere tabellen binnen de instantie Commerce |
| `is_active` | Een Booleaans veld dat &quot;1&quot; retourneert als het winkelwagentje door een klant is gemaakt en nog niet is omgezet in een bestelling. Hiermee wordt &quot;0&quot; geretourneerd voor omgezette winkelwagentjes of winkelwagentjes die via de beheerder zijn gemaakt |
| `items_qty` | Som van de totale hoeveelheid van alle in het winkelwagentje opgenomen artikelen |
| `reserved_order_id` | `Foreign key` in verband met de `sales_order` tabel. Verbinden met `sales_order.increment_id` om orderdetails te bepalen verbonden aan een omgezette kar. Voor winkelwagentjes die niet aan een omgezette volgorde zijn gekoppeld, wordt de opdracht `reserved_order_id` blijft `NULL` |
| `store_id` | `Foreign key` in verband met de `store` tabel. Verbinden met `store`.`store_id` om te bepalen welke mening van de Opslag van de Handel met de kar wordt geassocieerd |

{style=&quot;table-layout:auto&quot;}

## Gemeenschappelijke berekende kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `Order date` | Tijdstempel die de aanmaakdatum van de volgorde van omgezette winkelwagentjes aangeeft. Berekend door verbinding `quote.reserved_order_id` tot `sales_order.increment_id` en de `sales_order.created_at` field |
| `Seconds between cart creation and order` | Verlopen tijd tussen het maken van winkelwagentjes en het maken van bestellingen. Berekend door aftrekken `created_at` van `Order date`, geretourneerd als een geheel getal van seconden |
| `Seconds since cart creation` | Verlopen tijd tussen de aanmaakdatum van de wagen en nu. Berekend door aftrekken `created_at` vanuit de tijdstempel van de server op het moment dat de query wordt uitgevoerd, wordt geretourneerd als een geheel getal van seconden. Meestal gebruikt om de leeftijd van een winkelwagen te bepalen |
| `Store name` | De naam van de winkel Commerce die aan deze bestelling is gekoppeld. Berekend door verbinding `quote.store_id` tot `store.store_id` en de `name` field |

{style=&quot;table-layout:auto&quot;}

## Algemene cijfers

| **Metrische naam** | **Beschrijving** | **Constructie** |
|---|---|---|
| `Number of abandoned carts` | Aantal kartels dat voldoet aan specifieke &quot;voorwaarden voor stopzetting&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filters:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, waarbij &quot;x&quot; overeenkomt met de verstreken tijd (in seconden) sinds het maken van een winkelwagentje waarna een winkelwagentje als verlaten wordt beschouwd |
| `Avg time to cart conversion` | De gemiddelde tijd tussen het creëren van karretjes en ordeverwezenlijking voor omgezette karretjes | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | De som van de totale potentiële inkomsten uit verlaten winkelwagentjes, waarbij inkomsten worden gedefinieerd als de `base_grand_total` field | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filters:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, waarbij &quot;x&quot; overeenkomt met de verstreken tijd (in seconden) sinds het maken van een winkelwagentje waarna een winkelwagentje als verlaten wordt beschouwd |

{style=&quot;table-layout:auto&quot;}

## Vreemde sleutelpaden verbinden

`customer_entity`

* Verbinden met `customer_entity` lijst om nieuwe klant-vlakke kolommen te creëren verbonden aan de klant die de kar creeerde.
   * Pad: `quote.customer_id` (veel) => `customer_entity.entity_id` (1)

`sales_order`

* Verbinden met `sales_order` tabel voor het maken van nieuwe kolommen die orderdetails retourneren die zijn gekoppeld aan een omgezette winkelwagentje.
   * Pad:`quote.reserved_order_id` (veel) => `sales_order.increment_id` (1)

`store`

* Verbinden met `store` tabel voor het maken van nieuwe kolommen die details retourneren die betrekking hebben op de aan de winkelwagen gekoppelde handel.
   * Pad: `quote.store_id` (veel) => `store.store_id` (1)
