---
title: Recente, Frequentie, Monetaire (RFM) Analyse
description: Leer hoe te opstelling een dashboard dat u toestaat om uw klanten door hun recentie, frequentie, en monetaire rankings te segmenteren.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# RFM-analyse

In dit artikel ziet u hoe u een dashboard instelt waarmee u uw klanten kunt segmenteren op basis van hun recenentie, frequentie en monetaire waarderingen. De analyse van RFM is een marketing techniek die klantengedrag in overweging neemt om u te helpen segmentatie voor outreach bepalen. Het omvat drie aspecten:

* Recente periode in hoe recent een klant bij uw winkel heeft gekocht
* Frequentie in hoe vaak ze van u kopen
* Monetair in hoeveel de klant besteedt

![](../../assets/blobid0.png)

De RFM-analyse kan alleen worden geconfigureerd als u beschikt over [!DNL MBI] Pro-abonnement op de nieuwe architectuur (bijvoorbeeld als u de optie &quot;Weergaven Data Warehouse&quot; onder het menu &quot;Gegevens beheren&quot; hebt). Deze kolommen kunnen worden gemaakt op de pagina &quot;Gegevens beheren > Data Warehouse&quot;. Nadere instructies worden hieronder gegeven.

## Aan de slag

U moet eerst een bestand uploaden dat alleen een primaire sleutel met de waarde één bevat. Hierdoor kunnen enkele noodzakelijke berekende kolommen voor de analyse worden gemaakt.

U kunt dit [Help Center-artikel](../importing-data/connecting-data/using-file-uploader.md) en de afbeelding hieronder om het bestand op te maken.

## Berekende kolommen

Een verder onderscheid wordt gemaakt als uw zaken gastorden toestaat. Als dat het geval is, kunt u alle stappen voor de `customer_entity` tabel. Als gastorden niet worden toegestaan, negeer alle stappen voor `sales_flat_order` tabel.

Te maken kolommen

* **`Sales_flat_order/customer_entity`** table
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Geselecteerd [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       Seconden sinds laatste besteldatum van klant
   * [!UICONTROL Column type]: - &quot;Zelfde tabel > Leeftijd
* Geselecteerd [!UICONTROL column]: `Customer's last order date`

* (invoer) Verwijzing naar aantal
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL Inputs]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [!UICONTROL Datatype]: `Integer`

* **Telreferentie** tabel (dit is het bestand dat u hebt geüpload met het nummer &quot;1&quot;)
* Aantal klanten
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` OF `customer_entity.(input)reference > Count Reference`. `Primary Key`
* Geselecteerd [!UICONTROL column]: `sales_flat_order.customer_email` OF `customer_entity.entity_id`

* **Klant_entiteit** table
* Aantal klanten
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(input) reference > Customer Concentration. `Primary Key`
* Geselecteerd [!UICONTROL column]: `Number of customers`

* (invoer) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Rangschikken op basis van de inkomsten uit de levensduur van de klant
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL Datatype]: `Integer`

* Monetaire score van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL Datatype]: `Integer`

* (input) Rangorde volgens het aantal orders in de levensduur van de klant
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Rangschikking volgens levensduur van klant aantal orders
* 
   [!UICONTROL, kolomtype]: – "Zelfde tabel > Berekening"
* [!UICONTROL Inputs]: - **(input) Rangorde volgens het aantal orders in de levensduur van de klant**, **Aantal klanten**
* [!UICONTROL Calculation]: - **case als A null is, dan null else (B-(A-1)) end**
* [!UICONTROL Datatype]: - Geheel getal

* Frequentiescore van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL Datatype]: `Integer`

* Volgorde door seconden sinds laatste de ordedatum van de klant
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Recentiescore van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL Datatype]: `Integer`

* Recentiescore van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [!UICONTROL Datatype]: String

* **Telreferentie** table
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` OF `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Geselecteerd [!UICONTROL column]: `sales_flat_order.customer_email` OF `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Niet gelijk aan 000

* **Klant_entiteit** table
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Geselecteerd [!UICONTROL column]: - `Number of customers`

* Recentiescore van de klant `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [!UICONTROL Datatype]: `Integer`

* (input) Rangschikking op basis van de totale RFM-score van de klant
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Niet gelijk aan 000

* Rangschikking op basis van de totale RFM-score van de klant
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL Datatype]: `Integer`

* RFM-groep van de klant
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [!UICONTROL Datatype]: `Integer`

>[!NOTE]
>
>De gebruikte percentielen zijn zelfs splitsingen van klanten (bijvoorbeeld, 20% emmers om 1-5 terug te keren). Als u een aangepaste manier hebt waarop u deze wilt wegen, laat dan de analist weten wanneer u het ticket verzendt.

## Metrisch

Geen nieuwe metriek!

**Opmerking**: Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Rapporten

* **Klanten per RFM-groep**
* Metrisch `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Diagram verbergen
* [!UICONTROL Group by]: `Customer's RFM group`
* 
   [!UICONTROL Group door]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Klanten met vijf recentiescore**
* Metrisch `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* Diagram verbergen
* 
   [!UICONTROL Group door]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **Klanten met één recentiescore**
* Metrisch `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* Diagram verbergen
* 
   [!UICONTROL Group door]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan als het bovengenoemde steekproefdashboard kijken, maar de drie geproduceerde lijsten zijn enkel voorbeelden van de types van klantensegmentatie u kunt uitvoeren.
