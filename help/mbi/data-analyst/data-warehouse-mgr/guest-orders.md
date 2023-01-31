---
title: Gastorders
description: Meer informatie over de gevolgen die gastorders hebben voor uw gegevens en over de opties die u op de juiste wijze moet gebruiken voor gastorders in uw [!DNL MBI] data-entrepot.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Gastbestellingen

Als u tijdens het bekijken van uw bestellingen opmerkt dat `customer\_id` waarden zijn null of hebben geen waarde om terug te gaan naar de `customers` tabel, dit is meestal indicatief dat je winkel gastbestellingen toestaat. Dit betekent dat uw `customers` de lijst is zeer waarschijnlijk niet inclusief van al uw klanten.

In dit onderwerp bespreken wij de gevolgen gastorden op uw gegevens hebben en welke opties u behoorlijk voor gastorden in uw moet rekenschap geven [!DNL MBI] data-entrepot.

## Gevolgen van gastorders voor gegevens

In het typische handelsgegevensbestand, is er `orders` tabel die wordt gekoppeld aan een `customers` tabel. Elke rij op de `orders` tabel bevat een `customer\_id` kolom die uniek is voor één rij op de `customers` tabel.

* **Als alle klanten zijn geregistreerd** en gastorders niet zijn toegestaan, betekent dit dat alle records in de `orders` tabel bevat een waarde in het dialoogvenster `customer\_id` kolom. Dientengevolge, sluit elke orde zich aan bij terug naar `customers` tabel. U kunt dit zien in de onderstaande afbeelding.

   ![](../../assets/guest-orders-4.png)

* **Als gastorders zijn toegestaan**, betekent dit dat sommige orders geen waarde hebben in de `customer\_id` kolom. Alleen geregistreerde klanten krijgen een waarde voor de `customer\_id` kolom op de `orders` tabel. Klanten die niet zijn ingeschreven, ontvangen een `NULL` (of leeg) waarde voor deze kolom. Hierdoor hebben niet alle orderrecords in de `customers` tabel.

   >[!NOTE]
   >
   >Om het unieke individu te identificeren dat de orde maakte, moet er een ander uniek gebruikersattribuut naast zijn `customer\_id` aan een bestelling zijn gekoppeld. Het e-mailadres van de klant wordt doorgaans gebruikt.

## Hoe te om gastorden in de opstelling van het gegevenspakhuis rekenschap te geven

Typisch, zal de Ingenieur van de Verkoop die uw rekening uitvoert gastorden in overweging nemen wanneer het bouwen van de stichting van uw gegevenspakhuis.

De meest optimale manier om voor gastorden rekenschap te geven is alle klant-vlakke metriek op het `orders` tabel. Bij deze installatie wordt een unieke klant-id gebruikt die alle klanten hebben, inclusief gasten (doorgaans wordt de e-mail van de klant gebruikt). Hierbij worden de registratiegegevens van de `customers` tabel. Met deze optie worden alleen klanten die ten minste één aankoop hebben gedaan, opgenomen in rapporten op klantniveau. Geregistreerde gebruikers die nog geen aankoop hebben gedaan, worden niet opgenomen. Met deze optie `New customer` metrisch zal op de eerste de ordedatum van de klant in worden gebaseerd `orders` tabel.

U kunt zien dat de `Customers we count` filter dat in dit type opstelling wordt geplaatst heeft een filter voor `Customer's order number = 1`. Laten we eens bedenken waarom dit zo is.

![](../../assets/guest-orders-filter-set.png)

In een situatie zonder gastorden, bestaat elke klant als unieke rij in de klantenlijst (zie Beeld 1). Een metrische waarde zoals `New customers` kan de id van deze tabel eenvoudig tellen op basis van `created\_at` datum om nieuwe klanten te begrijpen op basis van registratiedatum.

In een opstelling van gastorden waar alle klantenmetriek op wordt gebaseerd `orders` lijst aan rekening voor gastorden, moet u ervoor zorgen dat u bent `not counting customers twice`. Als u de id van de tabel met bestellingen telt, telt u elke volgorde. Als u in plaats daarvan de id op de `orders` tabel en een filter gebruiken; `Customer's order number = 1`, dan gaat u elke unieke klant tellen `only one time`. Dit geldt voor alle maatstaven op klantniveau, zoals `Customer's lifetime revenue` of `Customer's lifetime number of orders`.

In bovenstaande afbeelding 2 ziet u dat de waarde null is `customer\_ids` in de `orders` tabel. Als wij de `customer\_email` om unieke klanten te identificeren, kunt u zien dat `erin@test.com` heeft drie (3) bestellingen geplaatst. Daarom kunnen we een `New customers` metrisch op uw `orders` tabel op basis van de volgende voorwaarden:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
