---
title: Gastorders
description: Leer over de gevolgen gastorden op uw gegevens hebben en welke opties u van gastorden in uw  [!DNL Commerce Intelligence]  Data Warehouse behoorlijk moet rekenschap geven.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Gastbestellingen

Als u tijdens het controleren van uw bestellingen opmerkt dat veel `customer\_id` -waarden null zijn of geen waarde hebben om weer deel te nemen aan de `customers` -tabel, is dit een indicatie dat in uw winkel bestellingen van gasten zijn toegestaan. Dit betekent dat uw `customers` tabel hoogstwaarschijnlijk niet voor al uw klanten inclusief is.

Dit onderwerp bespreekt de invloed gastorden op uw gegevens hebben en welke opties u behoorlijk voor gastorden in uw [!DNL Commerce Intelligence] Data Warehouse moet rekenschap geven.

## Gevolgen van gastorders voor gegevens

In de standaard commerciële database is er een `orders` -tabel die zich bij een `customers` -tabel aansluit. Elke rij in de tabel `orders` heeft een kolom `customer\_id` die uniek is voor één rij in de tabel `customers` .

* **als alle klanten** worden geregistreerd en gastorden niet worden toegestaan, betekent dit dat elk verslag in de `orders` lijst een waarde in de `customer\_id` kolom heeft. Hierdoor wordt elke volgorde weer gekoppeld aan de tabel `customers` .

  ![](../../assets/guest-orders-4.png)

* **als de gastorden** worden toegestaan, betekent dit dat sommige orden geen waarde in de `customer\_id` kolom hebben. Alleen geregistreerde klanten krijgen een waarde voor de kolom `customer\_id` in de tabel `orders` . Klanten die niet zijn geregistreerd, ontvangen een `NULL` (of lege) waarde voor deze kolom. Hierdoor hebben niet alle orderrecords overeenkomende records in de tabel `customers` .

  >[!NOTE]
  >
  >Om het unieke individu te identificeren dat de orde maakte, moet er een ander uniek gebruikersattribuut naast `customer\_id` in bijlage aan een orde zijn. Het e-mailadres van de klant wordt doorgaans gebruikt.

## Hoe te om gastorden in de opstelling van de Data Warehouse rekenschap te geven

Typisch, neemt de Ingenieur van de Verkoop die uw rekening uitvoert gastorden in overweging wanneer het bouwen van de stichting van uw Data Warehouse.

De meest optimale manier om voor gastorden rekening te houden is alle klant-vlakke metriek op de `orders` lijst te baseren. Bij deze installatie wordt een unieke klant-id gebruikt die alle klanten hebben, inclusief gasten (doorgaans wordt de e-mail van de klant gebruikt). Hierbij worden registratiegegevens uit de tabel `customers` genegeerd. Met deze optie worden alleen klanten die ten minste één aankoop hebben gedaan, opgenomen in rapporten op klantniveau. Geregistreerde gebruikers die nog geen aankoop hebben gedaan, worden niet opgenomen. Met deze optie is de maatstaf van `New customer` gebaseerd op de eerste besteldatum van de klant in de `orders` -tabel.

Het kan zijn dat het filter `Customers we count` dat in dit type instelling is ingesteld, een filter heeft voor `Customer's order number = 1` .

![](../../assets/guest-orders-filter-set.png)

In een situatie zonder gastorden, bestaat elke klant als unieke rij in de klantenlijst (zie Beeld 1). Een metrische waarde zoals `New customers` kan eenvoudig de id van deze tabel tellen op basis van `created\_at` -datum om te begrijpen dat nieuwe klanten op basis van de registratiedatum worden benaderd.

In een opstelling van gastorden waar alle klantenmetriek op de `orders` lijst om voor gastorden gebaseerd zijn, moet u ervoor zorgen dat u `not counting customers twice` bent. Als u de id van de tabel met bestellingen telt, telt u elke volgorde. Als u in plaats daarvan de id op de `orders` -tabel telt en een filter gebruikt, `Customer's order number = 1` , telt u elke unieke klant `only one time` . Dit is van toepassing op alle maatstaven op klantniveau, zoals `Customer's lifetime revenue` of `Customer's lifetime number of orders` .

Hierboven ziet u de waarde null `customer\_ids` in de tabel `orders` . Als u `customer\_email` gebruikt om unieke klanten te identificeren, ziet u dat `erin@test.com` drie (3) bestellingen heeft geplaatst. Daarom kunt u op basis van de volgende voorwaarden een `New customers` -metrische waarde maken voor de `orders` -tabel:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
