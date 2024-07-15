---
title: Gegevens van eCommerce opmaken en importeren
description: Leer de ideale gegevensindelingen voor het uploaden van eCommerce-gegevens.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Gegevens opmaken en importeren

Als u een integratie gebruikt die momenteel niet door [!DNL Adobe Commerce Intelligence] wordt gesteund, kunt u nog het [ Dossier gebruiken uploadt eigenschap ](using-file-uploader.md) om uw gegevens in uw Data Warehouse te krijgen. Dit onderwerp behandelt de ideale gegevensformaten die voor het uploaden van elektronische handelsgegevens moeten worden gebruikt.

## `Orders` table

De tabel `orders` moet één rij bevatten voor elke transactie die het bedrijf heeft uitgevoerd. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Order ID` | De volgorde-id moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de primaire sleutel voor de tabel. |
| `Customer` | De klant die de bestelling heeft geplaatst. |
| `Order total` | Het totaal van de bestelling. Dit kan een op berekening gebaseerde kolom zijn, waarbij waarden in andere kolommen - zoals subtotaal en verzendkosten - het totaal voor deze kolom vormen. |
| `Currency` | De valuta waarin de bestelling is betaald. Vermeld indien van toepassing. |
| ` Order status` | De status van de volgorde, zoals `In Progress` , `Refunded` of `Complete` . De waarde van deze kolom verandert (als niet volledig). De nieuwe en bijgewerkte gegevens kunnen worden ingevoerd gebruikend [ voegt de eigenschap van Gegevens ](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) op de `File Uploads` pagina toe. |
| `Acquisition/marketing channel` | Het aankoop- of marketingkanaal waar de klant die de order heeft geplaatst, naar werd verwezen. |
| `Order datetime` | De datum en tijd waarop de order is gemaakt. |
| `Order updated at` | De datum en het tijdstip waarop de laatste wijziging in de orderrecord is aangebracht. |

{style="table-layout:auto"}

## `Order detail/items` table {#itemstable}

De tabel `order_detail / items` moet één rij bevatten voor elk afzonderlijk item in elke volgorde. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Order item ID` | De id van het orderitem moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de `primary key` voor de tabel. |
| `Order ID` | De id van de bestelling. |
| `Product ID` | De id van het product. |
| `Product name` | De naam van het product. |
| `Product's unit price` | De prijs voor één eenheid van het product. |
| `Quantity` | De hoeveelheid product in de bestelling. |

## `Customers` table {#customerstable}

De tabel `customers` moet één rij bevatten voor elke klantenaccount. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Customer ID` | De klant-id moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de primaire sleutel voor de tabel. |
| `Customer created at` | De datum en tijd waarop de account van de klant is gemaakt. |
| `Customer modified at` | De datum en tijd waarop de account van de klant voor het laatst is gewijzigd. |
| `Acquisition/marketing channel source` | Het aankoop- of marketingkanaal waar de klant naar verwees. |
| `Demographic info` | Demografische gegevens zoals leeftijd en geslacht kunnen worden gebruikt om uw rapporten te segmenteren. |
| `Acquisition/marketing channel` | Het aankoop- of marketingkanaal waar de klant die de order heeft geplaatst, naar werd verwezen. |

## `Subscription payments` table

De tabel `subscriptions` moet één rij bevatten voor elke abonnementsbetaling. Mogelijke kolommen zijn:

| Kolomnaam | Beschrijving |
|----|----|
| `Subscription ID` | De abonnement-id moet uniek zijn voor elke rij in de tabel. Dit is doorgaans ook de primaire sleutel voor de tabel. |
| `Customer ID` | De id van de klant die de betaling heeft verricht. |
| `Payment amount` | Het bedrag van de abonnementsbetaling. |
| `Start date` | De begindatum van de periode waarop de betaling betrekking heeft. |
| `End date` | De einddatum van de periode waarop de betaling betrekking heeft. |
