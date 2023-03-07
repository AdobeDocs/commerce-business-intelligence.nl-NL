---
title: Gegevens opslaan in de handel
description: Leer hoe de gegevens worden geproduceerd, wat veroorzaakt dat een nieuwe rij wordt opgenomen, en hoe de acties in het gegevensbestand van de Handel worden geregistreerd.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 3%

---

# Gegevens opslaan in [!DNL Adobe Commerce]

Het Adobe Commerce-platform registreert en organiseert een grote verscheidenheid aan waardevolle handelsgegevens over honderden tabellen. Dit onderwerp beschrijft:

* hoe die gegevens worden gegenereerd
* wat er precies toe leidt dat een nieuwe rij wordt ingevoegd in een van de [Kernhandelsttabellen](../data-warehouse-mgr/common-mage-tables.md)
* de wijze waarop handelingen zoals het maken van een aankoop of het aanmaken van een account in de handelsdatabase worden opgenomen

Om deze concepten te verklaren, verwijs naar het volgende voorbeeld:

`Clothes4U` is een kledinghandelaar met zowel een online - als een baksteen - en mortierpresentie . Het gebruikt Magento Open Source achter zijn website om gegevens te verzamelen en te organiseren.

## `catalog\_product\_entity`

Het is 22 september, en `Clothes4U` voert drie nieuwe punten uit aan zijn Herfst lijn: `Throwback Bellbottoms`, `Straight Leg Jeans`, en `V-Neck T-Shirts`. A `Clothes4U` werknemer opent hun Admin van de Handel, klikt **[!UICONTROL Add Product]** en voert alle informatie in voor `Throwback Bellbottoms`.

Tevreden met alle montages voor `Throwback Bellbottoms`, klikt de werknemer **[!UICONTROL Save]**, die de eerste regel hieronder in de `catalog_product_entity` tabel. De werknemer herhaalt het proces, creërend een ander product van de Handel voor `Straight Leg Jeans`en vervolgens een derde voor `V-Neck T-Shirt`de tweede en derde regel hieronder invoegen in de `catalog_product_entity` tabel:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Dit is de primaire sleutel van de `catalog_product_entity` tabel, dat wil zeggen dat elke rij van de tabel een andere rij moet hebben `entity_id`. Elk `entity_id` in deze tabel kan slechts aan één product worden gekoppeld en elk product kan slechts aan één product worden gekoppeld `entity_id`
   * De bovenste regel van de bovenstaande tabel, `entity_id` = 205, is de nieuwe rij die voor &quot;Throwback Bellbottoms wordt gecreeerd.&quot; Waar `entity_id` = 205 komt voor in het handelsplatform, verwijst het naar het product &quot;Throwback Bellbottoms&quot;.
* `entity_type_id` - De handel heeft veelvoudige categorieën voorwerpen (zoals klanten, adressen, en producten om een paar te noemen), en deze kolom wordt gebruikt om de categorie te wijzen waarin deze bepaalde rij valt.
   * Dit is het `catalog_product_entity` tabel, heeft elke rij hetzelfde entiteitstype: product. In Adobe Commerce `entity_type_id` voor product is 4 , en daarom hebben alle drie de nieuwe producten voor deze kolom het rendement 4 gecreëerd.
* `attribute_set_id` - De reeksen van Attributen worden gebruikt om producten te identificeren die het zelfde van beschrijvers hebben.
   * De bovenste twee rijen van de tabel zijn de `Throwback Bellbottoms` en `Straight Leg Jeans` producten, die allebei een broek zijn. Deze producten zouden dezelfde beschrijvingen hebben (bijvoorbeeld naam, inseam, waistline) en daarom dezelfde `attribute_set_id`. de derde post, `V-Neck T-Shirt` heeft een andere `attribute_set_id` omdat het niet dezelfde beschrijvingen zou hebben als de broek; overhemden hebben geen golflengte of inseams .
* `sku` - Dit zijn unieke waarden die door de gebruiker aan elk product worden toegewezen bij het maken van een product in Adobe Commerce.
* `created_at` - Deze kolom retourneert de tijdstempel van het tijdstip waarop elk product is gemaakt

## `customer\_entity`

