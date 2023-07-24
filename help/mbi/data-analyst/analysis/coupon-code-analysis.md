---
title: Coupon-prestaties
description: Meer informatie over het analyseren van de prestaties van je coupon.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Geavanceerde puntcodeanalyse

Kennis van de couponprestaties van uw bedrijf is een interessante manier om uw bestellingen te segmenteren en uw klanten beter te begrijpen. Dit onderwerp begeleidt u door de stappen om analyses tot stand te brengen om te begrijpen welke klanten u door coupons te gebruiken verkrijgt, hoe zij uitvoeren en algemeen coupongebruik volgen.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Deze analyse bevat [geavanceerd berekende kolommen](../data-warehouse-mgr/adv-calc-columns.md).

## Aan de slag

Als eerste stap, moet u ervoor zorgen dat de volgende kolommen aan uw Data Warehouse worden gesynchroniseerd. Als dat niet zo is, ga dan door en ga naar `Manage Data` > `Data Warehouse`en het volgende synchroniseren:

* **sales\_flat\_order** table
* **coupon\_code**
* **base\_korting\_amount**

## Berekende kolommen

Kolommen om ongeacht het beleid van gastorden tot stand te brengen:

* `sales\_flat\_order` table
* **Op de order is coupon toegepast?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * 
     [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: geval wanneer `A` is dan null `No coupon` else `Coupon` end

* **\[INPUT\] klant\_id - couponcode**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype] String
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **Aantal opdrachten met deze coupon**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Eigenaar van gebeurtenis:`INPUT customer_id - coupon code`
   * Gebeurtenisgroep: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` filterset

Extra kolommen die moeten worden gemaakt als gastorders NIET worden ondersteund:

* `customer\_entity` table
   * **De eerste bestelling van de klant is voorzien van een coupon? (Coupon/Geen coupon)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Selecteer een [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **Het coupon van de eerste bestelling van de klant**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecteer een [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **Levenslang aantal gebruikte coupons van de klant**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **Klanten die geld aankopen of klanten die geen coupon kopen**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * 
        [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: **geval waarin A=&#39;Coupon&#39; dan &#39;Coupon acquisicustomer&#39; anders &#39;Non-coupon acquisition customer&#39; end is**

   * **Percentage van de orders van de klant met coupon**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * 
        [!UICONTROL Datatype]: `Decimal`
      * [!UICONTROL Calculation]: **case als A null of B null is of B=0 dan null als A/B-einde**

   * **Gebruik van coupon door klant**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * 
        [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: **case when A is null then null when A=0 then &#39;Never used coupon&#39; when A&lt;0.5 then &#39;Moarly full price&#39; when A=0.5 then &#39;50/50&#39; when A=1 then &#39;Coupons only&#39; when A>0.5 then &#39;Moarly coupon&#39; else &#39;Undefined&#39; end**

* `sales\_flat\_order` table
   * **De eerste bestelling van de klant is inclusief coupon? (Coupon/Geen coupon)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecteer een [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **Het coupon van de eerste bestelling van de klant**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Selecteer een [!UICONTROL column]: `Customer's first order coupon?`

Extra kolommen die moeten worden gemaakt als gastorders NIET worden ondersteund:

* `sales\_flat\_order` table
   * **De eerste bestelling van de klant is voorzien van een coupon? (Coupon/Geen coupon)** **-** gemaakt door analist als onderdeel van uw \[COUPON ANALYSE\]-ticket
   * **Het coupon van de eerste bestelling van de klant**{:}**-** gemaakt door analist als onderdeel van uw \[COUPON ANALYSE\]-ticket

