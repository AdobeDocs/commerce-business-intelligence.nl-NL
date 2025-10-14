---
title: customer_entity-tabel
description: Leer hoe u records van alle geregistreerde accounts kunt openen.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# customer_entity-tabel

De tabel `customer_entity` bevat records van alle geregistreerde accounts. Een account wordt beschouwd als geregistreerd als ze zich aanmelden voor een account, ongeacht of ze ooit een aankoop hebben voltooid. Elke rij komt overeen met één unieke geregistreerde account, zoals wordt aangegeven door het account `entity_id` .

Deze lijst bevat geen verslagen van klanten die een orde via gastcontrole plaatsen. Als uw opslag gastcontrole goedkeurt, zie [&#x200B; hoe te om gastorden &#x200B;](../data-warehouse-mgr/guest-orders.md) voor die orden rekenschap te geven.

## Algemene kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `created_at` | Tijdstempel die overeenkomt met de registratiedatum van het account en die lokaal in UTC is opgeslagen. Afhankelijk van uw configuratie in [!DNL Commerce Intelligence] kan dit tijdstempel worden omgezet in een tijdzone voor rapportage in [!DNL Commerce Intelligence] die afwijkt van de tijdzone van uw database |
| `email` | E-mailadres gekoppeld aan de account |
| `entity_id` (PK) | De unieke id voor de tabel en wordt doorgaans gebruikt in verbindingen met de `customer_id` in andere tabellen in de instantie |
| `group_id` | External key gekoppeld aan de tabel `customer_group` . Meld u aan bij `customer_group.customer_group_id` om te bepalen welke klantengroep aan de geregistreerde account is gekoppeld |
| `store_id` | External key gekoppeld aan de tabel `store` . Verbinden met `store` .`store_id` om te bepalen welke Commerce-winkelweergave is gekoppeld aan het geregistreerde account |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Customer's first 30 day revenue` | Totaal van de inkomsten voor alle orders die door deze klant binnen 30 dagen na de eerste besteldatum van de klant zijn geplaatst. Berekend door `customer_entity.entity_id` samen te voegen tot `sales_order.customer_id` en het veld `base_grand_total` op te tellen voor alle opdrachten waarbij `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, ofwel het aantal seconden in 30 dagen. |
| `Customer's first order date` | Tijdstempel van de eerste volgorde die door deze klant is geplaatst. Berekend door `customer_entity.entity_id` tot `sales_order.customer_id` samen te voegen en de minimum `sales_order` te retourneren.`created_at` value |
| `Customer's first order's billing region` | Factureringsgebied verbonden aan de eerste orde van de klant. Berekend door `customer_entity.entity_id` met `sales_order.customer_id` te verbinden en `Billing address region` waar `sales_order.Customer's order number` = 1 te retourneren |
| `Customer's first order's coupon_code` | Couponcode die is gekoppeld aan de eerste bestelling van de klant. Berekend door `customer_entity.entity_id` met `sales_order.customer_id` te verbinden en `sales_order.coupon_code` waar `sales_order.Customer's order number` = 1 te retourneren |
| `Customer's group code` | Groepsnaam van de geregistreerde klant. Berekend door `customer_entity.group_id` aan `customer_group` samen te voegen.`customer_group_id` en het veld `customer_group_code` retourneren |
| `Customer's lifetime number of coupons` | Het totale aantal coupons dat op alle door deze klant geplaatste orders wordt toegepast. Berekend door `customer_entity.entity_id` aan `sales_order.customer_id` samen te voegen en het aantal bestellingen te tellen waarbij `sales_order.coupon_code` niet `NULL` is |
| `Customer's lifetime number of orders` | Totaal aantal orders geplaatst door deze klant. Berekend door `customer_entity.entity_id` tot `sales_order.customer_id` samen te voegen en het aantal rijen in de tabel `sales_order` te tellen |
| `Customer's lifetime revenue` | Som totaal van opbrengsten voor alle orders geplaatst door deze klant. Berekend door `customer_entity.entity_id` tot `sales_order.customer_id` samen te voegen en het veld `base_grand_total` op te tellen voor alle bestellingen die door deze klant zijn geplaatst |
| `Seconds since customer's first order date` | Verstreken tijd tussen de eerste besteldatum van de klant en nu. Berekend door `Customer's first order date` af te trekken van de tijdstempel van de server op het moment dat de query wordt uitgevoerd, geretourneerd als een geheel getal van seconden |
| `Store name` | De naam van de Commerce-winkel die aan dit geregistreerde account is gekoppeld. Berekend door `customer_entity.store_id` met `store.store_id` te verbinden en het veld `name` te retourneren |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Avg first 30 day revenue` | De gemiddelde opbrengsten per klant voor orders die binnen 30 dagen na de eerste bestelling van de klant zijn geplaatst | Bewerking: Gemiddelde <br/> Operand: `Customer's first 30 day revenue`<br/> Tijdstempel: `created_at`<br/> Filters:<br/><br/> - \ [A \] `Seconds since customer's first order date` ≥ 2592000 (sluit klanten uit die nog niet 30 dagen sinds hun eerste orde hebben bereikt) |
| `Avg lifetime coupons` | Het gemiddelde aantal coupons dat gedurende hun levensduur op orders per klant wordt toegepast | Bewerking: Gemiddelde <br/> Operand: `Customer's lifetime number of coupons`<br/> Tijdstempel: `created_at` |
| `Avg lifetime orders` | Het gemiddelde aantal orders dat per klant gedurende zijn levensduur is geplaatst | Bewerking: Gemiddelde <br/> Operand: `Customer's lifetime number of orders`<br/> Tijdstempel: `created_at` |
| `Avg lifetime revenue` | De gemiddelde totale opbrengst per klant voor alle orders die gedurende hun levensduur zijn geplaatst | Bewerking: Gemiddelde <br/> Operand: `Customer's lifetime revenue`<br/> Tijdstempel: `created_at` |
| `New customers` | Het aantal klanten met ten minste één bestelling, gerekend op de datum van hun eerste bestelling. Hiermee sluit u accounts uit die zich registreren maar nooit een bestelling plaatsen | Bewerking: Telling <br/> Operand: `entity_id`<br/> Tijdstempel: `Customer's first order date` |
| `Registered accounts` | Het aantal geregistreerde accounts. Bevat alle geregistreerde accounts, ongeacht of de account ooit een bestelling heeft geplaatst | Bewerking: Telling <br/> Operand: `entity_id`<br/> Tijdstempel: `created_at` |

{style="table-layout:auto"}

## Vreemde sleutel die Wegen verbindt

`customer_group`

* Sluit u aan bij de tabel `customer_group` om kolommen te maken die de naam van de klantengroep van de geregistreerde account retourneren.
   * Pad: `customer_entity.group_id` (veel) => `customer_group.customer_group_id` (één)

`store`

* Sluit u aan bij de tabel `store` om kolommen te maken die gegevens retourneren die betrekking hebben op de winkel die is gekoppeld aan het geregistreerde account.
   * Pad: `customer_entity.store_id` (veel) => `store.store_id` (één)