Kort na de toevoeging van de drie nieuwe producten, een nieuwe klant, `Sammy Customer`, bezoeken `Clothes4U`Voor het eerst is de website van Sinds `Clothes4U` gastorders niet toestaat, `Sammy Customer` moet eerst een account op de website maken. De klant voert de vereiste gegevens in en klikt op Verzenden. Dit leidt tot de volgende nieuwe invoer in het dialoogvenster [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Net als de vorige tabel, `entity_id` is de primaire sleutel van `customer_entity` tabel.
   * Wanneer `Sammy Customer` heeft een account gemaakt en de bovenstaande rij is naar de `customer_entity` tabel, klant is toegewezen `entity_id` = 214. In alle lijsten, identificeerde de klant zoals `entity_id` = 214 verwijst altijd naar de gebruiker Sammy-klant
* `entity_type_id` - Deze kolom geeft aan welk type entiteit in deze tabel wordt vermeld en werkt op dezelfde manier als in de `catalog_product_entity` table
   * Elke rij op de `customer_entity` de lijst is een klant, en de Handel bepaalt klanten als `entity_type_id` 1 standaard
* `email` - dit veld wordt gevuld met de e-mail die een nieuwe klant invoert bij het maken van zijn account
* `created_at` - Deze kolom retourneert de tijdstempel voor het tijdstip waarop elke gebruiker zich bij het programma heeft gevoegd

## `sales\_flat\_order (or Sales\_order` als u Commerce 2.0 of hoger hebt)

Nu het aanmaken van de account is voltooid, `Sammy Customer` is klaar om een aankoop te beginnen. Op de website voegt de klant twee paren van de `Throwback Bellbottoms` en één `V-Neck T-Shirt` naar de wagen. Tevreden met de selecties, beweegt de klant zich aan controle en legt de orde voor, creërend de volgende ingang op [verkoop vlakke orde lijst](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - dit is de primaire sleutel van de `sales_flat_order` tabel.
   * Wanneer Sammy-klant deze bestelling heeft geplaatst en de bovenstaande rij naar de `sales_flat_order` tabel, de volgorde is toegewezen `entity_id` = 227.
* `customer_id` - Deze kolom is de unieke id van de klant die deze specifieke bestelling heeft geplaatst.
   * De `customer_id` aan deze bestelling is gekoppeld, is 214; dit is de `entity_id` op de `customer_entity` tabel.
* `subtotal` - Deze kolom is het totale bedrag dat aan een klant voor de bestelling in rekening wordt gebracht
   * De twee paren &quot;Throwback Bellbottoms&quot; en &quot;V-Neck T-Shirt&quot; kosten in totaal $94,85
* `created_at` - Deze kolom retourneert de tijdstempel voor het tijdstip waarop elke bestelling is gemaakt

## `sales\_flat\_order\_item ( or Sales\_order\_item` als u Commerce 2.0 of hoger hebt)

Naast de enkele rij op de `Sales\_flat\_order` tabel, wanneer `Sammy Customer` verzendt de orde, een rij voor elk uniek punt in die orde wordt opgenomen in [`sales\_flat\_order\_item` table](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - Deze kolom is de primaire sleutel van `sales_flat_order_item` table
   * `Sammy Customer`De orde van s heeft twee lijnen op deze lijst gecreeerd omdat de orde twee verschillende producten bevatte
* `name` - Deze kolom is de naam van het product
* `product_id` - Deze kolom is de unieke identificatie van het product waarnaar deze rij verwijst.
   * De eerste rij hierboven heeft `product_id` = 205 omdat `Throwback Bellbottoms` een `entity_id` van 205 `catalog_product_entity` table
* `order_id` - Deze kolom is de `entity_id` van de orde die deze bijzondere orde punten bevat
   * Beide rijen boven hebben `order_id` = 227 omdat ze beide deel uitmaken van de volgorde geplaatst door `Sammy Customer`, die `entity_id` = 227 op de `sales_flat_order` table
* `qty_ordered` - Deze kolom is het aantal eenheden van het product dat in deze specifieke volgorde is opgenomen
   * `Sammy Customer`De volgorde bevat twee paren `Throwback Bellbottoms`
* `price` - Deze kolom is de prijs van één eenheid van het orderitem
   * De `subtotal` van `Sammy Customer`s volgorde in de `sales_flat_order` de tabel was 94.85 , de som van twee paren van `Throwback Bellbottoms` bij $ 39,95 elk en 1 `V-Neck T-Shirt` tegen $ 14,95.
