---
title: LTV-analyse (Lifetime Value) verwacht voor Pro
description: Leer hoe u een dashboard instelt waarmee u inzicht krijgt in de groei van de levenswaarde van klanten en de verwachte levensduurwaarde van uw klanten.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Verwachte Lifetime-waardeanalyse

Dit onderwerp toont aan hoe te opstelling een dashboard dat u helpt de de waardegroei van het klantenleven en verwachte levenwaarde van uw klanten begrijpen.

![](../../assets/exp-lifetim-value-anyalysis.png)

Deze analyse is alleen beschikbaar voor klanten met een Pro-account op de nieuwe architectuur. Als uw account toegang heeft tot de functie `Persistent Views` onder de zijbalk van `Manage Data` , bevindt u zich op de nieuwe architectuur en kunt u de onderstaande instructies volgen om deze analyse zelf te maken.

Alvorens begonnen te worden, wilt u met de [ bouwer van het cohortrapport vertrouwd maken.](../dev-reports/cohort-rpt-bldr.md)

## Berekende kolommen

Kolommen om op de **orden** lijst tot stand te brengen {als het gebruiken van **30 dagmaanden**:

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

Kolommen om op de **`orders`** lijst te creëren als het gebruiken van **kalender** maanden:

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

* **Afzonderlijke klanten door eerste ordedatum**
   * Gebruik `customer_email` als u gastorders inschakelt

* In de tabel **`orders`**
* Deze metrisch voert de Afzonderlijke Waarden van de Telling van a **uit**
* Op de kolom **`customer_id`**
* Besteld door de **`Customer's first order date`** timestamp

>[!NOTE]
>
>Zorg ervoor om [ alle nieuwe kolommen als afmetingen aan metriek ](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

## Rapporten

### Instructies rapporteren

**Verwachte opbrengst per klant door maand**

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
* [!UICONTROL Group by]: `Calendar months between first order and this order` - alles weergeven
* Wijzig de `group by` voor de metrische waarde `All time customers` in Onafhankelijk met het potloodpictogram naast `group by`
* Bewerk de velden `Show top/bottom` als volgt:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Gem opbrengst per maand door cohort**

* Metrisch `A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Cumulatieve inkomsten avg per maand door cohort**

* Metrisch `A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat ziet er mogelijk uit als de afbeelding boven aan de pagina.

Als u in om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten in dienst willen nemen, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
