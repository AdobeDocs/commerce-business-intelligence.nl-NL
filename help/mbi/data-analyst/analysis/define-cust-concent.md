---
title: Concentratie van klanten definiëren
description: Leer hoe te opstelling een dashboard dat u helpt meten hoe de totale opbrengst onder uw klantenbasis wordt verdeeld.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Klantenconcentratie

Dit onderwerp toont aan hoe te opstelling een dashboard dat u helpt meten hoe de totale opbrengst onder uw klantenbasis wordt verdeeld. Begrijp welk percentage van klanten bijdragen welk percentage van opbrengst en creeer gesegmenteerde lijsten aan beste markt aan en behoud uw hoge bijdragende klanten.

Deze analyse bevat [ geavanceerde berekende kolommen ](../data-warehouse-mgr/adv-calc-columns.md).

## Aan de slag

U moet eerst een bestand uploaden dat alleen een primaire sleutel met de waarde één bevat. Hierdoor kunnen enkele noodzakelijke berekende kolommen voor de analyse worden gemaakt.

U kunt [ dossier uploader ](../importing-data/connecting-data/using-file-uploader.md) en het beeld gebruiken hieronder om uw dossier te formatteren.

## Berekende kolommen

Als u zich op de oorspronkelijke architectuur bevindt (bijvoorbeeld als u niet over de optie `Data Warehouse Views` in het menu `Manage Data` beschikt), neemt u contact op met het ondersteuningsteam om de onderstaande kolommen samen te stellen. Op de nieuwe architectuur, kunnen deze kolommen van de `Manage Data > Data Warehouse` pagina worden gecreeerd. Nadere instructies worden hieronder gegeven.

Een verder onderscheid wordt gemaakt als uw zaken gastorden toestaat. Als dat het geval is, kunt u alle stappen voor de tabel `customer_entity` negeren. Als gastorders niet zijn toegestaan, negeert u alle stappen voor de tabel `sales_flat_order` .

Te maken kolommen

* `Sales_flat_order/customer_entity` table
* (invoer) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **geval wanneer A ongeldig dan ongeldig is anders 1 eind**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` table (dit is het bestand dat u met het nummer hebt geüpload `1`)
* Aantal klanten
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Pad - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OF `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Geselecteerde kolom - `sales_flat_order.customer_email` OR `customer_entity.entity_id`

* `customer_entity` table
* Aantal klanten
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Pad - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Geselecteerde kolom - `Number of customers`

* (invoer) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* Eigenaar van gebeurtenis - `Number of customers`
* Status van gebeurtenis - `Customer's lifetime revenue`

* Inkomstenpercentage van de klant
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue` , `Number of customers`
* [!UICONTROL Calculation]: - * *geval wanneer A ongeldig dan ongeldig is anders (A/B)* 100 eind **
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` table
* Aantal klanten
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Pad - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Geselecteerde kolom - `Number of customers`

* (input) Rangorde door de opbrengst van het klantenleven
* [!UICONTROL Column type]: - `Same table > Event Number`
* Eigenaar van gebeurtenis - `Number of customers`
* Gebeurtenisgroep - `Customer's lifetime revenue`
* Filter - `Customer's order number = 1`

* Inkomstenpercentage van de klant
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue` , `Number of customers`
* [!UICONTROL Calculation]: - * *geval wanneer A ongeldig dan ongeldig is anders (A/B)* 100 eind **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>De gebruikte percentielen zijn zelfs splitsingen van klanten, die het xth percentiel van uw klantenbasis vertegenwoordigen. Elke klant wordt geassocieerd met een geheel van 1 tot 100, dat van als hun levenopbrengst *rang* kan worden gedacht. Bijvoorbeeld, als het de opbrengstpercentiel van de Klant voor een specifieke klant **5** is, is deze klant in het ***vijfde percentiel*** van alle klanten in termen van levensinkomsten.

## Metrisch

* **Totale waarde van het klantenleven**
* In de tabel `customer_entity`
* Deze metrisch voert a **Som** uit
* Op de kolom `Customer's lifetime revenue`
* Besteld door de `Customer's first order date` timestamp

## Rapporten

* **concentratie van de Klant**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
  [!UICONTROL Group door]: `Independent`
* Metrisch `A`: `Total customer lifetime revenue by percentile`
* Metrisch `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Boven/onder tonen: `100% of Customer's revenue percentile Name`
* 
  [!UICONTROL Chart type]: `Line`

* **Hoogste 10% concentratie**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Metrisch `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Diagram verbergen
* 
  [!UICONTROL Group door]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **Bottom 50% concentratie met slechts één aankoop**

* Metrisch `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Diagram verbergen
* 
  [!UICONTROL Group door]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **Bottom 10% concentratie**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Metrisch `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Diagram verbergen
* 
  [!UICONTROL Group door]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan er als het bovenstaande voorbeelddashboard uitzien.

Als u in om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten in dienst willen nemen, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
