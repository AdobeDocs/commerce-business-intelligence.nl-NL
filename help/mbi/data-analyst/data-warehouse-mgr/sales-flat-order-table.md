---
title: sales_order tabel
description: Leer hoe u met de tabel sales_order werkt.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# `sales_order` Tabel

De `sales_order` tabel (`sales_flat_order` op M1) is waar elke bestelling wordt vastgelegd. Doorgaans vertegenwoordigt elke rij één unieke volgorde, hoewel er aangepaste implementaties van Handel zijn die resulteren in het splitsen van een volgorde in afzonderlijke rijen.

Deze lijst omvat alle klantenorden, of die orde door gastcontrole werd verwerkt. Als je winkel het uitchecken van gasten accepteert, kun je meer informatie over dit onderwerp vinden [use case](../data-warehouse-mgr/guest-orders.md).

## Algemene kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `base_currency_code` | Valuta voor alle waarden die zijn vastgelegd in `base_*` velden (dat wil zeggen `base_grand_total`, `base_subtotal`, enzovoort). Dit weerspiegelt doorgaans de standaardvaluta van de Commerce Store |
| `base_discount_amount` | Korting op bestelling |
| `base_grand_total` | De uiteindelijke prijs die de klant op de bestelling heeft betaald, nadat alle belastingen, verzendkosten en kortingen zijn toegepast. Hoewel de precieze berekening aanpasbaar is, wordt in het algemeen `base_grand_total` wordt berekend als `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Bruto-handelswaarde van alle in de order opgenomen items. Belastingen, verzendkosten, kortingen enzovoort zijn niet inbegrepen |
| `base_shipping_amount` | Verzendwaarde toegepast op bestelling |
| `base_tax_amount` | Belastingwaarde toegepast op bestelling |
| `billing_address_id` | `Foreign key` in verband met de `sales_order_address` tabel. Verbinden met `sales_order_address.entity_id` om de factureringsadresdetails te bepalen verbonden aan de orde |
| `coupon_code` | Coupon toegepast op bestelling. Als er geen coupon wordt toegepast, wordt dit veld `NULL` |
| `created_at` | Tijdstempel van de bestelling wordt lokaal in UTC opgeslagen. Afhankelijk van uw configuratie in [!DNL Commerce Intelligence]kan deze tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL Commerce Intelligence] die van uw streek van de gegevensbestandtijd verschilt |
| `customer_email` | E-mailadres van de klant die de bestelling plaatst. Dit is in alle situaties bevolkt, met inbegrip van bestellingen die door gastafhandeling worden verwerkt |
| `customer_group_id` | Buitenlandse sleutel gekoppeld aan de `customer_group` tabel. Verbinden met `customer_group.customer_group_id` om de klantengroep te bepalen verbonden aan de orde |
| `customer_id` | `Foreign key` in verband met de `customer_entity` tabel, als de klant is geregistreerd. Verbinden met `customer_entity.entity_id` om klantenattributen te bepalen verbonden aan de orde. Als de bestelling via uitchecken door gasten is geplaatst, is dit veld `NULL` |
| `entity_id` (PK) | Unieke id voor de tabel en wordt doorgaans gebruikt in combinatie met andere tabellen binnen de instantie Commerce |
| `increment_id` | Unieke identificatiecode voor een order, gewoonlijk aangeduid als de `order_id` in Adobe Commerce. De `increment_id` wordt het vaakst gebruikt voor verbindingen met externe bronnen, zoals [!DNL Google Ecommerce] |
| `shipping_address_id` | Buitenlandse sleutel gekoppeld aan de `sales_order_address` tabel. Verbinden met `sales_order_address.entity_id` om de verzendadresgegevens van de bestelling te bepalen |
| `status` | Status van bestelling. Kan waarden als &#39;complete&#39;, &#39;processing&#39;, &#39;canceled&#39;, &#39;teruggegeven&#39; en aangepaste statussen die in de instantie Commerce zijn geïmplementeerd, retourneren. Afhankelijk van wijzigingen in de verwerking van de bestelling |
| `store_id` | `Foreign key` in verband met de `store` tabel. Verbinden met `store`.`store_id` om te bepalen welke de opslagmening van de Handel met de orde wordt geassocieerd |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `Billing address city` | Factureringsplaats voor de bestelling. Berekend door verbinding `sales_order`.`billing_address_id` tot `sales_order_address`.`entity_id` en de `city` field |
| `Billing address country` | Code van het land van de facturering voor de bestelling. Berekend door verbinding `sales_order`.`billing_address_id` tot `sales_order_address`.`entity_id` en de `country_id` |
| `Billing address region` | Factureringsgebied (meestal land of provincie) voor de bestelling. Berekend door verbinding `sales_order`.`billing_address_id` tot `sales_order_address`.`entity_id` en de `region` field |
| `Customer's first order date` | Tijdstempel van de eerste volgorde die door deze klant is geplaatst. Vaak beschouwd als de &quot;overnamedatum&quot; voor een klant. Berekend door het minimum te retourneren `sales_order`.`created_at` waarde voor elke unieke klant |
| `Customer's first order's billing region` | Factureringsgebied voor overname voor de klant die de bestelling heeft geplaatst. Berekend door de `Billing address region` gekoppeld aan de eerste bestelling van de klant |
| `Customer's first order's coupon_code` | Code van het overnamecertificaat voor de klant die deze bestelling heeft geplaatst. Berekend door de `coupon_code` gekoppeld aan de eerste bestelling van de klant |
| `Customer's group code` | Groepsnaam van de klant die deze bestelling heeft geplaatst. Berekend door verbinding `sales_order`.`customer_group_id` tot `customer_group`.`customer_group_id` en de `customer_group_code` field |
| `Customer's lifetime number of coupons` | Het totale aantal coupons dat wordt toegepast op alle orders die door deze klant worden geplaatst. Berekend door het aantal orders te tellen waarbij de `coupon_code` is niet `NULL` voor elke unieke klant |
| `Customer's lifetime number of orders` | Totaal aantal orders geplaatst door deze klant. Berekend door het aantal rijen in de `sales_order` tabel voor elke unieke klant |
| `Customer's lifetime revenue` | Som totaal van opbrengsten voor alle orders geplaatst door deze klant. Berekend door de `base_grand_total` veld voor alle orders voor elke unieke klant |
| `Customer's order number` | Volgorde in volgorde voor bestelling van deze klant. Berekend door alle orders te identificeren die door een klant zijn geplaatst, en deze in oplopende volgorde te sorteren door de `created_at` tijdstempel en een incrementele geheel-getalwaarde toewijzen aan elke volgorde. De eerste bestelling van de klant retourneert bijvoorbeeld een `Customer's order number` van 1, retourneert de tweede bestelling van de klant een `Customer's order number` van 2 enzovoort. |
| `Customer's order number (previous-current)` | Rang van de vorige bestelling van de klant samengevoegd met de rangorde van deze bestelling, gescheiden door een `-` teken. Berekend door samenvoegen (&quot;`Customer's order number` - 1&quot;) met &quot;`-`&quot; gevolgd door &quot;`Customer's order number`&quot;. Voor de bestelling die is gekoppeld aan de tweede aankoop van de klant retourneert deze kolom bijvoorbeeld de waarde van `1-2`. Het vaakst gebruikt wanneer het vertegenwoordigen van de tijd tussen twee ordegebeurtenissen (namelijk in de &quot;Tijd tussen orden&quot;grafiek) |
| `Is customer's last order?` | Hiermee wordt bepaald of de bestelling overeenkomt met de laatste of meest recente bestelling van de klant. Berekend door de `Customer's order number` waarde met `Customer's lifetime number of orders`. Wanneer deze twee velden gelijk zijn voor de opgegeven volgorde, wordt deze kolom geretourneerd `Yes`; anders retourneert het `No` |
| `Number of items in order` | Totale hoeveelheid items die in de bestelling is opgenomen. Berekend door verbinding `sales_order`.`entity_id` tot `sales_order_item`.`order_id` en de `sales_order_item`.`qty_ordered` field |
| `Seconds between customer's first order date and this order` | Verlopen tijd tussen deze bestelling en de eerste bestelling van de klant. Berekend door aftrekken `Customer's first order date` van de `created_at` voor elke orde, teruggekeerd als geheel aantal seconden |
| `Seconds since previous order` | Verlopen tijd tussen deze bestelling en de onmiddellijk voorafgaande bestelling van de klant. Berekend door de `created_at` voor de vorige bestelling van de `created_at` van deze volgorde, geretourneerd als een geheel getal van seconden. Bijvoorbeeld, voor het orderverslag dat aan de derde orde van een klant beantwoordt, keert deze kolom het aantal seconden tussen de tweede orde van de klant en derde orde terug. Voor de eerste bestelling van de klant retourneert dit veld `NULL` |
| `Shipping address city` | Plaats van verzending voor de bestelling. Berekend door verbinding `sales_order`.`shipping_address_id` tot `sales_order_address`.`entity_id` en de `city` field |
| `Shipping address country` | Landcode voor verzending van de bestelling. Berekend door verbinding `sales_order`.`Shipping_address_id` tot `sales_order_address`.`entity_id` en de `country_id` |
| `Shipping address region` | Verzendgebied (meestal provincie of staat) voor de bestelling. Berekend door verbinding `sales_order`.`shipping_address_id` tot `sales_order_address`.`entity_id` en de `region` field |
| `Store name` | De naam van de winkel Commerce die aan deze bestelling is gekoppeld. Berekend door verbinding `sales_order`.`store_id` tot `store`.`store_id` en de `name` field |

