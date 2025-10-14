---
title: sales_order tabel
description: Leer hoe u met de tabel sales_order werkt.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# `sales_order` Tabel

In de `sales_order` -tabel (`sales_flat_order` op M1) wordt elke volgorde vastgelegd. Doorgaans vertegenwoordigt elke rij één unieke volgorde, hoewel er aangepaste implementaties van Commerce zijn die resulteren in het splitsen van een volgorde in afzonderlijke rijen.

Deze lijst omvat alle klantenorden, of die orde door gastcontrole werd verwerkt. Als uw opslag gastcontrole goedkeurt, kunt u meer informatie over dit [&#x200B; gebruiksgeval &#x200B;](../data-warehouse-mgr/guest-orders.md) vinden.

## Algemene kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `base_currency_code` | Valuta voor alle waarden die zijn vastgelegd in `base_*` -velden (dat wil zeggen `base_grand_total` , `base_subtotal` , enzovoort). Dit is doorgaans de standaardvaluta van de Commerce Store. |
| `base_discount_amount` | Korting op bestelling |
| `base_grand_total` | De uiteindelijke prijs die de klant op de bestelling heeft betaald, nadat alle belastingen, verzendkosten en kortingen zijn toegepast. Hoewel de exacte berekening aanpasbaar is, wordt de waarde van `base_grand_total` doorgaans berekend als `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Bruto-handelswaarde van alle in de order opgenomen items. Belastingen, verzendkosten, kortingen enzovoort zijn niet inbegrepen |
| `base_shipping_amount` | Verzendwaarde toegepast op bestelling |
| `base_tax_amount` | Belastingwaarde toegepast op bestelling |
| `billing_address_id` | `Foreign key` die aan de tabel `sales_order_address` is gekoppeld. Verbinden met `sales_order_address.entity_id` om de factureringsadresdetails te bepalen verbonden aan de orde |
| `coupon_code` | Coupon toegepast op bestelling. Als er geen coupon wordt toegepast, is dit veld `NULL` |
| `created_at` | Tijdstempel voor het maken van de bestelling, lokaal opgeslagen in UTC. Afhankelijk van uw configuratie in [!DNL Commerce Intelligence] kan dit tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL Commerce Intelligence] die afwijkt van de tijdzone van uw database |
| `customer_email` | E-mailadres van de klant die de bestelling plaatst. Dit is in alle situaties bevolkt, met inbegrip van bestellingen die door gastafhandeling worden verwerkt |
| `customer_group_id` | External key gekoppeld aan de tabel `customer_group` . Verbinden met `customer_group.customer_group_id` om de klantengroep te bepalen verbonden aan de orde |
| `customer_id` | `Foreign key` die aan de tabel `customer_entity` is gekoppeld, als de klant is geregistreerd. Sluit u aan bij `customer_entity.entity_id` om te bepalen welke klantkenmerken aan de order zijn gekoppeld. Als de volgorde door uitchecken door gasten is geplaatst, is dit veld `NULL` |
| `entity_id` (PK) | Unieke id voor de tabel en wordt doorgaans gebruikt in verbindingen met andere tabellen binnen de Commerce-instantie |
| `increment_id` | Unieke id voor een bestelling. Wordt meestal `order_id` in Adobe Commerce genoemd. `increment_id` wordt het meest gebruikt voor verbindingen met externe bronnen, zoals [!DNL Google Ecommerce] |
| `shipping_address_id` | External key gekoppeld aan de tabel `sales_order_address` . Sluit u aan bij `sales_order_address.entity_id` om de verzendadresgegevens voor de bestelling te bepalen |
| `status` | Status van bestelling. Kan waarden als &#39;complete&#39;, &#39;processing&#39;, &#39;canceled&#39;, &#39;teruggegeven&#39; en aangepaste statussen die zijn geïmplementeerd op de Commerce-instantie, retourneren. Afhankelijk van wijzigingen in de verwerking van de bestelling |
| `store_id` | `Foreign key` die aan de tabel `store` is gekoppeld. Verbinden met `store` .`store_id` om te bepalen welke Commerce-winkelweergave is gekoppeld aan de bestelling |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Billing address city` | Factureringsplaats voor de bestelling. Berekend door `sales_order` samen te voegen.`billing_address_id` tot en met `sales_order_address` .`entity_id` en het veld `city` retourneren |
| `Billing address country` | Code van het land van de facturering voor de bestelling. Berekend door `sales_order` samen te voegen.`billing_address_id` tot en met `sales_order_address` .`entity_id` en retourneert de `country_id` |
| `Billing address region` | Factureringsgebied (meestal land of provincie) voor de bestelling. Berekend door `sales_order` samen te voegen.`billing_address_id` tot en met `sales_order_address` .`entity_id` en het veld `region` retourneren |
| `Customer's first order date` | Tijdstempel van de eerste volgorde die door deze klant is geplaatst. Vaak beschouwd als de &quot;overnamedatum&quot; voor een klant. Berekend door het minimum `sales_order` te retourneren.`created_at` waarde voor elke unieke klant |
| `Customer's first order's billing region` | Factureringsgebied voor overname voor de klant die de bestelling heeft geplaatst. Berekend door de `Billing address region` te retourneren die is gekoppeld aan de eerste bestelling van de klant |
| `Customer's first order's coupon_code` | Code van het overnamecertificaat voor de klant die deze bestelling heeft geplaatst. Berekend door de `coupon_code` te retourneren die is gekoppeld aan de eerste bestelling van de klant |
| `Customer's group code` | Groepsnaam van de klant die deze bestelling heeft geplaatst. Berekend door `sales_order` samen te voegen.`customer_group_id` tot en met `customer_group` .`customer_group_id` en het veld `customer_group_code` retourneren |
| `Customer's lifetime number of coupons` | Het totale aantal coupons dat wordt toegepast op alle door deze klant geplaatste orders. Berekend door het aantal bestellingen te tellen waarbij `coupon_code` niet `NULL` is voor elke unieke klant |
| `Customer's lifetime number of orders` | Totaal aantal orders geplaatst door deze klant. Berekend door het aantal rijen in de tabel `sales_order` te tellen voor elke unieke klant |
| `Customer's lifetime revenue` | Som totaal van opbrengsten voor alle orders geplaatst door deze klant. Berekend door het veld `base_grand_total` op te tellen voor alle bestellingen voor elke unieke klant |
| `Customer's order number` | Volgorde voor de orde van deze klant. Berekend door alle orders te identificeren die door een klant zijn geplaatst, deze in oplopende volgorde te sorteren op het tijdstempel van `created_at` en een oplopende geheel-getalwaarde toe te wijzen aan elke bestelling. De eerste bestelling van de klant retourneert bijvoorbeeld een `Customer's order number` van 1, de tweede bestelling van de klant een `Customer's order number` van 2 enzovoort. |
| `Customer's order number (previous-current)` | Rang van de vorige bestelling van de klant samengevoegd met de rang van deze bestelling, gescheiden door een teken `-` . Berekend door (&quot;`Customer's order number` - 1&quot;) met &quot;`-`&quot;aaneen te schakelen gevolgd door &quot;`Customer's order number`&quot;. Voor de order die bijvoorbeeld aan de tweede aankoop van de klant is gekoppeld, retourneert deze kolom de waarde `1-2`. Het vaakst gebruikt wanneer het vertegenwoordigen van de tijd tussen twee ordegebeurtenissen (namelijk in de &quot;Tijd tussen orden&quot;grafiek) |
| `Is customer's last order?` | Hiermee wordt bepaald of de bestelling overeenkomt met de laatste of meest recente bestelling van de klant. Berekend door de `Customer's order number` -waarde te vergelijken met `Customer's lifetime number of orders` . Wanneer deze twee velden gelijk zijn voor de opgegeven volgorde, wordt deze kolom `Yes` geretourneerd; anders wordt `No` geretourneerd |
| `Number of items in order` | Totale hoeveelheid items die in de bestelling is opgenomen. Berekend door `sales_order` samen te voegen.`entity_id` tot en met `sales_order_item` .`order_id` en de `sales_order_item` bij te vatten.`qty_ordered` field |
| `Seconds between customer's first order date and this order` | Verlopen tijd tussen deze bestelling en de eerste bestelling van de klant. Berekend door `Customer's first order date` af te trekken van de `created_at` voor elke volgorde, geretourneerd als een geheel getal van seconden |
| `Seconds since previous order` | Verlopen tijd tussen deze bestelling en de onmiddellijk voorafgaande bestelling van de klant. Berekend door `created_at` voor de vorige volgorde af te trekken van `created_at` van deze volgorde, geretourneerd als een geheel getal van seconden. Bijvoorbeeld, voor het orderverslag dat aan de derde orde van een klant beantwoordt, keert deze kolom het aantal seconden tussen de tweede orde van de klant en derde orde terug. Voor de eerste bestelling van de klant retourneert dit veld `NULL` |
| `Shipping address city` | Plaats van verzending voor de bestelling. Berekend door `sales_order` samen te voegen.`shipping_address_id` tot en met `sales_order_address` .`entity_id` en het veld `city` retourneren |
| `Shipping address country` | Landcode voor verzending van de bestelling. Berekend door `sales_order` samen te voegen.`Shipping_address_id` tot en met `sales_order_address` .`entity_id` en retourneert de `country_id` |
| `Shipping address region` | Verzendgebied (meestal provincie of staat) voor de bestelling. Berekend door `sales_order` samen te voegen.`shipping_address_id` tot en met `sales_order_address` .`entity_id` en het veld `region` retourneren |
| `Store name` | De naam van de Commerce-winkel die aan deze bestelling is gekoppeld. Berekend door `sales_order` samen te voegen.`store_id` tot en met `store` .`store_id` en het veld `name` retourneren |

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Avg order value` | De gemiddelde opbrengst per orde, waar de opbrengst als `base_grand_total` wordt gedefinieerd | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | De gemiddelde tijd tussen (n-1) orde van een klant en nth orde, voor alle klanten en orden | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | De som van de bruto-handelswaarde voor alle orders, waarbij GMV wordt gedefinieerd als het subtotaal, voordat alle belastingen en kortingen worden toegepast | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | De mediane tijd tussen de (n-1) orde van een klant en nde orde, voor alle klanten en orden | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Het totale aantal geplaatste orders | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | De som van de opbrengsten van alle orders, waarbij de opbrengsten worden gedefinieerd als de uiteindelijke prijs die de klant betaalt, na alle belastingen, kortingen, verzendingen enzovoort. | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | De som van het verzendbedrag voor alle bestellingen | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | De som van de belastingen die op alle orders worden toegepast | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Het aantal unieke klanten die een orde in het bepaalde rapporteringstijdinterval plaatsen. Bijvoorbeeld als het interval van het rapport wekelijks was, wordt elke klant die minstens één orde in een bepaalde week plaatst precies eens geteld, ongeacht hoeveel orden zij in die week plaatsten | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Paden samenvoegen

`customer_entity`

* Sluit u aan bij de tabel `customer_entity` om nieuwe kolommen op klantniveau te maken die zijn gekoppeld aan de klant die de order heeft geplaatst.
   * Pad: `sales_order.customer_id` (veel) => `customer_entity.entity_id` (één)

`customer_group`

* Sluit u aan bij de tabel `customer_group` om kolommen te maken die de naam van de klantengroep retourneren van de klant die de order heeft geplaatst.
   * Pad: `sales_order.customer_group_id` (veel) => `customer_group.customer_group_id` (één)

`sales_order_address`

* Verbind met `sales_order_address` lijst om kolommen tot stand te brengen die het factureren en het verschepen plaatsen verbonden aan de orde terugkeren. Twee verbindende wegen zijn mogelijk, afhankelijk van of de het factureren of verzendende details worden vereist.
   * Paden:
      * Verzending: `sales_order.shipping_address_id` (veel) => `sales_order_address.entity_id` (één)
      * Facturering: `sales_order.billing_address_id` (veel) => `sales_order_address.entity_id` (één)

`store`

* Sluit u aan bij de tabel `store` om kolommen te maken die gegevens retourneren die betrekking hebben op de Commerce-winkel die aan de bestelling is gekoppeld.
   * Pad: `sales_order.store_id` (veel) => `store.store_id` (één)
