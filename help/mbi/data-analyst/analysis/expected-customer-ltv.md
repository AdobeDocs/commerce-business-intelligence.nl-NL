---
title: LTV-analyse (Lifetime Value) verwacht voor Pro
description: Leer hoe te opstelling een dashboard dat u zal helpen de waardeverhoging van de klantenleven en verwachte levenwaarde van uw klanten begrijpen.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Verwachte Lifetime-waardeanalyse

In dit artikel, tonen wij aan hoe te opstelling een dashboard dat u zal helpen de waardegroei van de klantenleven en verwachte levenwaarde van uw klanten begrijpen.

![](../../assets/exp-lifetim-value-anyalysis.png)

Deze analyse is alleen beschikbaar voor klanten met een Pro-account op de nieuwe architectuur. Als uw account toegang heeft tot `Persistent Views` onderdeel onder de `Manage Data` zijbalk, bevindt u zich op de nieuwe architectuur en kunt u de hier vermelde instructies opvolgen om deze analyse zelf te maken.

Voordat u aan de slag gaat, wilt u zich vertrouwd maken met onze [cohort report builder.](../dev-reports/cohort-rpt-bldr.md)

## Berekende kolommen

Kolommen die op de **orders** tabel indien gebruiken **30 dagen**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definitie:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* Definitie: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Kolommen die op de **`orders`** tabel indien gebruiken **kalender** maanden:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* Definitie: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definitie:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* Definitie: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Metrisch

### Metrische instructies

Te maken statistieken

* **Afzonderlijke klanten op eerste besteldatum**
   * Als u gastorders inschakelt, gebruikt u `customer_email`

* In de **`orders`** table
* Deze maatstaf voert een **Afzonderlijke telwaarden**
* Op de **`customer_id`** kolom
* Besteld door de **`Customer's first order date`** tijdstempel

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Rapporten

### Instructies rapporteren

**Verwachte opbrengsten per klant per maand**

* Metrisch `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (Kies een redelijk getal voor X, bijvoorbeeld 24 maanden)
   * `Is in current month?` = `No`

* 
   [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Filter]:

* Metrisch `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* Metrisch `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

Overige diagramdetails

* [!UICONTROL Time period]: `All time`
* Tijdinterval: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - alles tonen
* Wijzig de `group by` voor de `All time customers` Metrisch naar onafhankelijk gebruiken van het potloodpictogram naast `group by`
* Bewerk de `Show top/bottom` velden als volgt:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Gem-ontvangsten per maand per cohort**

* Metrisch `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Gecumuleerde BG-inkomsten per maand per cohort**

* Metrisch `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het eindresultaat ziet er mogelijk uit als de afbeelding boven aan de pagina.

Als u op vragen loopt terwijl u deze analyse bouwt, of eenvoudig ons professionele de dienstenteam wilt in dienst nemen, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
