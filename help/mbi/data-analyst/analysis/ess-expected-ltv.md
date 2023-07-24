---
title: Analyse van de verwachte levenwaarde (LTV) (basis)
description: Leer hoe u analyses maakt om de levensduurwaarde van uw huidige klanten te begrijpen en hoe de levensduurwaarde met meer bestellingen toeneemt.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Verwachte Lifetime-waardeanalyse

Het voorspellen van de levenwaarde van klanten aangezien zij meer orden plaatsen is één van de belangrijkste aspecten van om het even welke zaken van om het even welke grootte.

Hieronder vindt u de stappen voor het maken van analyses om de levensduurwaarde van uw huidige klanten te begrijpen en te voorspellen hoe de levensduurwaarde met meer bestellingen toeneemt.

![verwachte levenwaarde](../../assets/expected_ltv_720.png)

## Een metrisch object maken

De eerste stap bestaat uit het samenstellen van een nieuwe metrische code met de volgende stappen:
* Navigeren naar **[!UICONTROL Manage Data > Metrics]**
   * Bestaande weergeven **[!UICONTROL Avg lifetime revenue]**.

  >[!NOTE]
  >
  >De lijst deze metrisch wordt geconstrueerd (waarschijnlijk `customer_entity` of `sales_order` afhankelijk van de mogelijkheid van je winkel om uitchecken door gasten te accepteren.)

   * Klikken **[!UICONTROL Create New Metric]** en selecteer de tabel hierboven.
   * Deze maatstaf voert een **Mediaan** op de `Customer's lifetime revenue` kolom, geordend door `created_at`.
      * [!UICONTROL Filters]:
         * Voeg de `Customers we count (Saved Filter Set)` (of `Registered accounts we count`)

   * Geef metrisch een naam, zoals `Median lifetime revenue`.

## Het dashboard maken

Zodra metrisch is gecreeerd, kunt u **een dashboard maken** door dit te doen :
* Navigeren naar **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Geef het dashboard een naam, zoals `Expected LTV`.

* Hier maakt u alle rapporten en voegt u deze toe.

## Rapporten samenstellen

>[!NOTE]
>
>Aan **[!UICONTROL Time Period:]** wordt de termijn voor elk verslag als volgt vermeld: `All-time`. U kunt dit aanpassen aan uw analysebehoeften. Adobe raadt alle rapporten op dit dashboard aan dezelfde periode te bestrijken, zoals `All time`, `Year-to-date`, of `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Toevoegen [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Niet gelijk aan** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Groter dan**`0`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * Metrisch `1`: `Avg lifetime revenue`
   * Metrisch `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
     [!UICONTROL Chart Type]: `Line`
   * Uitschakelen `Multiple Y-Axes`

* **LTV op levensduuraantal orders**
   * Metrisch `1`: `Avg lifetime revenue`
   * Metrisch `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 
     [!UICONTROL Chart Type]: `Line`

  >[!NOTE]
  >
  >Niet alle waarden toevoegen voor `Customer's lifetime number of orders`. In plaats daarvan, bekijk een punt waar het aantal Nieuwe Klanten een klein aantal bereikt en manueel het levenslevensaantal van elke Klant van ordewaarde aan dat punt toevoegen. Bijvoorbeeld, als er 200 klanten bij één orde zijn, 75 bij twee, 15 bij drie, en 3 bij vier, voeg toe *1, 2 en 3*.

* Bestaande toevoegen [!UICONTROL Avg customer lifetime revenue by cohort] verslag.

Na het bouwen van de rapporten, verwijs naar het beeld bij de bovenkant van dit onderwerp voor hoe u de rapporten op uw dashboard kunt organiseren.