* **Levenslang aantal gebruikte coupons van de klant**{:}**-** gemaakt door analist als onderdeel van uw \[COUPON ANALYSE\]-ticket
* **Klanten die geld aankopen of klanten die geen coupon kopen**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * 
     [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: **geval waarin A=&#39;Coupon&#39; dan &#39;Coupon acquisicustomer&#39; anders &#39;Non-coupon acquisition customer&#39; end is**

* **Percentage van de orders van de klant met coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * 
     [!UICONTROL Datatype]: `Decimal`
   * [!UICONTROL Calculation]: **case als A null of B null is of B=0 dan null als A/B-einde**

* **Gebruik van coupon door klant**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * 
     [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: **case when A is null then null when A=0 then &#39;Never used coupon&#39; when A&lt;0.5 then &#39;Moarly full price&#39; when A=0.5 then &#39;50/50&#39; when A=1 then &#39;Coupons only&#39; when A>0.5 then &#39;Moarly coupon&#39; else &#39;Undefined&#39; end**

## Metrisch

* **Koopkorting**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* In de `sales\_flat\_order` table
* Deze maatstaf voert een **Som**
* Op de `discount\_amount` kolom
* Besteld door de `created\_at` tijdstempel
* [!UICONTROL Filter]:

* **Aantal gebruikte coupons**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* In de `sales\_flat\_order` table
* Deze maatstaf voert een **Aantal**
* Op de `entity\_id` kolom
* Besteld door de `created\_at` tijdstempel
* [!UICONTROL Filter]:

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Rapporten

* **% van klanten met en zonder coupon**
   * [!UICONTROL Metric]: `New customers`

* Metrisch `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` of `Non coupon acquisition customer`
* 
  [!UICONTROL Chart type]: `Pie`

* **Aantal klanten met en zonder coupon**
   * [!UICONTROL Metric]: `New customers`

* Metrisch A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` of `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Gemiddelde inkomsten tijdens de levensduur: Coupon Acq. (leeftijd van 90+ dagen)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * De eerste bestelling van de klant bevatte een coupon (Coupon/No Coupon) = Coupon

* Metrisch `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Gemiddelde inkomsten tijdens de levensduur: Geen coupon Acq. (leeftijd van 90+ dagen)**
   * [!UICONTROL Metric]: Gemiddelde inkomsten tijdens de levensduur
   * [!UICONTROL Filter]:
      * De eerste opdracht van de klant bevatte een coupon (Coupon/No Coupon) = Geen coupon

* Metrisch `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Gemiddelde levensopbrengsten per coupon voor eerste bestelling**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Metrisch `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 
  [!UICONTROL Chart type]: `Column`

>[!NOTE]
>
>Als u veel couponcodes hebt, zoals veel clients doen, wilt u een Top/Bottom toepassen, zoals Top 10, gesorteerd op Gem. levenslange inkomsten

* **Waarschijnlijk herhalingsvolgorde: Overnames van coupons**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * De eerste bestelling van de klant bevatte een coupon (Coupon/No Coupon) = Coupon

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * De eerste bestelling van de klant bevatte een coupon (Coupon/No Coupon) = Coupon
      * Is de laatste bestelling van de klant? = Nee
   * 
     [!UICONTROL-formule]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * statistisch significant aantal selecteren uit `Customer's by lifetime orders` grafiek. Wanneer het bekijken van de grafiek, als goede regel orderaantallen met 30 of meer klanten in het emmertje moet zoeken. Afhankelijk van uw gegevensset kan dit een groot aantal zijn, zodat u 1-10 gratis kunt toevoegen.

* Metrisch `A`: `Number of orders`
* Metrisch `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Herhalingsvolgorde: Niet-couponaankopen**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * De eerste bestelling van de klant bevatte een coupon (Coupon/No Coupon) = Geen coupon

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * De eerste bestelling van de klant bevatte een coupon (Coupon/No Coupon) = Geen coupon
      * Is de laatste bestelling van de klant? = Nee

   * 
     [!UICONTROL-formule]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * statistisch significant aantal selecteren uit `Customer's by lifetime orders` grafiek of 1-5.

* Metrisch `A`: `Number of orders`
* Metrisch `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Door coupon verkregen gebruikstarief van klanten met coupon (herhaalde opdrachten)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Klanten die geld aankopen of klanten die geen coupon aankopen = couponaankoop

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant > 1
      * De eerste bestelling van de klant is voorzien van een coupon? (Coupon/No coupon) = Coupon

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant > 1
      * De eerste bestelling van de klant is voorzien van een coupon? (Coupon/No coupon) = Coupon
      * Op de order is coupon toegepast? (Coupon/No coupon) = Coupon

   * 
     [!UICONTROL-formule]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* Metrisch `A`: `Coupon-acquired customers`
* Metrisch `B`: `Number of repeat orders`
* Metrisch `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Table` (kan deze tabel omzetten voor een betere visualisatie)

* **Gebruik van coupon door klanten zonder coupon (herhaalde opdrachten)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Klanten die geld aankopen of klanten die geen coupon kopen = Niet-couponaankoop

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant > 1
      * De eerste bestelling van de klant is voorzien van een coupon? (Coupon/No coupon) = Geen coupon

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant > 1
      * De eerste bestelling van de klant is voorzien van een coupon? (Coupon/No coupon) = Geen coupon
      * Op de order is coupon toegepast? (Coupon/No coupon) = Coupon

   * 
     [!UICONTROL-formule]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* Metrisch `A`: `Non-coupon-acquired customers`
* Metrisch `B`: `Number of repeat orders`
* Metrisch `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Table` (kan deze tabel omzetten voor een betere visualisatie)

* **Gebruiksgegevens van coupon (eerste bestellingen)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant = 1
      * Aantal opdrachten met deze coupon > 10

   * 
     [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant = 1
      * Aantal opdrachten met deze coupon > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant = 1
      * Aantal opdrachten met deze coupon > 10

   * [!UICONTROL Formula]: `B-C` (indien C negatief is); B+C (als C positief is)
   * 
     [!UICONTROL-indeling]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * bestelnummer van de klant = 1
      * Aantal opdrachten met deze coupon > 10

* Metrisch `A`: `First time orders (FTO)`
* Metrisch `B`: `Revenue from FTO`
* Metrisch `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Metrisch `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
  [!UICONTROL Chart type]: `Table`
>[!NOTE]
>
>Het aantal van 10 voor &quot;Aantal orders met deze coupon&quot; is willekeurig. Voel u vrij om de meest geschikte hoeveelheid voor dit filter te gebruiken.

* **Aantal opdrachten met coupon (alle tijd)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Metrisch `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Netto-inkomsten uit orders met coupons (alle tijd)**
   * 
     [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter]:
      * Op de order is coupon toegepast? (Coupon/No coupon) = Coupon

* Metrisch `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Kortingen op coupons (alle tijd)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Metrisch `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Aantal orders met en zonder coupons**
   * [!UICONTROL Metric]: `Number of orders`

* Metrisch `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Coupongebruik bij herhaalde gebruikers**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Aantal bestellingen > 1

* Metrisch `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 
  [!UICONTROL Chart type]: `Pie`

* **Gebruiksgegevens van coupon**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Aantal opdrachten met deze coupon > 10

   * 
     [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter]:
      * Aantal opdrachten met deze coupon > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Aantal opdrachten met deze coupon > 10

   * [!UICONTROL Formula]: `B-C` (if `C` negatief is); `B+C` (if `C` is positief)
   * 
     [!UICONTROL-indeling]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (if `C` negatief is); `C/(B+C)` (if `C` is positief)
   * 
     [!UICONTROL-indeling]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Aantal opdrachten met deze coupon > 10

   * 
     [!UICONTROL-formule]: `C/A`
   * 
     [!UICONTROL-indeling]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * Aantal opdrachten met deze coupon > 10

* Metrisch `A`: `Number of orders`
* Metrisch `B`: `Net revenue from orders`
* Metrisch `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Metrisch `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Metrisch `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
  [!UICONTROL Chart type]: `Table`

>[!NOTE]
>
>Het aantal van 10 voor &quot;Aantal orders met deze coupon&quot; is willekeurig. Voel u vrij om de meest geschikte hoeveelheid voor dit filter te gebruiken.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat ziet er mogelijk uit als de afbeelding boven aan de pagina.

Als u op om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten wilt in dienst nemen, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
