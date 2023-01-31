---
title: customer_entity-tabel
description: Leer hoe u records van alle geregistreerde accounts kunt openen.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# klant_entiteitstabel

De `customer_entity` de tabel bevat een overzicht van alle geregistreerde accounts . Een account wordt beschouwd als geregistreerd als ze zich aanmelden voor een account, ongeacht of ze ooit een aankoop hebben voltooid. Elke rij komt overeen met één unieke geregistreerde account, zoals die door de `entity_id`.

Deze lijst bevat geen verslagen van klanten die een orde via gastcontrole plaatsen. Als je winkel het uitchecken van gasten accepteert, [leren hoe u account kunt maken](../data-warehouse-mgr/guest-orders.md) voor die klanten.

## Algemene kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `created_at` | Tijdstempel die overeenkomt met de registratiedatum van de account, wordt gewoonlijk lokaal opgeslagen in UTC. Afhankelijk van uw configuratie in [!DNL MBI]kan deze tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL MBI] die van uw streek van de gegevensbestandtijd verschilt |
| `email` | E-mailadres gekoppeld aan de account |
| `entity_id` (PK) | De unieke id voor de tabel en wordt doorgaans gebruikt in verbindingen met de `customer_id` in andere tabellen binnen de instantie |
| `group_id` | Buitenlandse sleutel gekoppeld aan de `customer_group` tabel. Verbinden met `customer_group.customer_group_id` om de klantengroep te bepalen die aan de geregistreerde rekening wordt geassocieerd |
| `store_id` | Buitenlandse sleutel gekoppeld aan de `store` tabel. Verbinden met `store`.`store_id` om te bepalen welke mening van de Winkel van de Handel met de geregistreerde rekening wordt geassocieerd |

{style=&quot;table-layout:auto&quot;}

## Gemeenschappelijke berekende kolommen

| **Kolomnaam** | **Beschrijving** |
|---|---|
| `Customer's first 30 day revenue` | Totaal van de inkomsten voor alle orders die door deze klant binnen 30 dagen na de eerste besteldatum van de klant zijn geplaatst. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en de `base_grand_total` veld voor alle orders `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, het aantal seconden in 30 dagen |
| `Customer's first order date` | Tijdstempel van de eerste volgorde die door deze klant is geplaatst. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en het minimum `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Factureringsgebied verbonden aan de eerste orde van de klant. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en de `Billing address region` waar `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Couponcode die is gekoppeld aan de eerste bestelling van de klant. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en de `sales_order.coupon_code` waar `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Groepsnaam van de geregistreerde klant. Berekend door verbinding `customer_entity.group_id` tot `customer_group`.`customer_group_id` en de `customer_group_code` field |
| `Customer's lifetime number of coupons` | Het totale aantal coupons dat wordt toegepast op alle orders die door deze klant worden geplaatst. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en tellen van het aantal orders waarbij `sales_order.coupon_code` is niet `NULL` |
| `Customer's lifetime number of orders` | Totaal aantal orders geplaatst door deze klant. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en het aantal rijen tellen in de `sales_order` table |
| `Customer's lifetime revenue` | Som totaal van opbrengsten voor alle orders geplaatst door deze klant. Berekend door verbinding `customer_entity.entity_id` tot `sales_order.customer_id` en de `base_grand_total` veld voor alle orders geplaatst door deze klant |
| `Seconds since customer's first order date` | Verstreken tijd tussen de eerste besteldatum van de klant en nu. Berekend door aftrekken `Customer's first order date` vanuit de tijdstempel van de server op het moment dat de query wordt uitgevoerd, geretourneerd als een geheel getal van seconden |
| `Store name` | De naam van de winkel Commerce die aan dit geregistreerde account is gekoppeld. Berekend door verbinding `customer_entity.store_id` tot `store.store_id` en de `name` field |

{style=&quot;table-layout:auto&quot;}

## Algemene cijfers

| **Metrische naam** | **Beschrijving** | **Constructie** |
|---|---|---|
| `Avg first 30 day revenue` | De gemiddelde opbrengsten per klant voor orders die binnen 30 dagen na de eerste bestelling van de klant zijn geplaatst | Bewerking: Gemiddeld<br/>Operand: `Customer's first 30 day revenue`<br/>Tijdstempel: `created_at`<br/>Filters:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exclusief klanten die nog geen 30 dagen na hun eerste bestelling hebben bereikt) |
| `Avg lifetime coupons` | Het gemiddelde aantal coupons dat gedurende hun levensduur op orders per klant wordt toegepast | Bewerking: Gemiddeld<br/>Operand: `Customer's lifetime number of coupons`<br/>Tijdstempel: `created_at` |
| `Avg lifetime orders` | Het gemiddelde aantal orders dat per klant gedurende zijn levensduur is geplaatst | Bewerking: Gemiddeld<br/>Operand: `Customer's lifetime number of orders`<br/>Tijdstempel: `created_at` |
| `Avg lifetime revenue` | De gemiddelde totale opbrengst per klant voor alle orders die gedurende hun levensduur zijn geplaatst | Bewerking: Gemiddeld<br/>Operand: `Customer's lifetime revenue`<br/>Tijdstempel: `created_at` |
| `New customers` | Het aantal klanten met ten minste één bestelling, gerekend op de datum van hun eerste bestelling. Hiermee sluit u accounts uit die zich registreren maar nooit een bestelling plaatsen | Bewerking: Aantal<br/>Operand: `entity_id`<br/>Tijdstempel: `Customer's first order date` |
| `Registered accounts` | Het aantal geregistreerde accounts. Bevat alle geregistreerde accounts, ongeacht of de account ooit een bestelling heeft geplaatst | Bewerking: Aantal<br/>Operand: `entity_id`<br/>Tijdstempel: `created_at` |

{style=&quot;table-layout:auto&quot;}

## Vreemde sleutelpaden verbinden

`customer_group`

* Verbinden met `customer_group` tabel om nieuwe kolommen te maken die de naam van de klantengroep van de geregistreerde account retourneren.
   * Pad: `customer_entity.group_id` (veel) => `customer_group.customer_group_id` (1)

`store`

* Verbinden met `store` tabel voor het maken van nieuwe kolommen die gegevens retourneren die betrekking hebben op de winkel die is gekoppeld aan een geregistreerde account.
   * Pad: `customer_entity.store_id` (veel) => `store.store_id` (1)
