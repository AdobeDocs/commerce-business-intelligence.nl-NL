---
title: Gastorders
description: Meer informatie over de gevolgen die gastorders hebben voor uw gegevens en over de opties die u op de juiste wijze moet gebruiken voor gastorders in uw [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Gastbestellingen

Als u tijdens het bekijken van uw bestellingen opmerkt dat `customer\_id` waarden zijn null of hebben geen waarde om terug te gaan naar de `customers` tabel, dit is een indicatie dat je winkel gastbestellingen toestaat. Dit betekent dat uw `customers` de lijst is zeer waarschijnlijk niet inclusief van al uw klanten.

Dit onderwerp bespreekt de gevolgen gastorden op uw gegevens hebben en welke opties u van gastorden in uw moet behoorlijk rekenschap geven [!DNL Commerce Intelligence] Data Warehouse.

## Gevolgen van gastorders voor gegevens

In het typische handelsgegevensbestand, is er `orders` tabel die wordt gekoppeld aan een `customers` tabel. Elke rij op de `orders` tabel bevat een `customer\_id` kolom die uniek is voor één rij op de `customers` tabel.

* **Als alle klanten zijn geregistreerd** en gastorders niet zijn toegestaan, betekent dit dat alle records in de `orders` tabel bevat een waarde in het dialoogvenster `customer\_id` kolom. Dientengevolge, sluit elke orde zich aan bij terug naar `customers` tabel.

  ![](../../assets/guest-orders-4.png)

* **Als gastorders zijn toegestaan**, betekent dit dat sommige orders geen waarde hebben in de `customer\_id` kolom. Alleen geregistreerde klanten krijgen een waarde voor de `customer\_id` kolom op de `orders` tabel. Klanten die niet zijn ingeschreven, ontvangen een `NULL` (of leeg) waarde voor deze kolom. Hierdoor hebben niet alle orderrecords overeenkomende records in de `customers` tabel.

  >[!NOTE]
  >
  >Om het unieke individu te identificeren dat de orde maakte, moet er een ander uniek gebruikersattribuut naast zijn `customer\_id` aan een bestelling zijn gekoppeld. Het e-mailadres van de klant wordt doorgaans gebruikt.

## Hoe te om gastorden in de opstelling van de Data Warehouse rekenschap te geven

Typisch, neemt de Ingenieur van de Verkoop die uw rekening uitvoert gastorden in overweging wanneer het bouwen van de stichting van uw Data Warehouse.

De meest optimale manier om voor gastorden rekenschap te geven is alle klant-vlakke metriek op het `orders` tabel. Bij deze installatie wordt een unieke klant-id gebruikt die alle klanten hebben, inclusief gasten (doorgaans wordt de e-mail van de klant gebruikt). Hierbij worden de registratiegegevens van de `customers` tabel. Met deze optie worden alleen klanten die minstens één aankoop hebben gedaan opgenomen in rapporten op klantniveau. Geregistreerde gebruikers die nog geen aankoop hebben gedaan, worden niet opgenomen. Met deze optie `New customer` metrisch is gebaseerd op de eerste de ordedatum van de klant in `orders` tabel.

U kunt zien dat de `Customers we count` filter dat in dit type opstelling wordt geplaatst heeft een filter voor `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

In een situatie zonder gastorden, bestaat elke klant als unieke rij in de klantenlijst (zie Beeld 1). Een metrische waarde zoals `New customers` kan de id van deze tabel eenvoudig tellen op basis van `created\_at` datum om nieuwe klanten te begrijpen op basis van registratiedatum.

In een opstelling van gastorden waar alle klantenmetriek op wordt gebaseerd `orders` tabel ter verantwoording van gastorders, moet u ervoor zorgen dat u `not counting customers twice`. Als u de id van de tabel met bestellingen telt, telt u elke volgorde. Als u in plaats daarvan de id op de `orders` tabel en een filter gebruiken; `Customer's order number = 1`, dan gaat u elke unieke klant tellen `only one time`. Dit geldt voor alle maatstaven op klantniveau, zoals `Customer's lifetime revenue` of `Customer's lifetime number of orders`.

U kunt hierboven zien dat er null is `customer\_ids` in de `orders` tabel. Als u het `customer\_email` om unieke klanten te identificeren, kunt u zien dat `erin@test.com` heeft drie (3) bestellingen geplaatst. Daarom kunt u een `New customers` metrisch op uw `orders` tabel op basis van de volgende voorwaarden:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
