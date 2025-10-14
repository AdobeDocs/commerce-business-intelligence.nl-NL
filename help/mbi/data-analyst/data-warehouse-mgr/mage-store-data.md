---
title: Gegevens opslaan in Adobe Commerce
description: Leer hoe de gegevens worden geproduceerd, wat veroorzaakt dat een nieuwe rij wordt opgenomen, en hoe de acties in het gegevensbestand van Adobe Commerce worden geregistreerd.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Gegevens opslaan in [!DNL Adobe Commerce]

Het platform van [!DNL Adobe Commerce] registreert en organiseert een grote verscheidenheid van waardevolle handelsgegevens over honderden lijsten. Dit onderwerp beschrijft:

* hoe die gegevens worden gegenereerd
* wat een nieuwe rij veroorzaakt om in één van de [&#x200B; Lijsten van Commerce van de Kern worden opgenomen &#x200B;](../data-warehouse-mgr/common-mage-tables.md)
* hoe handelingen zoals het maken van een aankoop of het maken van een account worden opgenomen in de [!DNL Adobe Commerce] -database

Raadpleeg het volgende voorbeeld om deze concepten te bespreken:

`Clothes4U` is een kleding-retailer met zowel een online als een baksteen- en mortierpresentie. [!DNL Magento Open Source] achter de website wordt gebruikt om gegevens te verzamelen en te ordenen.

## `catalog\_product\_entity`

Het is 22 september en `Clothes4U` implementeert drie nieuwe items naar de Fall-regel: `Throwback Bellbottoms`, `Straight Leg Jeans` en `V-Neck T-Shirts` . Een `Clothes4U` employee opent zijn Commerce-beheerder, klikt op **[!UICONTROL Add Product]** en voert alle informatie in voor `Throwback Bellbottoms` .

Tevreden met alle montages voor `Throwback Bellbottoms`, klikt de werknemer **[!UICONTROL Save]**, die de eerste lijn hieronder in de `catalog_product_entity` lijst opneemt. De employee herhaalt het proces, waarbij een ander Commerce-product voor `Straight Leg Jeans` wordt gemaakt en een derde voor `V-Neck T-Shirt` , waarbij de tweede en derde regel onder in de tabel `catalog_product_entity` worden ingevoegd:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09 :15: 43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09 :18: 17 |
| 207 | 4 | 12 | Hemden6 | 2016/09/22 09 :24: 02 |

* `entity_id` - Dit is de primaire sleutel van de `catalog_product_entity` -tabel. Dit houdt in dat elke rij van de tabel een andere `entity_id` moet hebben. Elke `entity_id` in deze tabel kan slechts aan één product worden gekoppeld en elk product kan slechts aan één product worden gekoppeld `entity_id`
   * De bovenste regel van de bovenstaande tabel, `entity_id` = 205, is de nieuwe rij die is gemaakt voor &quot;Throwback Bellbottoms&quot;. Waar `entity_id` = 205 wordt weergegeven op het Commerce-platform, verwijst dit naar het product &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - Commerce heeft meerdere categorieën objecten (zoals klanten, adressen en producten die een paar namen moeten geven). Deze kolom wordt gebruikt om de categorie aan te duiden waarin deze bepaalde rij valt.
   * Omdat dit de `catalog_product_entity` lijst is, heeft elke rij het zelfde entiteitstype: product. In Adobe Commerce is de waarde van `entity_type_id` for product 4. Daarom hebben alle drie de nieuwe producten return 4 voor deze kolom gemaakt.
* `attribute_set_id` - Kenmerksets worden gebruikt om producten te identificeren die dezelfde beschrijving hebben.
   * De bovenste twee rijen van de tabel zijn de `Throwback Bellbottoms` - en `Straight Leg Jeans` -producten, die allebei een broek zijn. Deze producten zouden dezelfde beschrijvingen hebben (bijvoorbeeld naam, inseam, waistline) en hebben daarom dezelfde `attribute_set_id` . Het derde item, `V-Neck T-Shirt` , heeft een ander `attribute_set_id` omdat het niet dezelfde beschrijvingen zou hebben als de broek; overhemden hebben geen golflengte of inseam.
* `sku` - Dit zijn unieke waarden die door de gebruiker aan elk product worden toegewezen bij het maken van een product in Adobe Commerce.
* `created_at` - Deze kolom retourneert de tijdstempel van het tijdstip waarop elk product is gemaakt

## `customer\_entity`

Kort na de toevoeging van de drie nieuwe producten bezoekt een nieuwe klant, `Sammy Customer`, de website van `Clothes4U` voor het eerst. Omdat in `Clothes4U` bestellingen door gasten niet zijn toegestaan, moet `Sammy Customer` eerst een account op de website maken. De klant voert de vereiste gegevens in en klikt op Verzenden. Dit leidt tot de volgende nieuwe invoer in de [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md) :

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Net als de vorige tabel is `entity_id` de primaire sleutel van de tabel `customer_entity` .
   * Toen `Sammy Customer` een account heeft gemaakt en de bovenstaande rij naar de `customer_entity` -tabel is geschreven, is aan de klant `entity_id` = 214 toegewezen. In alle tabellen verwijst de klant die als `entity_id` = 214 wordt aangeduid, altijd naar de Sammy-klant van de gebruiker
* `entity_type_id` - Deze kolom geeft aan welk type entiteit in deze tabel wordt vermeld en werkt op dezelfde manier als in de `catalog_product_entity` -tabel
   * Elke rij in de tabel `customer_entity` is een klant en Commerce definieert klanten standaard als `entity_type_id` 1
* `email` - dit veld wordt gevuld met de e-mail die een nieuwe klant invoert bij het maken van zijn account
* `created_at` - Deze kolom retourneert de tijdstempel voor het tijdstip waarop elke gebruiker zich aanmeldt

## `sales\_flat\_order (or Sales\_order` als u [!DNL Adobe Commerce 2.x]

Nu het maken van de account is voltooid, is `Sammy Customer` gereed om een aankoop te starten. Op de website voegt de klant twee paren van de `Throwback Bellbottoms` en één `V-Neck T-Shirt` aan de winkelwagen toe. Tevreden met de selecties, beweegt de klant zich om de orde te controleren en voor te leggen, creërend de volgende ingang op de [&#x200B; lijst van de verkoop vlakke orde &#x200B;](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 2016/09/23 15 :41: 39 |

* `entity_id` - dit is de primaire sleutel van de `sales_flat_order` lijst.
   * Toen Sammy-klant deze bestelling plaatste en de bovenstaande rij naar de tabel `sales_flat_order` werd geschreven, werd de bestelling toegewezen aan `entity_id` = 227.
* `customer_id` - Deze kolom is de unieke id van de klant die deze bepaalde bestelling heeft geplaatst
   * De `customer_id` die aan deze bestelling is gekoppeld, is 214. Dit is Sammy Customer&#39;s `entity_id` in de tabel `customer_entity` .
* `subtotal` - Deze kolom is het totale bedrag dat aan een klant voor de order in rekening wordt gebracht
   * De twee paren &quot;Throwback Bellbottoms&quot; en &quot;V-Neck T-Shirt&quot; kosten in totaal $94,85
* `created_at` - Deze kolom retourneert de tijdstempel voor het tijdstip waarop elke bestelling is gemaakt

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(als u Commerce 2.0 of hoger hebt)

Naast de enkele rij op de `Sales\_flat\_order` lijst, wanneer `Sammy Customer` de orde voorlegt, wordt een rij voor elk uniek punt in die orde opgenomen in de [`sales\_flat\_order\_item` lijst &#x200B;](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Deze kolom is de primaire sleutel van de tabel `sales_flat_order_item`
   * De volgorde van `Sammy Customer` heeft twee regels voor deze tabel gemaakt omdat de volgorde twee verschillende producten bevatte
* `name` - Deze kolom is de naam van het product
* `product_id` - Deze kolom is de unieke id van het product waarnaar deze rij verwijst
   * De eerste rij hierboven heeft `product_id` = 205 omdat `Throwback Bellbottoms` een `entity_id` waarde van 205 heeft in de `catalog_product_entity` -tabel
* `order_id` - Deze kolom is de `entity_id` van de volgorde die deze bepaalde volgordepunten bevat
   * Beide rijen boven hebben `order_id` = 227 omdat ze beide deel uitmaken van de volgorde die wordt geplaatst door `Sammy Customer` , met `entity_id` = 227 in de `sales_flat_order` -tabel
* `qty_ordered` - Deze kolom is het aantal eenheden van het product dat in deze specifieke volgorde is opgenomen
   * De volgorde van `Sammy Customer` bevatte twee paren van `Throwback Bellbottoms`
* `price` - Deze kolom is de prijs van één eenheid van het orde punt
   * De `subtotal` van de orde van `Sammy Customer` in de `sales_flat_order` lijst was 94.85, die de som twee paren van `Throwback Bellbottoms` bij $39.95 elk en 1 `V-Neck T-Shirt` bij $14.95 is.
