---
title: Basisanalyses begrijpen en bouwen
description: Leer hoe u analyses van basisbeginselen begrijpt en bouwt.
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Dashboards, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '3113'
ht-degree: 0%

---

# Basisanalyses

Als u eenmaal vertrouwd bent met de [!DNL Adobe Commerce Intelligence] en u hebt een basiskennis van het hulpmiddel, wilt u beginnen rapporten op te stellen. Een van de meest voorkomende vragen die je hebt is: &quot;Waar moet ik naar kijken?&quot;

De informatie hieronder schetst enkele gemeenschappelijke metriek en rapporten die u waardevol zou kunnen vinden. Sommige van deze rapporten bestaan in uw account, dus controleer de cijfers en rapporten die in uw account staan om te voorkomen dat er duplicaten worden gemaakt.

## Tabellen en kolommen die u wilt begrijpen

Wanneer het bouwen van metrisch, moet u vier stukken van informatie kennen:

1. De tafel waarop de gegevens leven,
1. De specifieke handeling die u wilt uitvoeren,
1. De kolom waarop u die handeling wilt uitvoeren, en
1. Het tijdstempel dat u wilt gebruiken voor het bijhouden van die gegevens.

Waarschijnlijk verschillen de namen van de tabellen die in deze voorbeelden worden gebruikt enigszins van de kolom- en tabelnamen in uw database, omdat elke database uniek is. Verwijs naar de onderstaande definities als u hulp met het identificeren van een overeenkomstige lijst of kolom in uw gegevensbestand nodig hebt.

## Klantentabel

Deze lijst bevat de belangrijkste informatie over elke klant, zoals een unieke klant - identiteitskaart, e-mailadres, etc. De onderstaande voorbeelden worden gebruikt **[!UICONTROL customer_entity]** als de naam van een voorbeeldklantentabel.

Als sommige van deze berekeningen momenteel niet bestaan in uw database, kunnen alle beheerders in uw account ze maken. Bovendien moet u ervoor zorgen dat deze afmetingen gegroepeerd zijn voor alle toepasselijke meetgegevens.

**Dimension**