## Algemene cijfers

| **Metrische naam** | **Beschrijving** | **Constructie** |
|---|---|---|
| `Avg order value` | De gemiddelde ontvangsten per bestelling, waarbij de ontvangsten worden gedefinieerd als de `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | De gemiddelde tijd tussen (n-1) orde van een klant en nth orde, voor alle klanten en orden | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | De som van de bruto-handelswaarde voor alle orders, waarbij GMV wordt gedefinieerd als het subtotaal, voordat alle belastingen en kortingen worden toegepast | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | De mediane tijd tussen de (n-1) orde van een klant en nde orde, voor alle klanten en orden | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Totaal aantal geplaatste orders | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | De som van de opbrengsten van alle orders, waarbij de opbrengsten worden gedefinieerd als de uiteindelijke prijs die de klant betaalt, na alle belastingen, kortingen, verzendingen enzovoort. | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | De som van het verzendbedrag voor alle bestellingen | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | De som van de belastingen die op alle orders worden toegepast | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Het aantal unieke klanten die een orde in het bepaalde rapporteringstijdinterval plaatsen. Bijvoorbeeld als het interval van het rapport wekelijks was, wordt elke klant die minstens één orde in een bepaalde week plaatst precies eens geteld, ongeacht hoeveel orden zij in die week plaatsten | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Paden samenvoegen

`customer_entity`

* Verbinden met `customer_entity` lijst om nieuwe klant-vlakke kolommen te creëren verbonden aan de klant die de orde plaatste.
   * Pad: `sales_order.customer_id` (veel) => `customer_entity.entity_id` (1)

`customer_group`

* Verbinden met `customer_group` lijst om kolommen tot stand te brengen die de naam van de klantengroep van de klant terugkeren die de orde plaatste.
   * Pad: `sales_order.customer_group_id` (veel) => `customer_group.customer_group_id` (1)

`sales_order_address`

* Verbinden met `sales_order_address` tabel om kolommen te maken die facturerings- en verzendlocaties voor de bestelling retourneren. Twee verbindende wegen zijn mogelijk, afhankelijk van of de het factureren of verzendende details worden vereist.
   * Paden:
      * Verzending: `sales_order.shipping_address_id`(veel) => `sales_order_address.entity_id` (1)
      * Facturering: `sales_order.billing_address_id`(veel) => `sales_order_address.entity_id` (1)

`store`

* Verbinden met `store` tabel om kolommen te maken die details retourneren met betrekking tot de winkel Commerce die aan de bestelling is gekoppeld.
   * Pad: `sales_order.store_id` (veel) => `store.store_id` (1)
