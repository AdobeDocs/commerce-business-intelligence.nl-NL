---
title: Gegevens van eCommerce opmaken en importeren
description: Leer de ideale gegevensindelingen voor het uploaden van eCommerce-gegevens.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Gegevens opmaken en importeren

Als u een integratie gebruikt die momenteel niet door wordt gesteund [!DNL MBI]kunt u de [Bestanden uploaden, functie](using-file-uploader.md) om uw gegevens in uw Data Warehouse te krijgen. In dit artikel worden de ideale gegevensindelingen beschreven voor het uploaden van eCommerce-gegevens.

## `Orders` table

De `orders` de tabel moet één rij bevatten voor elke transactie die de onderneming heeft uitgevoerd. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Order ID` | De volgorde-id moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de primaire sleutel voor de tabel. |
| `Customer` | De klant die de bestelling heeft geplaatst. |
| `Order total` | Het totaal van de bestelling. Dit kan een op berekening gebaseerde kolom zijn, waarbij waarden in andere kolommen - zoals subtotaal en verzendkosten - het totaal voor deze kolom vormen. |
| `Currency` | De valuta waarin de bestelling is betaald. Vermeld indien van toepassing. |
| ` Order status` | De status van de order, zoals `In Progress`, `Refunded`, of `Complete`. De waarde van deze kolom verandert (als niet volledig). Nieuwe en bijgewerkte gegevens kunnen worden geïmporteerd met de opdracht [Gegevensfunctie toevoegen](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) op de `File Uploads` pagina. |
| `Acquisition/marketing channel` | Het aankoop- of marketingkanaal waar de klant die de order heeft geplaatst, naar werd verwezen. |
| `Order datetime` | De datum en tijd waarop de order is gemaakt. |
| `Order updated at` | De datum en het tijdstip waarop de laatste wijziging in de orderrecord is aangebracht. |

{style="table-layout:auto"}

## `Order detail/items` table {#itemstable}

De `order_detail / items` de lijst zou één rij voor elk verschillend punt in elke orde moeten bevatten. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Order item ID` | De id van het orderitem moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de `primary key` voor de tabel. |
| `Order ID` | De id van de bestelling. |
| `Product ID` | De id van het product. |
| `Product name` | De naam van het product. |
| `Product's unit price` | De prijs voor één eenheid van het product. |
| `Quantity` | De hoeveelheid van het product in de bestelling. |

## `Customers` table {#customerstable}

De `customers` de lijst zou één rij voor elke klantenrekening moeten bevatten. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Customer ID` | De klant-id moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de primaire sleutel voor de tabel. |
| `Customer created at` | De datum en tijd waarop de account van de klant is gemaakt. |
| `Customer modified at` | De datum en tijd waarop de account van de klant voor het laatst is gewijzigd. |
| `Acquisition/marketing channel source` | Het aankoop- of marketingkanaal waar de klant naar verwees. |
| `Demographic info` | Demografische gegevens zoals leeftijd en geslacht kunnen worden gebruikt om uw rapporten te segmenteren. |
| `Acquisition/marketing channel` | Het aankoop- of marketingkanaal waar de klant die de order heeft geplaatst, naar werd verwezen. |

## `Subscription payments` table

De `subscriptions` de tabel moet één rij bevatten voor elke abonnementsbetaling. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Subscription ID` | De abonnement-id moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de primaire sleutel voor de tabel. |
| `Customer ID` | De id van de klant die de betaling heeft verricht. |
| `Payment amount` | Het bedrag van de abonnementsbetaling. |
| `Start date` | De begindatum van de periode waarop de betaling betrekking heeft. |
| `End date` | De einddatum van de periode waarop de betaling betrekking heeft. |
