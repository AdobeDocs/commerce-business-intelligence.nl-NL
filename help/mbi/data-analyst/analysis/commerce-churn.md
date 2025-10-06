---
title: Commerce Churn
description: Leer hoe u uw Commerce-wisselkoers kunt genereren en analyseren.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# Wisselfrequentie

Dit onderwerp toont aan hoe te om het tarief van de a **kurn** voor uw **commerciële klanten** te berekenen. In tegenstelling tot SaaS of traditionele abonnementsbedrijven, hebben de handelklanten typisch geen concrete **&quot;koordgebeurtenis&quot;** om u te tonen dat zij niet meer op uw actieve klanten zouden moeten tellen. Daarom kunt u met de onderstaande instructies een klant definiëren als &#39;afgewaardeerd&#39; op basis van een bepaalde hoeveelheid tijd die is verstreken sinds de laatste bestelling.

![ de tariefvisualisatie die van de Churn klantenbehoud in tijd toont ](../../assets/Churn_rate_image.png)

Vele klanten willen hulp in beginnen te conceptualiseren wat **timeframe** zij zouden moeten gebruiken gebaseerd op hun gegevens. Als u historisch klantengedrag wilt gebruiken om dit **koele timeframe** te bepalen, kunt u zich met [ willen vertrouwd maken bepalend koor ](../analysis/define-cust-churn.md) onderwerp. Vervolgens kunt u de resultaten in de formule voor de kleurfrequentie in de onderstaande instructies gebruiken.

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
>Zorg ervoor om [ alle nieuwe kolommen als afmetingen aan metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

## Metrisch

* **Nieuwe klanten (door eerste ordedatum)**
   * Klanten die worden geteld

>[!NOTE]
>
>Deze maatstaf kan op uw account bestaan.

* In de tabel **`customer_entity`**
* Deze metrisch voert a **Telling** uit
* Op de kolom **`entity_id`**
* Besteld door de **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **Nieuwe klanten (door laatste ordedatum)**
   * Klanten die worden geteld

  >[!NOTE]
  >
  >Deze maatstaf kan op uw account bestaan.

* In de tabel **`customer_entity`**
* Deze metrisch voert a **Telling** uit
* Op de kolom **`entity_id`**
* Besteld door de **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Zorg ervoor om [ alle nieuwe kolommen als afmetingen aan metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

## Rapporten

* **Tarief van de Knevel**
   * [!UICONTROL Metric]: Nieuwe klanten (op eerste besteldatum)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Seconden sinds laatste de ordedatum van de klant >= [ Uw zelf-bepaalde grens voor gekochte klanten ]**`^`**
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
| 3 | 7.776.000 |
| 6 | 15.552.000 |
| 9 | 23.328.000 |
| 12 | 31.104.000 |

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan er als het bovenstaande voorbeelddashboard uitzien.
