---
title: enterprise_rma-tabel
description: Leer hoe u informatie over een specifieke retouraanvraag analyseert.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# enterprise_rma-tabel

Elke rij in de tabel `enterprise_rma` (wordt vaak `magento_rma` in Adobe Commerce 2.x genoemd, maar de naam kan worden aangepast) bevat informatie over een specifieke retouraanvraag.

>[!NOTE]
>
>Deze tabel wordt alleen standaard geleverd bij uw Adobe Commerce-account als u een `Enterprise Edition` - of `Enterprise Cloud Edition` -klant bent.

## Algemene native kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `entity\_id` | Unieke id voor de tabel. Elke `entity\_id` vertegenwoordigt een geretourneerde aanvraag. |
| `date\_requested` | De datum waarop de terugkeer werd gevraagd. |
| `status` | De status van de terugkeer. Waarden zijn onder andere &#39;receive&#39;, &#39;pending&#39;, &#39;authorised&#39;. |
| `order\_id` | External key gekoppeld aan de tabel `sales\_flat\_order` . |
| `customer\_id` | External key gekoppeld aan de tabel `customer\_entity` . |

{style="table-layout:auto"}

## Gemeenschappelijke berekende kolommen

| **de Naam van de Kolom** | **Beschrijving** |
|---|---|
| `Order's created\_at` | Dit is de datum van de oorspronkelijke bestelling. Dit kan worden gebruikt om de tijd tussen orde en terugkeerverzoek te verkrijgen. |
| `Customer's order number` | Dit is het bestelnummer van de klant dat aan de oorspronkelijke bestelling is gekoppeld. |
| `Seconds between order's created\_at and return's date\_requested` | Het aantal seconden vanaf de besteldatum tot de geretourneerde aanvraag. |
| `Return's total value` | Dit is het totale monetaire bedrag dat wordt teruggegeven. Dit is de som van het individuele retourbedrag van elk retouritem. |

{style="table-layout:auto"}

## Algemene cijfers

| **Metrische Naam** | **Beschrijving** | **Bouw** |
|---|---|---|
| `Number of returns` | The number of returns requested. | `Operation` column: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Column: `date requested` |
| `Total returned amount` | Het totale geretourneerde monetaire bedrag. | `Operation ` Kolom: `Return's total value`<br>`Operation`: Som <br>`Timestamp` Kolom: gevraagde datum |
| `Average returned amount` | Het gemiddelde monetaire bedrag dat is geretourneerd. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Column: `date requested` |
| `Average time to return` | De gemiddelde tijd van orde om terug te keren. | `Operation` Kolom: seconden tussen de aanmaakdatum van de order en de opgevraagde datum van de geretourneerde waarde <br>`Operation`: `Average`<br>`Timestamp` Kolom: `date requested` |

{style="table-layout:auto"}

## Verbindingen met Andere Lijsten

`sale_flat_order`

* Maak bij elkaar gevoegde kolommen om te segmenteren en filteren door kenmerk op orderniveau in de tabel `enterprise_rma` via de volgende samenvoeging:
   * Commerce 1.x: `enterprise_rma.order_id` (many) => `sales_flat_order.entity_id` (one)
   * Commerce 2.x: `magento_rma.order_id` (veel) => `sales_order.entity_id` (één)

`enterprise_rma_item_entity`

* U kunt een veel-op-een kolom maken, zoals `Return's total value` in de `enterprise_rma` -tabel via de volgende samenvoeging:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (many) => `enterprise_rma.entity_id` (one)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (veel) => `magento_rma.entity_id` (één)
