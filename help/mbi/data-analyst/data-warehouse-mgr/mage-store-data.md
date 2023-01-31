---
title: Gegevens opslaan in de handel
description: Leer hoe gegevens worden geproduceerd, wat precies veroorzaakt dat een nieuwe rij in één van de Lijsten van de Handel van de Kern wordt opgenomen, en hoe acties zoals het maken van een aankoop of het creëren van een rekening in het gegevensbestand van de Handel wordt geregistreerd.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Gegevens opslaan in [!DNL Magento]

Het platform van de Handel registreert en organiseert een grote verscheidenheid van waardevolle handelsgegevens over honderden lijsten. In dit onderwerp, zult u leren hoe dat gegeven wordt geproduceerd, wat precies veroorzaakt dat een nieuwe rij in één van wordt opgenomen [Kernhandelsttabellen](../data-warehouse-mgr/common-mage-tables.md), en hoe worden acties zoals het maken van een aankoop of het creëren van een rekening geregistreerd in het gegevensbestand van de Handel. Om deze concepten te verklaren, verwijs naar het volgende voorbeeld:

`Clothes4U` is een kledinghandelaar met zowel een online - als een baksteen - en mortierpresentie . Het gebruikt Magento Open Source achter zijn website om gegevens te verzamelen en te organiseren.

## `catalog\_product\_entity`

Het is 22 september, en `Clothes4U` voert drie nieuwe punten uit aan zijn Herfst lijn: `Throwback Bellbottoms`, `Straight Leg Jeans`, en `V-Neck T-Shirts`. A `Clothes4U` werknemer opent hun Admin van de Handel, klikt **[!UICONTROL Add Product]** en voert alle informatie in voor `Throwback Bellbottoms`.

Tevreden met alle montages voor `Throwback Bellbottoms`, klikt de werknemer **[!UICONTROL Save]**, die de eerste regel hieronder in de `catalog_product_entity` tabel. De werknemer herhaalt het proces, creërend een ander nieuw product van de Handel voor `Straight Leg Jeans`en vervolgens een derde voor `V-Neck T-Shirt`de tweede en derde regel hieronder invoegen in de `catalog_product_entity` tabel:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Hemden6 | 2016/09/22 09:24:02 |

* `entity_id` - Dit is de primaire sleutel van de `catalog_product_entity` tabel, dat wil zeggen dat elke rij van de tabel een andere rij moet hebben `entity_id`. Elk `entity_id` in deze tabel kan slechts aan één product worden gekoppeld en elk product kan slechts aan één product worden gekoppeld `entity_id`
   * De bovenste regel van de bovenstaande tabel, `entity_id` = 205, is de nieuwe rij die voor &quot;Throwback Bellbottoms wordt gecreeerd.&quot; Waar `entity_id` = 205 komt voor in het handelsplatform, verwijst het naar het product &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - De handel heeft veelvoudige categorieën voorwerpen (zoals klanten, adressen, en producten om een paar te noemen), en deze kolom wordt gebruikt om de categorie te wijzen waarin deze bepaalde rij valt.
   * Dit is het `catalog_product_entity` tabel, heeft elke rij hetzelfde entiteitstype: product. In Magento, `entity_type_id` voor product is 4 , en daarom hebben alle drie de nieuwe producten voor deze kolom het rendement 4 gecreëerd.
* `attribute_set_id` - De reeksen van Attributen worden gebruikt om producten te identificeren die het zelfde van beschrijvers hebben.
   * De bovenste twee rijen van de tabel zijn de `Throwback Bellbottoms` en `Straight Leg Jeans` producten, die allebei een broek zijn. Deze producten zouden dezelfde beschrijvingen hebben (bijvoorbeeld naam, inseam, waistline) en daarom dezelfde `attribute_set_id`. de derde post, `V-Neck T-Shirt` heeft een andere `attribute_set_id` omdat het niet dezelfde beschrijvingen zou hebben als de broek; overhemden hebben geen golflengte of inseams .
* `sku` - Dit zijn unieke waarden die door de gebruiker aan elk product worden toegewezen bij het maken van een nieuw product in Magento.
* `created_at` - Deze kolom retourneert de tijdstempel van het tijdstip waarop elk product is gemaakt

## `customer\_entity`

