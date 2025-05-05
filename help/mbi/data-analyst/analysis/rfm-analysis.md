---
title: Recente, Frequentie, Monetaire (RFM) Analyse
description: Leer hoe te opstelling een dashboard dat u toestaat om uw klanten door hun recentie, frequentie, en monetaire rankings te segmenteren.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# RFM-analyse

Dit onderwerp toont aan hoe te opstelling een dashboard dat u toestaat om uw klanten door hun recentie, frequentie, en monetaire rankings te segmenteren. De analyse van RFM is een marketing techniek die klantengedrag in overweging neemt om u te helpen segmentatie voor outreach bepalen. Het omvat drie aspecten:

1. Recente periode in hoe recent een klant bij uw winkel heeft gekocht
1. Frequentie in hoe vaak ze van u kopen
1. Monetair in hoeveel de klant besteedt

![](../../assets/blobid0.png)

De RFM-analyse kan alleen worden geconfigureerd als u het [!DNL Adobe Commerce Intelligence] Pro-plan voor de nieuwe architectuur hebt (bijvoorbeeld als u de optie `Data Warehouse Views` onder het menu `Manage Data` hebt). Deze kolommen kunnen worden gemaakt op basis van de pagina **[!DNL Manage Data > Data Warehouse]** . Hieronder vindt u gedetailleerde instructies.

## Aan de slag

U moet eerst een bestand uploaden dat alleen een primaire sleutel met de waarde één bevat. Hierdoor kunnen enkele noodzakelijke berekende kolommen voor de analyse worden gemaakt.

U kunt dit [ artikel ](../importing-data/connecting-data/using-file-uploader.md) en het beeld hieronder gebruiken om uw dossier te formatteren.

## Berekende kolommen

Een verder onderscheid wordt gemaakt als uw zaken gastorden toestaat. Als dat het geval is, kunt u alle stappen voor de tabel `customer_entity` negeren. Als gastorders niet zijn toegestaan, negeert u alle stappen voor de tabel `sales_flat_order` .

Te maken kolommen

* **`Sales_flat_order/customer_entity`** table
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Geselecteerd [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* &#x200B;
       Seconden sinds de laatste ordedatum van de klant 
  * [!UICONTROL Column type] : -     &quot;Zelfde tabel > Leeftijd
* Geselecteerd [!UICONTROL column]: `Customer's last order date`

* (invoer) Verwijzing naar aantal
* [!UICONTROL Column type]: `Same table > Calculation`
* &#x200B;
  [!UICONTROL Inputs]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* **de verwijzings** lijst van de Telling (dit is het dossier u met het aantal &quot;1&quot;uploadde)
* Aantal klanten
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` OR `customer_entity.(input)reference > Count Reference` . `Primary Key`
* Geselecteerd [!UICONTROL column]: `sales_flat_order.customer_email` OR `customer_entity.entity_id`

* **Customer_entity** lijst
* Aantal klanten
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity` .(input) reference > Customer Concentration. `Primary Key`
* Geselecteerd [!UICONTROL column]: `Number of customers`

* (invoer) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Rangschikken op basis van de inkomsten uit de levensduur van de klant
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue` , `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* Monetaire score van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue` , `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* (input) Rangorde volgens het aantal orders in de levensduur van de klant
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Rangschikking volgens het aantal orders in de levensduur van de klant
* &#x200B;
  [!UICONTROL , kolomtype]: – "Zelfde tabel > Berekening"
* [!UICONTROL Inputs]: - **(input) het Rangschikken door het aantal van het klantenleven van orden**, **Aantal klanten**
* [!UICONTROL Calculation]: - **geval wanneer A ongeldig dan ongeldig anders (B- (A-1)) eind** is
* [!UICONTROL Datatype]: - Geheel getal

* Frequentiescore van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders` , `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* Volgorde door seconden sinds laatste de ordedatum van de klant
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Recentiescore van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders` , `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* Recentiescore van de klant (in percentielen)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)` , `Customer's frequency score (by percentiles)` , `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* &#x200B;
  [!UICONTROL Datatype]: String

* **de verwijzing van de Telling** lijst
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` OR `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Geselecteerd [!UICONTROL column]: `sales_flat_order.customer_email` OR `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Niet gelijk aan 000

* **Customer_entity** lijst
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Geselecteerd [!UICONTROL column]: - `Number of customers`

* Recentiescore van de klant `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: - `Customer's recency score (by percentiles)` , `Customer's frequency score (by percentiles)` , `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* (input) Rangschikking volgens de algemene RFM-score van de klant
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Niet gelijk aan 000

* Rangschikking volgens totale RFM-score van de klant
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score` , `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

* RFM-groep van de klant
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue` , `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`

>[!NOTE]
>
>De gebruikte percentielen zijn zelfs splitsingen van klanten (bijvoorbeeld, 20 percentenemmers om 1-5 terug te keren). Als u een aangepaste manier hebt waarop u deze wilt wegen, laat dan de analist weten wanneer u het ticket verzendt.

## Metrisch

Geen nieuwe metriek!

>[!NOTE]
>
>Zorg ervoor om [ alle nieuwe kolommen als afmetingen aan metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

## Rapporten

* **Klanten door groepering RFM**
* Metrisch `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Diagram verbergen
* [!UICONTROL Group by]: `Customer's RFM group`
* &#x200B;
  [!UICONTROL Group door]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Klanten met vijf recentiescore**
* Metrisch `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* Diagram verbergen
* &#x200B;
  [!UICONTROL Group door]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Klanten met één recentiescore**
* Metrisch `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* Diagram verbergen
* &#x200B;
  [!UICONTROL Group door]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan als het bovengenoemde steekproefdashboard kijken, maar de drie geproduceerde lijsten zijn enkel voorbeelden van de types van klantensegmentatie u kunt uitvoeren.
