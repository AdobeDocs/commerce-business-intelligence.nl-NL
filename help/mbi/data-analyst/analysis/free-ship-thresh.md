---
title: Gratis verzenddrempel
description: Leer hoe u een dashboard instelt dat de prestaties van je gratis verzenddrempel bijhoudt.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# Gratis verzending

>[!NOTE]
>
>Dit artikel bevat instructies voor cliënten die de originele architectuur en de nieuwe architectuur gebruiken. U bevindt zich op de nieuwe architectuur als de sectie &quot;Weergaven Data Warehouse&quot; beschikbaar is nadat u &quot;Gegevens beheren&quot; op de hoofdwerkbalk hebt geselecteerd.

Dit artikel laat zien hoe u een dashboard instelt dat de prestaties van uw gratis verzenddrempel bijhoudt. Dit dashboard, dat hieronder wordt getoond, is een uitstekende manier aan test A/B twee vrije verschepingsdrempels. Je bedrijf weet bijvoorbeeld niet zeker of je gratis verzending moet aanbieden op $50 of $100. U zou een A/B test van twee willekeurige ondergroepen van uw klanten moeten uitvoeren, en de analyse uitvoeren in [!DNL MBI].

Voordat je aan de slag gaat, wil je twee verschillende tijdsperioden identificeren waarbij je verschillende waarden hebt voor de drempel voor gratis verzending in je winkel.

![](../../assets/free_shipping_threshold.png)

Deze analyse bevat [geavanceerd berekende kolommen](../data-warehouse-mgr/adv-calc-columns.md).

## Berekende kolommen

Als u zich op de originele architectuur bevindt (bijvoorbeeld als u geen `Data Warehouse Views` optie onder de `Manage Data` (menu), wilt u uit naar het ondersteuningsteam om de hieronder kolommen te bouwen. Op de nieuwe architectuur, kunnen deze kolommen van worden gecreeerd `Manage Data > Data Warehouse` pagina. Nadere instructies worden hieronder gegeven.

* **`sales_flat_order`** table
   * Met deze berekening maakt u emmers in stappen ten opzichte van de typische tekengrootten. Dit kan variëren van stappen zoals 5, 10, 50, 100

* **`Order subtotal (buckets)`** Oorspronkelijke architectuur: gemaakt door een analist als onderdeel van uw `[FREE SHIPPING ANALYSIS]` kaartje
* **`Order subtotal (buckets)`** Nieuwe architectuur:
   * Zoals hierboven vermeld, leidt deze berekening tot emmers in toename met betrekking tot uw typische wortelgrootte. Als u een native subtotaal kolom hebt, zoals `base_subtotal`, die als basis voor deze nieuwe kolom kunnen worden gebruikt. Als dat niet het geval is, kan het een berekende kolom zijn die verzendingen en kortingen van inkomsten uitsluit.
   >[!NOTE]
   >
   >De &quot;emmer&quot;grootte hangt van wat voor u als cliënt aangewezen is af. U kunt beginnen met uw `average order value` en maak enkele emmers kleiner dan of groter dan die hoeveelheid. Wanneer het bekijken van de berekening hieronder, ziet u hoe te om een deel van de vraag gemakkelijk te kopiëren, het uit te geven, en extra emmers tot stand te brengen. Het voorbeeld wordt uitgevoerd in stappen van 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`, of `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
wanneer `A< 200` en `A <= 250` dan `201 - 250`
wanneer `A<251` en `A<= 300` dan `251 - 300`
wanneer `A<301` en `A<= 350` dan `301 - 350`
wanneer `A<351` en `A<=400` dan `351 - 400`
wanneer `A<401` en `A<=450` dan `401 - 450`
else &quot;over 450&quot; end



## Metrisch

Geen nieuwe metriek!!!

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Rapporten

* **Gemiddelde bestelwaarde met verzendregel A**
   * [!UICONTROL Metric]: `Average order value`

* Metrisch `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Aantal orders per subtotaal emmer met verzendingsregel A**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >U kunt het staartuiteinde afsnijden door de bovenkant te tonen `X` `sorted by` `Order subtotal` (emmers) in de `Show top/bottom`.

* Metrisch `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **Percentage van bestellingen per subtotaal met verzendregel A**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL Group door]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* Metrisch `A`: `Number of orders by subtotal (hide)`
* Metrisch `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`

* **Percentage van orders met een subtotaal dat de verzendingsregel A overschrijdt**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Group door]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* Metrisch `A`: `Number of orders by subtotal`
* Metrisch `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


Herhaal bovenstaande stappen en rapporten voor Verzending B en de tijdsperiode met verzendregel B.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat ziet er mogelijk uit als de afbeelding boven aan deze pagina.