Kort na de toevoeging van de drie nieuwe producten, een nieuwe klant, `Sammy Customer`, bezoeken `Clothes4U`Voor het eerst is de website van Sinds `Clothes4U` niet [gastorders toestaan](https://support.magento.com/hc/en-us/articles/360016729951-Common-Magento-Misconceptions), `Sammy Customer` moet eerst een account op de website maken. Ze voert haar gegevens in en klikt op Verzenden. Dit leidt tot de volgende nieuwe vermelding in het dialoogvenster [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Net als de vorige tabel, `entity_id` is de primaire sleutel van `customer_entity` tabel.
   * Wanneer `Sammy Customer` heeft haar account gemaakt en de bovenstaande rij is naar de `customer_entity` tabel, ze is toegewezen `entity_id` = 214. In alle lijsten, identificeerde de klant zoals `entity_id` = 214 verwijst altijd naar de Sammy-gebruiker
* `entity_type_id` - Deze kolom geeft aan welk type entiteit in deze tabel wordt vermeld en werkt op dezelfde manier als in de `catalog_product_entity` table
   * Elke rij op de `customer_entity` de lijst zal een klant zijn, en de Handel bepaalt klanten als `entity_type_id` 1 standaard
* `email` - dit veld wordt gevuld met de e-mail die een nieuwe klant invoert bij het maken van zijn account
* `created_at` - Deze kolom retourneert de tijdstempel voor het tijdstip waarop elke gebruiker zich bij het programma heeft gevoegd

## `sales\_flat\_order (or Sales\_order` als u Commerce 2.0 of hoger hebt)

Met haar account is het aanmaken voltooid, `Sammy Customer` is klaar om haar aankoop te beginnen. Terwijl ze door de website navigeert, voegt ze twee paren van de `Throwback Bellbottoms` en één `V-Neck T-Shirt` naar haar kar. Tevreden met haar selecties, beweegt zij zich om uit te checken en haar orde voor te leggen, creërend de volgende ingang op [verkoop vlakke orde lijst](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 2016/09/23 15:41:39 |

* `entity_id` - dit is de primaire sleutel van de `sales_flat_order` tabel.
   * Wanneer Sammy-klant deze bestelling heeft geplaatst en de bovenstaande rij naar de `sales_flat_order` tabel, de volgorde is toegewezen `entity_id` = 227.
* `customer_id` - Deze kolom is de unieke id van de klant die deze specifieke bestelling heeft geplaatst.
   * De `customer_id` aan deze bestelling is gekoppeld, is 214; dit is de `entity_id` op de `customer_entity` tabel.
* `subtotal` - Deze kolom is het totale bedrag dat aan een klant voor de bestelling in rekening wordt gebracht
   * De twee paren &quot;Throwback Bellbottoms&quot; en &quot;V-Neck T-Shirt&quot; kosten in totaal $94,85
* `created_at` - Deze kolom retourneert de tijdstempel voor het tijdstip waarop elke bestelling is gemaakt

## `sales\_flat\_order\_item ( or Sales\_order\_item` als u Commerce 2.0 of hoger hebt)

Naast de enkele rij op de `Sales\_flat\_order` tabel, wanneer `Sammy Customer` verzendt haar orde, een rij voor elk uniek punt in die orde wordt opgenomen in [`sales\_flat\_order\_item` table](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Deze kolom is de primaire sleutel van `sales_flat_order_item` table
   * `Sammy Customer`De bestelling van deze tabel bevat twee regels omdat haar bestelling twee verschillende producten bevat
* `name` - Deze kolom is de naam van het product
* `product_id` - Deze kolom is de unieke identificatie van het product waarnaar deze rij verwijst.
   * De eerste rij hierboven heeft `product_id` = 205 omdat `Throwback Bellbottoms` een `entity_id` van 205 `catalog_product_entity` table
* `order_id` - Deze kolom is de `entity_id` van de orde die deze bijzondere orde punten bevat
   * Beide rijen boven hebben `order_id` = 227 omdat ze beide deel uitmaken van de volgorde geplaatst door `Sammy Customer`, die `entity_id` = 227 op de `sales_flat_order` table
* `qty_ordered` - Deze kolom is het aantal eenheden van het product dat in deze specifieke volgorde is opgenomen
   * `Sammy Customer`s order bevat 2 paren `Throwback Bellbottoms`
* `price` - Deze kolom is de prijs van één eenheid van het orderitem
   * De `subtotal` van `Sammy Customer`s volgorde in de `sales_flat_order` de tabel was 94.85 , de som van 2 paren van `Throwback Bellbottoms` bij $ 39,95 elk en 1 `V-Neck T-Shirt` tegen $ 14,95.
