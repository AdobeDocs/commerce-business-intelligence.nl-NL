---
title: SQL-query's omzetten in Commerce Intelligence-rapporten
description: Leer hoe SQL de vragen in de berekende kolommen, metriek worden vertaald u in Commerce Intelligence gebruikt.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# SQL-query&#39;s vertalen in Commerce Intelligence

Heb zich ooit afgevraagd hoe SQL de vragen in de [ berekende kolommen ](../data-warehouse-mgr/creating-calculated-columns.md), [ metriek ](../../data-user/reports/ess-manage-data-metrics.md) worden vertaald, en [ rapporten ](../../tutorials/using-visual-report-builder.md) u gebruikt in [!DNL Commerce Intelligence]? Als u een zware SQL gebruiker bent, laat het begrip hoe SQL in [!DNL Commerce Intelligence] wordt vertaald u toe om slimmer in de [ Manager van Data Warehouse ](../data-warehouse-mgr/tour-dwm.md) te werken en de meesten uit het [!DNL Commerce Intelligence] platform te krijgen.

Aan het eind van dit onderwerp, vindt u a **vertaalmatrijs** voor SQL vraagclausules en [!DNL Commerce Intelligence] elementen.

Begin door een algemene vraag te bekijken:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Rapport `group by` |
| `SUM(b)` | `Aggregate function` (kolom) |
| `FROM c` | `Source` table |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Rapport `time frame` |
| `GROUP BY a` | Rapport `group by` |

In dit voorbeeld worden de meeste gevallen van vertaling behandeld, maar er zijn enkele uitzonderingen. Induiken, te beginnen met hoe de functie `aggregate` wordt vertaald.

## Samengevoegde functies

De samengevoegde functies (bijvoorbeeld, `count`, `sum`, `average`, `max`, `min`) in vragen nemen of de vorm van **metrische samenvoegingen** of **kolomsamenvoegingen** in [!DNL Commerce Intelligence]. De differentiërende factor is of een verbinding wordt vereist om de samenvoeging uit te voeren.

Bekijk een voorbeeld voor elk van bovenstaande.

## Metrische aggregaten {#aggregate}

Er is metrische waarde vereist bij het samenvoegen van `within a single table` . De `SUM(b)` statistische functie van de bovenstaande query wordt dus hoogstwaarschijnlijk vertegenwoordigd door een metrische functie die de kolom `B` sommen. 