* **[!UICONTROL Entity_id]**: Een unieke id voor elke klant. Dit kan ook een uniek klantnummer of een e-mailadres van een klant zijn en moet fungeren als referentietoets voor de tabel van uw bestelling.
* **[!UICONTROL Created_at]**: De datum waarop de account van de klant is gemaakt en aan uw database is toegevoegd.
* **[!UICONTROL Customer's lifetime revenue]**: De totale levensinkomsten die door een klant worden gegenereerd.
* **[!UICONTROL Customer's first 30-day revenue]**: Het totale bedrag aan inkomsten dat een klant in de eerste 30 dagen heeft gegenereerd.
* **[!UICONTROL Customer's lifetime number of orders]**: Het aantal orders die door een klant gedurende hun leven worden geplaatst.
* **[!UICONTROL Customer's lifetime number of coupons]**: Het totale aantal coupons dat een klant gedurende zijn levensduur gebruikt.
* **[!UICONTROL Customer's first order date]**: De datum van de eerste bestelling van een klant. Dit kan anders zijn dan de created_at datum als een klant geen orde op het tijdstip van hun verwezenlijking plaatste.

**Accepteer je gastorders?**

*In dat geval bevat deze tabel mogelijk niet al uw klanten. Contact opnemen met de [ondersteuningsteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om ervoor te zorgen dat alle klanten bij de analyses van uw klanten worden betrokken.*

*Weet u niet zeker of u gastorders accepteert? Zie [dit onderwerp](../data-warehouse-mgr/guest-orders.md) voor meer informatie!*

## Orderentabel

In deze tabel vertegenwoordigt elke rij één volgorde. De kolommen in deze tabel bevatten basisinformatie over elke bestelling, zoals de id van de bestelling, de aanmaakdatum, de status, de id van de klant die de bestelling heeft geplaatst, enzovoort. De onderstaande voorbeelden worden gebruikt **[!UICONTROL sales_flat_order]** als de naam van een tabel met voorbeeldorders.

**Dimension**

* **[!UICONTROL Customer_id]**: Een unieke id voor de klant die de bestelling heeft geplaatst. Dit wordt vaak gebruikt om informatie tussen de klant en orden lijsten te bewegen. In deze voorbeelden verwacht u customer_id op **[!UICONTROL sales_flat_order]** tabel die moet worden uitgelijnd met de **[!UICONTROL entitiy_id]** op de **[!UICONTROL customer_entity]** tabel.
* **[!UICONTROL Created_at]**: De datum waarop de bestelling is gemaakt of geplaatst.
* **[!UICONTROL Customer_email]**: Het e-mailadres van de klant die de bestelling heeft geplaatst. Dit kan ook de unieke identificatie voor de klant zijn.
* **[!UICONTROL Customer's lifetime number of orders]**: Een kopie van de kolom met dezelfde naam op uw `Customers` tabel.
* **[!UICONTROL Customer's order number]**: Het volgnummer van de bestelling dat aan de bestelling is gekoppeld. Bijvoorbeeld, als de rij u bekijkt de eerste orde van een klant is, is deze kolom &quot;1&quot;; maar als dit de 15e bestelling van de klant was, staat in deze kolom &quot;15&quot; voor deze bestelling. Als deze dimensie niet bestaat op uw `Customers` tabel, vraag de [ondersteuningsteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om u te helpen het bouwen.
* **[!UICONTROL Customer's order number (previous-current)]**: Een aaneenschakeling van twee waarden in de **[!UICONTROL Customer's order number]** kolom. Het wordt gebruikt in een steekproefrapport hieronder om de verstreken tijd tussen om het even welke twee orden te tonen. De tijd tussen bijvoorbeeld de eerste besteldatum van een klant en de tweede besteldatum wordt bij deze berekening weergegeven als &quot;1-2&quot;.
* **[!UICONTROL Coupon_code]**: Geeft aan welke coupons zijn gebruikt voor elke bestelling.
* **[!UICONTROL Seconds since previous order]**: De tijd (in seconden) tussen bestellingen van een klant.

## Tabel met volgordeitems

In deze tabel vertegenwoordigt elke rij één object dat is verkocht. Deze tabel bevat informatie over de objecten die in elke bestelling worden verkocht, zoals het referentienummer van de bestelling, het productnummer, de hoeveelheid, enzovoort. De onderstaande voorbeelden worden gebruikt `sales_flat_order_item` als de naam van een tabel met items in de voorbeeldvolgorde.

**Dimension**

* **[!UICONTROL Item_id]**: De unieke id voor elke rij in de tabel.
* **[!UICONTROL Order_id]**: De referentiesleutel voor uw `Orders` tabel die aangeeft welke items in dezelfde volgorde zijn aangeschaft. Als een volgorde meerdere items bevat, wordt deze waarde herhaald.
* **[!UICONTROL Product_id]**: Als u informatie wilt over het specifieke product dat is aangeschaft (zoals kleur, grootte, enzovoort), gebruikt u deze kolom om die informatie uit de tabel met producten te halen.
* **[!UICONTROL Order's created_at]**: Het tijdstempel dat de bestelling is geplaatst, wordt doorgaans naar uw `order line items` tabel `Orders` tabel.
* **[!UICONTROL Order's coupon_code]**: Vergelijkbaar met de `Order's created_at` dimensie, wordt deze kolom gekopieerd uit uw lijst van orden.

## Subscriptietabel

Deze tabel wordt gebruikt voor het beheer van uw abonnementsgegevens, zoals de abonnements-id, het e-mailadres van de abonnee, de startdatum van het abonnement enzovoort.

**Dimension**

* **[!UICONTROL Customer_id]**: Een unieke id voor de klant die de bestelling heeft geplaatst. Dit is een gemeenschappelijke manier om een weg tussen de lijst van Klanten en de lijst van Orden te bouwen. In deze voorbeelden verwacht u customer_id op **sales_flat_order** tabel die moet worden uitgelijnd met de `entitiy_id` op de `customer_entity` tabel.
* **[!UICONTROL Start date]**: De datum waarop het abonnement van een klant is gestart.

## Tabel met marketinguitgaven

Wanneer u uw marketinguitgaven analyseert, kunt u [!DNL Facebook], [!DNL Google AdWords]of andere bronnen in uw analyses. Als u meerdere marketinguitgavenbronnen hebt, neemt u contact op met de [Managed Services Team](https://business.adobe.com/products/magento/fully-managed-service.html) voor hulp bij het instellen van een geconsolideerde tabel voor uw marketingcampagnes.

**Dimension**

* **[!UICONTROL Spend]**: De totale advertentie-uitgaven. In [!DNL Facebook]Dit zou de uitgavenkolom zijn in de `facebook_ads_insights_####` tabel. Voor [!DNL Google AdWords]is dit `adCost` in de `campaigns####` tabel.
* De `####` die aan elk van deze tabellen wordt toegevoegd, heeft betrekking op de specifieke account-id voor uw [!DNL Facebook] of [!DNL Google AdWords] account.
* **[!UICONTROL Clicks]**: Het totale aantal klikken. In [!DNL Facebook], dit zou de klikkolom in zijn `facebook_ads_insights_####` tabel. In [!DNL Google AdWords], dit zou de kolom adClicks in `campaigns####` tabel.
* **[!UICONTROL Impressions]**: The total number of impressions. In [!DNL Facebook], zou dit de indruk zijn in de `facebook_ads_insights_####` tabel. In [!DNL Google AdWords]Dit zou de indruk wekken dat `campaigns####` tabel.
* **[!UICONTROL Campaign]**: Het totale aantal klikken. In [!DNL Facebook], dit zou de kolom campagne_name in `facebook_ads_insights_####` tabel. In [!DNL Google AdWords]Dit zou de campagnekolom zijn in het dialoogvenster `campaigns####` tabel.
* **[!UICONTROL Date]**: Het tijdstip en de datum waarop de activiteit (uitgeven, klikken of indrukken) voor een bepaalde campagne is opgetreden. In [!DNL Facebook]is dit `date_start` in de `facebook_ads_insights_####` tabel. In [!DNL Google AdWords]Dit is de datumkolom in het dialoogvenster `campaigns####` tabel.
* **[!UICONTROL Customer's first order's source]**: De bron van de bestelling van de eerste bestelling van de klant. Controleer eerst of u een kolom met de naam `customer's first order's source` in uw account. Als deze kolom niet wordt weergegeven, kunt u met deze instructies de gewenste kolom maken.
* **[!UICONTROL Customer's first order's medium]**: Het medium van de bestelling van de eerste bestelling van de klant. Controleer eerst of u een kolom met de naam `customer's first order's source` in uw account. Als deze kolom niet wordt weergegeven, kunt u met deze instructies de gewenste kolom maken.
* **[!UICONTROL Customer's first order's campaign]**: De campagne van de bestelling van de eerste bestelling van een klant. Controleer eerst of u een kolom met de naam `customer's first order's source` in uw account. Als deze kolom niet wordt weergegeven, kunt u met deze instructies de gewenste kolom maken.

## Algemene rapporten en maatstaven

Hier volgen enkele voorbeelden van rapporten en meetgegevens die u nuttig kunt vinden:

* [Klantenanalyse](#customeranalytics)
* [Order Analytics](#orderanalytics)
* [Analyse van marketinguitgaven](#mktgspendanalytics)

## Klantenanalyse {#customeranalytics}

### Nieuwe gebruikers

* **Beschrijving**: Een telling van het totale aantal nieuw verworven gebruikers over een bepaalde periode. `New Users` verschilt van `Unique Customers`, omdat `New Users` heeft het tijdstempel dat een account is gemaakt met uw service (dit betekent niet dat ze noodzakelijkerwijs een bestelling plaatsen), terwijl `Unique Customers` ten minste één bestelling hebben geplaatst.
* **Metrische definitie**: Deze maatstaf voert een **Aantal** van `entity_id` van `customer_entity` tabel geordend door `created_at`.
* **Voorbeeld van rapport**: Aantal nieuwe gebruikers dat vorige maand is gemaakt
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Time Range]**: `Last Month`
   * **[!UICONTROL Time Interval]**: `By Day`

![Nieuwe gebruikers](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### Unieke klanten

* **Beschrijving**: Een telling van het totale aantal afzonderlijke klanten over een bepaalde periode. Dit verschilt van `New Users`, omdat deze alleen klanten volgt die minstens één bestelling hebben geplaatst. Een verschillend rapport van de klant volgt slechts één keer een klant in een bepaald tijdinterval. Als u het tijdsinterval instelt op `By Day` en een klant op die dag meer dan één aankoop doet, wordt de klant slechts één keer meegeteld. Als je een totaal aantal aankopen in het algemeen wilt zien, kijk dan naar `Number of Orders`.
* **Metrische definitie**: Deze maatstaf voert een **Verschil aantal** van `customer_id` van `sales_flat_order` tabel geordend door `created_at`.
* **Voorbeeld van rapport**: Afzonderlijke klanten per week in de afgelopen 90 dagen
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**: `By Day`

![Unieke klanten.](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### Nieuwe abonnees

* **Beschrijving**: Een telling van het totale aantal nieuwe abonnees dat over een bepaalde periode is verworven.
* **Metrische definitie**: Deze maatstaf voert een **Verschil aantal** van `customer_id` van `subscriptions` tabel geordend door `start_date`.
* **Voorbeeld van rapport**: Dit jaar op maand nieuwe abonnees
   * **[!UICONTROL Metric]**: `New Subscribers`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

![Abonnees](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### Klanten herhalen

* **Beschrijving**: Het totale aantal klanten dat meer dan één bestelling over een periode heeft geplaatst. In een rapport van herhaalde klanten, kunt u gebruiken `Distinct Customers` de `Customer's Order Number` dimensie van uw `orders` tabel.
* **Metrisch gebruikt**: `Distinct Customers`
* **Voorbeeld van rapport**: Aantal tweede en derde aankopen vorig jaar
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's Order Number`selecteert u vervolgens `2` en `3`

  ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **Voorbeeld 2 van rapport**: Aantal herhaalde klanten in de afgelopen jaren
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Filters]**: `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**: `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`

  ![Vorig jaar klanten herhalen](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### Bovenste klanten op levenslange aantal orders

* **Beschrijving**: Een lijst van de hoogste klanten die op hun totaal aantal orden wordt gebaseerd. Dit biedt je een directe lijst van je meest voorkomende kopers.
* **Metrisch gebruikt**: `Orders`
* **Voorbeeld van rapport**: De 25 belangrijkste klanten volgens het aantal bestellingen tijdens hun levensduur
   * **[!UICONTROL Metric]**: `Orders`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top/Bottom]**: Top 25 gesorteerd op bestellingen

  ![De 25 belangrijkste klanten per bestelling](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### De hoogste klanten door levensinkomsten

* **Beschrijving**: Een lijst van de hoogste klanten die op levensinkomsten worden gebaseerd.
* **Metrisch gebruikt**: `Average Lifetime Revenue`
* **Voorbeeld van rapport**: De 25 meest klanten met inkomsten uit levenstijd
   * **[!UICONTROL Metric]**: `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top Bottom]**: Top 25 gesorteerd op inkomsten uit levens

  ![Top 25 van klanten op basis van inkomsten](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### Gemiddelde levensopbrengsten per cohort

* **Beschrijving**: De [gemiddelde levensduuropbrengsten van verschillende cohorten](../dev-reports/lifetime-rev-cohort-analysis.md) van gebruikers in de loop van de tijd om de best presterende cohorten te identificeren. Cohorts worden gegroepeerd op een gemeenschappelijke datum, zoals de eerste besteldatum of de aanmaakdatum.
* **Metrisch gebruikt**: `Revenue`
* **Voorbeeld van rapport**: Gemiddelde inkomsten uit levensduur van klanten per cohort
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Cohort Date]**: `Customer's first order date`
   * **[!UICONTROL Time Interval]**: `Month`
   * **[!UICONTROL Time Period]**: Verhuisset cohorten van de meest recente acht cohorten met ten minste vier maanden gegevens
   * **[!UICONTROL Duration]**: `12 Month(s)`
   * **[!UICONTROL Table]**: `Customer_entity`
   * **[!UICONTROL Perspective]**: Gecumuleerde gemiddelde waarde per cohortelid

  ![Inkomsten uit overlevingstijd van klanten per cohort](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### Klanten op basis van gebruik van coupons

* **Beschrijving**: Een aantal klanten die een coupon-/disconteringscode hebben gebruikt. Dit kan u helpen een duidelijk beeld van uw kortingzoekers tegenover volledige kopers te krijgen.
* **Metrisch gebruikt**: `New Users`
* **Voorbeeld van rapport**: Klanten met coupon en zonder coupon per maand
   * **[!UICONTROL Metric A]**: `Non coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: Levensduur van de klant Aantal bestellingen groter dan 0 en levenslange aantal coupons gelijk aan 0 van de klant
   * **[!UICONTROL Metric B]**: `Coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: Het aantal bestellingen van klanten dat langer is dan 0 en het levenslange aantal coupons van de klant dat groter is dan 0
   * **[!UICONTROL Time range]**: `All Time`
   * **[!UICONTROL Time interval]**: `By Month`

  ![Klanten op basis van Coupon-gebruik](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **Voorbeeld 2 van rapport**: Percentage klanten met coupon en zonder coupon per maand
   * **[!UICONTROL Metric A]**: `Non coupon customers` (metrische gegevens verbergen)
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customer's Lifetime Number of Orders Greater Than 0` en `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**: `Coupon customers`
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customers Lifetime Number of Orders Greater Than 0` en `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Formula]**: `B/(A+B)`

>[!NOTE]
>
> **Alle metriek verbergen**

![Coupongebruik](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### Gemiddelde eerste 30-daagse inkomsten

* **Beschrijving**: Het gemiddelde van het bedrag van inkomsten dat klanten binnen hun eerste 30 dagen als klant hebben gegenereerd.
* **Metrische beschrijving**: Deze maatstaf voert een **Gemiddeld** van `Customer's First 30 Day Revenue` van `customer_entity` tabel geordend door `created_at`.
* **Beschrijving van rapport**: Het gemiddelde van de eerste 30 dagen van de klant
* **[!UICONTROL Metric]**: `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]**: `All Time`
* **[!UICONTROL Time Interval]**: `None`

![Gemiddelde omzet eerste 30 dagen](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### Gemiddelde omzet tijdens de levensduur van de klant

* **Beschrijving**: Het gemiddelde bedrag van opbrengst die door uw klanten over hun leven wordt geproduceerd.
* **Metrische beschrijving**: Deze maatstaf voert een **Gemiddeld** van de `Customer's Lifetime Revenue` kolom op de `customer_entity` op basis van de `created_at`.
* **Beschrijving van rapport**: Gemiddelde over de gehele levensduur van de klant
   * **[!UICONTROL Metric]**: `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`

![Inkomsten uit levensduur van klanten](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## Analyses bestellen {#orderanalytics}

### Ontvangsten

* **Beschrijving**: De maatstaf van de opbrengst toont de totale opbrengst die over een gekozen tijdspanne wordt verdiend.
* Deze maatstaf voert een **som** van `grand_total` van `sales_flat_order` tabel geordend door `created_at`.
* **Voorbeeld van rapport**: Ontvangsten per maand, YTD
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **Tijdinterval**: `By Month`

>[!TIP]
>
>Zorg ervoor uw omzetmetrische berekening verenigbaar met de definitie is die u intern bespreekt. U wilt bijvoorbeeld inkomsten tellen uit orders die zijn verzonden, valuta&#39;s uit verschillende regio&#39;s converteren of belasting uitsluiten. U kunt ook [Filtersets](../../data-user/reports/ess-manage-data-filters.md) om consistentie te verzekeren over alle metriek die op de zelfde lijst worden voortgebouwd.

![Ontvangsten](../../assets/revenue.png)<!--{: width="929"}-->

### Orders

* **Beschrijving**: Een telling van het totale aantal orders over een bepaalde periode. Een orderrapport volgt veranderingen in ordervolume die door nieuw productdienstenaanbod, promoties, of om het even wat worden veroorzaakt die (of) transactievolume kunnen verhogen of verminderen. U kunt deze metrisch vaak door sommige variabelen willen segmenteren om uw vragen te beantwoorden.
* **Metrische definitie**: Deze maatstaf voert een **Aantal** van `entity_id` van `sales_flat_order` tabel geordend door `created_at`.
* **Voorbeeld van rapport**: Orders per maand, YTD
   * **[!UICONTROL Metric]**: `number of orders`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

>[!TIP]
>
>Net als de metrische inkomsten, moet u [Filtersets](../../data-user/reports/ess-manage-data-filters.md) op zijn plaats om onvolledige, test, of teruggekeerde orden uit te sluiten.

![Orders](../../assets/orders_pic.png)<!--{: width="929"}-->

### Geordende producten

* **Beschrijving**: De geordende metrische producten vertellen u de hoeveelheid punten die over een specifieke tijdspanne worden verkocht.
* **Metrische definitie**: Deze maatstaf voert een **som** van `qty_ordered` van `sales_flat_order_item` tabel geordend door `created_at`.
* **Voorbeeld van rapport**: Objecten verkocht per maand, YTD
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

  ![Geordende producten](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* Combineer deze metrische waarde met het aantal orders om het aantal items per bestelling te berekenen. Voeg vervolgens couponcodes toe aan het rapport om te bepalen hoe uw promoties de grootte van winkelwagentjes beïnvloeden, of deel deze met nieuwe of herhaalde bestellingen om uw klantengedrag beter te begrijpen.
* **Voorbeeld van rapport**: Producten per bestelling: eerste orde vs. herhalingsorden
   * **[!UICONTROL Metric A]**: Geordende producten: eerste opdracht
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric B]**: Bestellingen: eerste opdracht
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric C]**: Geordende producten: herhalingsorders
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Metric D]**: Bestellingen: Volgorde herhalen
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Week`
   * **[!UICONTROL Formula 1]**: `A/B`
   * **[!UICONTROL Formula 2]**: `C/D`

>[!NOTE]
>
>Schakel het selectievakje `Multiple Y-Axes box` en `Hide` alle meetwaarden

![Producten geordend 2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### Gemiddelde orderwaarde

* **Beschrijving**: De gemiddelde waarde van de orders over een periode bijhouden. Met deze maatstaf kunt u snel bepalen hoe uw gemiddelde orderwaarde (AOV) is gewijzigd als gevolg van uw marketinginspanningen, productaanbod en/of andere wijzigingen in uw bedrijf.
* **Metrische definitie**: Deze maatstaf voert een **gemiddelde** van `grand_total` van `sales_flat_order` tabel geordend door `created_at`.
* **Voorbeeld van rapport**: AOV vs. vorig jaar, YTD
   * **[!UICONTROL Metric]**: `Average order value`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Perspective]**: `Amount Change vs Previous Year`

  ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### Producten die het meest met coupons worden gekocht

* **Beschrijving**: Dit rapport geeft inzicht in welke producten worden verkocht wanneer je aanbiedingen of coupons aanbiedt.
* **Metrisch gebruikt**: Geordende producten
* **Voorbeeld van rapport**: Producten die het meest met coupons worden gekocht
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Filter]**: `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By**]: `name` (of `SKU`of een andere productidentificatie)
   * **[!UICONTROL Show top/bottom]**: Top 25 gesorteerd op geordende producten

  ![Producten met coupons](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### Tijd tussen bestellingen

* **Beschrijving**: Test uw veronderstellingen en verwachtingen over de aankoopcycli van uw klanten met een **tijd tussen bestellingen** analyse die het gemiddelde (of mediaan!) bekijkt tijdsduur tussen aankopen. In de onderstaande grafiek ziet u dat uw beste klanten - die meer dan drie bestellingen plaatsen - hun tweede aankoop binnen minder dan zes maanden doen. Klanten die geen vierde bestelling hebben geplaatst, wachten veertien maanden voordat ze een tweede aankoop doen.
* **Metrische definitie**: Deze maatstaf voert een **gemiddelde** van `Time since previous order` van `sales_flat_order` geordend door `created_at`.
* **Voorbeeld van rapport**:
   * **Metrisch 1**: ≤ 3 orders
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders ≤ 3`
   * **Metrisch 2**: > 3 bestellingen
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>Schakel het selectievakje `Multiple Y-Axes` doos.

![Tijd tussen bestellingen](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## Analyse marketinguitgaven {#mktgspendanalytics}

### Advertentie-uitgaven

* **Beschrijving**: U kunt uw marketinguitgaven analyseren over verschillende tijdsperioden en intervallen, via campagnes of advertentiesets of andere segmentaties.
* **Metrische definitie**: Deze metrisch voert een Som op de uitgavenkolom in uit `Marketing Spend` tabel geordend door de `date` kolom.
* **Voorbeeld van rapport**: Toegestane uitgaven per campagne
   * **[!UICONTROL Metric]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `campaign`

![Advertentie-uitgaven](../../assets/ad_spend.png)<!--{: width="929"}-->

### Afbeeldingen toevoegen en klikken

* **Beschrijving**: Naast het analyseren en uitgeven, kunt u uw beelden analyseren en klikken.
* **Metrische definitie**: Deze metrisch voert een Som op de impressies (of klikt) kolom in uit `Marketing Spend` tabel geordend door de datumkolom.
* **Voorbeeld van rapport**: Afbeeldingen toevoegen en klikken op dag
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**: `By Day`

  ![Advertentie-impressies](../../assets/ad_impressions.png)<!--{: width="929"}-->

### Klikken-door-tarief (CTR)

* **Beschrijving**: Met behulp van de bovenstaande afbeeldingen en met de muis kunt u de klikdoorloop door verschillende campagnes in de loop der tijd analyseren.
* **Voorbeeld van rapport**: CTR via campagne
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * Selecteer `%` optie.
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>U kunt **titel** de formule als `CTR`, en **verbergen** alle meetwaarden.

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### Kosten per klik (CPC)

* **Beschrijving**: Met de advertentie die u hierboven hebt gemaakt en waarop u klikt, kunt u uw kosten per klik analyseren door verschillende campagnes in de loop van de tijd.
* **Voorbeeld van rapport**: CPC via campagne
   * **[!UICONTROL Metric A]**: `Ad spend`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `A/B`
   * Selecteer `currency` option
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>U kunt **titel** de formule als `CPC`, en **verbergen** alle meetwaarden.

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### Klanten op basis van aankoopbron

* **Beschrijving**: Als u de bron, het medium en de campagne van een bestelling bijhoudt met [!DNL Google eCommerce]kunt u uw klanten analyseren op basis van hun aankoopbron. Dit helpt u identificeren welke marketing bronnen klanten en antwoordvragen zoals &quot;zijn de meesten van uw klanten die hun eerste orden door maken [!DNL Google], [!DNL Facebook]of een andere bron?&quot;
* **Voorbeeld van rapport**: Klanten op basis van aankoopbron
   * **[!UICONTROL Metric Used]**: `New Customers`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's first order's source`

>[!NOTE]
>
>Uitchecken [dit artikel](../analysis/most-value-source-channel.md) voor meer voorbeelden van rapporten die de verwervingsbron gebruiken.

![Verwervingsbron](../../assets/acquisition_source.png)<!--{: width="929"}-->

### Klanten via aankoopmedium en acquisitiecampagne

* **Beschrijving**: Net als bij het analyseren van klanten op basis van de aankoopbron, kunt u ook uw klanten analyseren op basis van het medium en de campagne van hun eerste bestelling. Dit kan u helpen vragen zoals &quot;beantwoorden welke campagnes nieuwe klanten aantrekken?&quot;
* **Voorbeeld van rapport**: Klanten via acquisitiecampagne met betaalmiddel
   * **[!UICONTROL Metric Used]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>Voor het filter in uw `New Customers` metrisch, kunt u om het even welke andere media toevoegen die als &quot;betaalde&quot;media voor uw zaken zoals cpc of betaald onderzoek worden beschouwd.

![Aankoop normaal](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### Aanschafkosten (CAC) of kostprijs per aankoop (CPA)

* **Beschrijving**: Eén manier om de kosten van een campagne te analyseren, is door alle kosten toe te wijzen aan alleen de klanten die u via de campagne hebt aangeschaft.
* **Voorbeeld van rapport**: CAC via campagne
   * **[!UICONTROL Metric A]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Ad Spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * Selecteer `currency` option
   * **[!UICONTROL Group By]**:
      * Voor metrisch `A`, selecteert u `Customer's first order's campaign`
      * Voor metrisch `B`, selecteert u `campaign`

  ![Nieuwe gebruikers.](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>U kunt **titel** de formule als `CTR`, en **verbergen** alle meetwaarden. Ook uitchecken [dit artikel](../analysis/roi-ad-camp.md) voor meer informatie .

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### De waarde van het leven door aanschafbron, middel, en campagne

* **Beschrijving**: Naast het analyseren van het aantal klanten die door elke campagne worden verworven, kunt u de gemiddelde levenopbrengst van deze klanten analyseren. Zo kunt u beter identificeren:
   * Als bepaalde campagnes een groot aantal klanten aantrekken, maar die klanten hebben een lage levenwaarde.
   * Als bepaalde campagnes een laag volume van klanten aantrekken, maar die klanten hebben een hoge levenwaarde.
* **Voorbeeld van rapport**: Voeg eerst de `New customers` metrisch. Voeg vervolgens de `Average lifetime revenue` metrisch. Selecteer het gewenste tijdframe en kies de optie `interval` als `None`. Tot slot selecteert u `group by` optie als`Customer's first order's campaign`.
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>Voor de twee filters, kunt u andere media toevoegen die als &quot;betaalde&quot;media voor uw zaken (zoals cpc of betaalde onderzoek) worden beschouwd. U kunt ook andere bronnen toevoegen die u wilt analyseren, zoals Facebook. Uitchecken [dit artikel](../analysis/roi-ad-camp.md) voor meer informatie over CAC, LTV, en ROI.

![De waarde van het leven door aanschafbron, middel, en campagne](../../assets/LTV_2.png)<!--{: width="929"}-->

### Rendement van investeringen (ROI)

* **Beschrijving**: Één manier om ROI door campagne te berekenen is door alle orden te analyseren die door de campagne worden geplaatst. Nochtans, analyseert een alternatieve methode de levenwaarde van klanten die door een campagne worden verworven. Om ROI te analyseren, is het belangrijk dat de campagnemenamen over uw uitgavengegevens en transactionele gegevens verenigbaar zijn. Als u het volgende rapport maakt en er geen ROI-waarden zijn vanwege niet-overeenkomende campagnemenamen, moet u mogelijk naar de [UTM-tags](../../best-practices/utm-tagging-google.md) u hebt geïmplementeerd.
* **Voorbeeld van rapport**: ROI per campagne
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `(B-(C/A))/(C/A)`
   * Selecteer `% `option
   * **[!UICONTROL Group By]**:
      * Voor metrisch `A` en `B`, selecteert u `Customer's first order's campaign`
      * Voor metrisch `C`, selecteert u `campaign`

>[!NOTE]
>
>U kunt de formule een titel geven als &quot;ROI&quot; en alle metriek verbergen. Bovendien kunt u de filters in de metriek aanpassen om alternatieve bronnen en media te analyseren. Ook uitchecken [dit onderwerp](../analysis/roi-ad-camp.md) voor meer informatie over CAC, LTV, en ROI.

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
