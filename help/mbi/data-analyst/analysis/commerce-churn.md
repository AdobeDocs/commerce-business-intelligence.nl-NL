---
title: Commerce Churn
description: Leer hoe u de Koopprijs genereert en analyseert.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Wisselfrequentie

Dit onderwerp demonstreert hoe u een **kromtrekken** voor uw **handelsklanten**. In tegenstelling tot SaaS of traditionele abonnementsbedrijven hebben commerciële klanten gewoonlijk geen beton **&quot;churn event&quot;** om u te tonen dat zij niet meer aan uw actieve klanten zouden moeten tellen. Daarom kunt u met de onderstaande instructies een klant definiëren als &#39;afgewaardeerd&#39; op basis van een bepaalde hoeveelheid tijd die is verstreken sinds de laatste bestelling.

![](../../assets/Churn_rate_image.png)

Veel klanten willen hulp bij het conceptualiseren van wat **tijdframe** zij moeten op basis van hun gegevens gebruiken . Als u historisch klantengedrag wilt gebruiken om dit te bepalen **churn timeframe**, kan het zijn dat u zich vertrouwd wilt maken met de [churn definiëren](../analysis/define-cust-churn.md) onderwerp. Vervolgens kunt u de resultaten in de formule voor de kleurfrequentie in de onderstaande instructies gebruiken.

## Berekende kolommen

Te maken kolommen

* **`customer_entity`** table
* **`Customer's last order date`**
   * Selecteer een [!UICONTROL definition]: `Max`
   * Selecteren [!UICONTROL table]: `sales_flat_order`
   * Selecteren [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Selecteer een [!UICONTROL definition]: `Age`
   * Selecteren [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Metrisch

* **Nieuwe klanten (op eerste besteldatum)**
   * Klanten die worden geteld

>[!NOTE]
>
>Deze maatstaf kan op uw account bestaan.

* In de **`customer_entity`** table
* Deze maatstaf voert een **Aantal**
* Op de **`entity_id`** kolom
* Besteld door de **`Customer's first order date`** tijdstempel
* [!UICONTROL Filter]:

* **Nieuwe klanten (op laatste besteldatum)**
   * Klanten die worden geteld

  >[!NOTE]
  >
  >Deze maatstaf kan op uw account bestaan.

* In de **`customer_entity`** table
* Deze maatstaf voert een **Aantal**
* Op de **`entity_id`** kolom
* Besteld door de **`Customer's last order date`** tijdstempel
* [!UICONTROL Filter]:

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Rapporten

* **Wisselfrequentie**
   * [!UICONTROL Metric]: Nieuwe klanten (op eerste besteldatum)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Seconden sinds laatste besteldatum van klant >= [Uw zelf-bepaalde grens voor gekochte klanten ]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 
     [!UICONTROL Format]: Percentage

* *Metrisch `A`:`New customers cumulative`*
* *Metrisch `B`:`Churned customers by last order date`*
* *Metrisch `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Hieronder vindt u een aantal gangbare conversies voor maanden > seconden, maar google biedt andere waarden, waaronder conversies in week > seconden voor aangepaste waarden die u zoekt.

| **Maanden** | **Seconden** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan er als het bovenstaande voorbeelddashboard uitzien.