Bekijk een specifiek voorbeeld van hoe een `Total Revenue` metrisch in [!DNL Commerce Intelligence] zou kunnen worden bepaald. Bekijk de query hieronder die u probeert te vertalen:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (kolom) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrisch `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Metrisch `timestamp` (en rapportering `time range`) |

Navigeer aan de metrische bouwer door **[!UICONTROL Manage Data** > ** Metriek **te klikken > **creeer Nieuwe Metrisch]**, moet u eerst de aangewezen `source` lijst selecteren, die in dit geval de `orders` lijst is. Dan zou metrisch opstelling zoals hieronder getoond zijn:

![ Metrische samenvoeging ](../../assets/Metric_aggregation.png)

## Kolomaggregaties

Een berekende kolom wordt vereist wanneer het samenvoegen van een kolom die van een andere lijst wordt aangesloten. U hebt bijvoorbeeld een kolom in de tabel `customer` met de naam `Customer LTV` ingebouwd, die de totale waarde van alle orders die aan die klant zijn gekoppeld in de tabel `orders` opsomt.

De query voor deze aggregatie kan er ongeveer als volgt uitzien:

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | Geaggregeerde eigenaar |
| `SUM(o.order_total) as "Customer LTV"` | Samengevoegde bewerking (kolom) |
| `FROM customers c` | Aggregate owner table |
| `JOIN orders o` | Aggregatiebrontabel |
| `ON c.customer_id = o.customer_id` | Pad |
| `WHERE o.status = 'success'` | Samenvoegen, filter |

Voor het instellen van deze instelling in [!DNL Commerce Intelligence] is het gebruik van uw Data Warehouse-manager vereist. Hierbij maakt u een pad tussen uw `orders` - en `customers` -tabel en maakt u vervolgens een kolom met de naam `Customer LTV` in de tabel van uw klant.

Bekijk hoe u een nieuw pad kunt maken tussen de `customers` en `orders` . Het einddoel is een nieuwe bijeengevoegde kolom in de `customers` lijst tot stand te brengen, zodat navigeer eerst aan de `customers` lijst in uw Data Warehouse, dan klik **[!UICONTROL Create a Column** > ** selecteer een definitie **> **SUM]**.

Vervolgens moet u de brontabel selecteren. Als er een pad naar de `orders` -tabel bestaat, selecteert u dit in de vervolgkeuzelijst. Als u echter een nieuw pad maakt, klikt u op **[!UICONTROL Create new path]** en ziet u hieronder het scherm:

![ creeer nieuwe weg ](../../assets/Create_new_path.png)

Hier moet u zorgvuldig het verband tussen de twee lijsten overwegen u probeert om zich aan te sluiten. In dit geval zijn er potentieel `Many` bestellingen gekoppeld aan `One` customer. De tabel `orders` wordt daarom vermeld aan de `Many` side, terwijl de tabel `customers` geselecteerd aan de `One` side.

>[!NOTE]
>
>In [!DNL Commerce Intelligence] is een `path` gelijk aan een `Join` in SQL.

Nadat het pad is opgeslagen, kunt u de kolom `Customer LTV` maken! Zie hieronder:

![](../../assets/Customer_LTV.gif)

Nu u de nieuwe `Customer LTV` kolom in uw `customers` lijst hebt gebouwd, bent u bereid om a [ metrische samenvoeging ](#aggregate) te creëren gebruikend deze kolom (bijvoorbeeld, om gemiddelde LTV per klant te vinden). U kunt ook `group by` of `filter` door de berekende kolom in een rapport gebruiken gebruikend bestaande metriek die op de `customers` lijst wordt voortgebouwd.

>[!NOTE]
>
>Voor laatstgenoemde, wanneer u een nieuwe berekende kolom bouwt moet u [ de afmeting aan bestaande metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toevoegen alvorens het als a `filter` of `group by` beschikbaar is.

Zie [ het creëren van berekende kolommen ](../data-warehouse-mgr/creating-calculated-columns.md) met uw Manager van Data Warehouse.

## `Group By` clausules

`Group By` functies in query&#39;s worden vaak in [!DNL Commerce Intelligence] weergegeven als een kolom die wordt gebruikt om een visueel rapport te segmenteren of te filteren. Laten we bijvoorbeeld terugkeren naar de query van `Total Revenue` die u eerder hebt verkend, maar deze keer segmenteert u de inkomsten van `coupon\_code` om beter te begrijpen welke coupons de meeste inkomsten genereren.

Begin met de onderstaande query:

| | |
|--- |--- |
| `SELECT coupon_code,` | Rapport `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (column) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrisch `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Metrisch `timestamp` (en rapportering `time range`) |
| `GROUP BY coupon_code` | Rapport `group by` |

>[!NOTE]
>
>Het enige verschil met de query waarmee u eerder bent begonnen, is de toevoeging van de &#39;coupon\_code&#39; als groep door._

Met dezelfde `Total Revenue` metrische code die u eerder hebt gemaakt, kunt u nu uw rapport maken met inkomsten die zijn gesegmenteerd door couponcode! Kijk hieronder naar de gif die toont hoe te opstelling dit visuele rapport die gegevens van september tot november bekijkt:

![ Ontvangsten door couponcode ](../../assets/Revenue_by_coupon_code.gif)

## Formulas

Soms, kan een vraag veelvoudige samenvoegingen impliceren om het verband tussen afzonderlijke kolommen te berekenen. U kunt bijvoorbeeld op twee manieren de gemiddelde orderwaarde in een query berekenen:

* `AVG('order\_total')` OR
* `SUM('order\_total')/COUNT('order\_id')`

De eerste methode zou het maken van een nieuwe metrische waarde omvatten, die een gemiddelde voor de kolom `order\_total` uitvoert. De laatste methode kan echter rechtstreeks in de rapportbuilder worden gemaakt, ervan uitgaande dat u al metriek hebt ingesteld om de `Total Revenue` en `Number of orders` te berekenen.

Neem een stap terug en bekijk de algemene vraag voor `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Metrisch `operation` (kolom) |
| `COUNT(order_id) as "Number of orders"` | Metrisch `operation` (kolom) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Metrisch `operation` (kolom) / Metrisch (kolom) |
| `FROM orders` | Metrisch `source` tabel |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrisch `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Metrische tijdstempel (en tijdbereik van rapportage) |

Stel nu dat u al metriek hebt ingesteld om de `Total Revenue` en `Number of orders` te berekenen. Aangezien deze meetgegevens bestaan, kunt u de `Report Builder` openen en een berekening op aanvraag maken met de functie `Formula` :

![ AOV forumula ](../../assets/AOV_forumula.gif)

## Omloop omhoog

Als u een zware SQL-gebruiker bent en nadenkt over de manier waarop query&#39;s in [!DNL Commerce Intelligence] worden vertaald, kunt u berekende kolommen, metriek en rapporten maken.

Voor een snelle referentie kunt u de onderstaande matrix uitchecken. Dit toont het equivalente [!DNL Commerce Intelligence] element van een SQL clausule en hoe het aan meer dan één element in kaart kan brengen, afhankelijk van hoe het in de vraag wordt gebruikt.

## Commerce Intelligence Elements

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (met tijdelementen) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
