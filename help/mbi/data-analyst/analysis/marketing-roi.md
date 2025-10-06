---
title: Marketing ROI
description: Leer hoe u een dashboard instelt dat uw kanaalanalyse bijhoudt - inclusief ROI in geaggregeerde vorm en per campagne.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Marketing ROI

>[!NOTE]
>
>Dit onderwerp bevat instructies voor cliënten die de originele architectuur en de nieuwe architectuur gebruiken. U bent op de [&#x200B; nieuwe architectuur &#x200B;](../../administrator/account-management/new-architecture.md) als u de &quot;sectie van de Mening van Data Warehouse&quot;beschikbaar na het selecteren van &quot;Gegevens&quot;van de belangrijkste toolbar hebt.

Als u geld uitgeeft aan online reclame, wilt u uw rendement op dit geld volgen en gegevensgedreven besluiten over verdere investeringen nemen. Dit onderwerp toont hoe te opstelling een dashboard dat uw kanaalanalyse - met inbegrip van ROI in bijeengevoegde en door campagne volgt.

![&#x200B; Marketing dashboard die de metriek van ROI en campagneprestaties tonen &#x200B;](../../assets/Marketing_dashboard_example.png)

Voordat u aan de slag gaat, wilt u eerst verbinding maken met uw [[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md) -, [[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md) - en [[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md) -accounts en aanvullende online gegevens plaatsen en doorgeven. Deze analyse bevat [&#x200B; geavanceerde berekende kolommen &#x200B;](../data-warehouse-mgr/adv-calc-columns.md).

## Geconsolideerde tabellen

**Oorspronkelijke architectuur:** om uw uitgaven van diverse bronnen, zoals [!DNL Facebook Ads] of [!DNL Google Adwords] te verenigen, adviseert Adobe het creëren van a **geconsolideerde lijst** van elk van uw advertentie uitgeven. U hebt een analist nodig om deze stap voor u te voltooien. Als u niet, [&#x200B; dossier een steunverzoek &#x200B;](../../guide-overview.md#Submitting-a-Support-Ticket) met het onderwerp `[MARKETING ROI ANALYSIS]` hebt, en een analist leidt tot deze lijst.

**Nieuwe architectuur:** u kunt het voorbeeld in [&#x200B; volgen dit onderwerp van de Bibliotheek van de Analyse &#x200B;](../../data-analyst/data-warehouse-mgr/create-dw-views.md). Geconsolideerde tabellen worden nu Data Warehouse Views on the new architectuur genoemd.

## Berekende kolommen

Te maken kolommen

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** wordt gecreeerd door een analist van Adobe als deel van uw **[MARKETING ROI ANALYSE]** kaartje

**Oorspronkelijke en nieuwe architecturen:**

* **`sales_flat_order`** table
   * **`Order's GA campaign`**
      * Selecteer een definitie: `Joined Column`
      * [!UICONTROL Create Path]:
      * &#x200B;
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * &#x200B;
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * Selecteer een [!UICONTROL table]: `ecommerce####`
      * Selecteer een [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * Selecteer een definitie: Samengevoegde kolom
      * Selecteer een [!UICONTROL table]: `ecommerce####`
      * Selecteer een [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = e-commerce####.transactionId

   * **`Order's GA source`**
      * Selecteer een definitie: Samengevoegde kolom
      * Selecteer een [!UICONTROL table]: `ecommerce####`
      * Selecteer een [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = e-commerce####.transactionId
^

* **`customer_entity`** table
* **`Customer's first order GA campaign`**
   * Selecteer een definitie: `Max`
   * Selecteer een [!UICONTROL table]: `sales_flat_order`
   * Selecteer een [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Selecteer een definitie: `Max`
   * Selecteer een [!UICONTROL table]: `sales_flat_order`
   * Selecteer een [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: verkoop_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Selecteer een definitie: `Max`
   * Selecteer een [!UICONTROL table]: `sales_flat_order`
   * Selecteer een [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** table
* **`Customer's first order GA campaign`**
   * Selecteer een definitie: `Joined Column`
   * Selecteer een [!UICONTROL table]: `customer_entity`
   * Selecteer een [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Selecteer een definitie: Samengevoegde kolom
   * Selecteer een [!UICONTROL table]: `customer_entity`
   * Selecteer een [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Selecteer een definitie: `Joined Column`
   * Selecteer een [!UICONTROL table]: `customer_entity`
   * Selecteer een [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Metrisch

* **uitgeeft de Advertentie**
* In de tabel **`Consolidated Digital Ad Spend`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`adCost`**
* Besteld door de **`date`** timestamp

* **toevoegt impressies**
* In de tabel **`Consolidated Digital Ad Spend`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`Impressions`**
* Besteld door de **`Month`** timestamp

* **Advertentie klikt**
* In de tabel **`Consolidated Digital Ad Spend`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`adClicks`**
* Besteld door de **`Month`** timestamp

>[!NOTE]
>
>Zorg ervoor om [&#x200B; alle nieuwe kolommen als afmetingen aan metriek &#x200B;](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

## Rapporten

* **besteedt de Advertentie (alle tijd)**
   * [!UICONTROL Metric]: extra uitgaven

* Metrisch `A`: Advertentie-uitgaven
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Add klantenverwervingen (allen tijd)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogica: ([`A`] OR [`B`] OR [`C`]) EN [`D`]

* Metrisch `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Add ROI**
   * [!UICONTROL Metric]: extra uitgaven

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogica: ([`A`] OR [`B`] OR [`C`]) EN [`D`]

   * [!UICONTROL Metric]: gemiddelde inkomsten tijdens de levensduur
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogica: ([`A`] OR [`B`] OR [`C`]) EN [`D`]

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

* Metrisch `A`: `Ad Spend (hide)`
* Metrisch `B`: `Ad customer acquisitions (hide)`
* Metrisch `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Orders door gummiddel**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`

* Metrisch `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]: `Area`

* **ROI van de Advertentie door campagne**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogica: ([`A`] OR [`B`] OR [`C`]) EN [`D`]

   * [!UICONTROL Metric]: gemiddelde inkomsten tijdens de levensduur
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogica: ([`A`] OR [`B`] OR [`C`]) EN [`D`]

   * [!UICONTROL Metric]: Gemiddeld aantal bestellingen tijdens de levensduur
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogica: ([`A`] OR [`B`] OR [`C`]) EN [`D`]

   * [!UICONTROL Formula]: `(A / B)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

* Metrisch `A`: `Ad Spend` (hide)
* Metrisch `B`: `Ad customer acquisitions`
* Metrisch `C`: `Average LTV`
* Metrisch `D`: `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL -formule]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Metrisch `H`: `adClicks`
* Metrisch `I`: `Impressions`
* &#x200B;
  [!UICONTROL -formule]: `CTR`
* &#x200B;
  [!UICONTROL -formule]: `CPC`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Group door]: `campaign` (Gebruik de campagne &#39;First Order&#39; van de Klant voor niet-ad-uitgaventabelgegevens)
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

Als u in om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten in dienst willen nemen, [&#x200B; contactsteun &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Verwante

* [Best-practices voor UTM-codering in  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Hoe werkt  [!DNL Google Analytics]  UTM attributie?](../analysis/utm-attributes.md)
