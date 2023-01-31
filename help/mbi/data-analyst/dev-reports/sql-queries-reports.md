---
title: SQL-query's omzetten in [!DNL MBI] rapporten
description: Leer hoe SQL de vragen in berekende kolommen worden vertaald, metriek u binnen gebruikt [!DNL MBI].
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# SQL-query&#39;s vertalen in MBI

ooit vroeg zich af hoe SQL-query&#39;s vertaald worden in de [berekende kolommen](../data-warehouse-mgr/creating-calculated-columns.md), [cijfers](../../data-user/reports/ess-manage-data-metrics.md), en [rapporten](../../tutorials/using-visual-report-builder.md) u gebruikt in [!DNL MBI]? Als u een zware SQL-gebruiker bent, begrijpen hoe SQL wordt vertaald in [!DNL MBI] kunt u slimmer werken in de [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) en het beste uit de [!DNL MBI] platform.

Aan het einde van dit artikel hebben we een **vertaalmatrix** voor SQL-queryclausules en [!DNL MBI] elementen.

We beginnen met een algemene query:

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | Rapport `group by` |
| `SUM(b)` | `Aggregate function` (kolom) |
| `FROM c` | `Source` table |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Rapport `time frame` |
| `GROUP BY a` | Rapport `group by` |

In dit voorbeeld worden de meeste gevallen van vertaling behandeld, maar er zijn enkele uitzonderingen. Laten we induiken, te beginnen met hoe de `aggregate` functie is omgezet.

## Samengevoegde functies

Samengevoegde functies (bijvoorbeeld `count`, `sum`, `average`, `max`, `min`) bij vragen in de vorm van **metrische aggregaten** of **kolomaggregaties** in [!DNL MBI]. De differentiërende factor is al dan niet een verbinding wordt vereist om de samenvoeging uit te voeren.

Laten we een voorbeeld nemen voor elk van de bovenstaande punten.

## Metrische aggregaten {#aggregate}

Metrisch is vereist bij aggregatie `within a single table`. Bijvoorbeeld de `SUM(b)` de gezamenlijke functie van de vraag hierboven zou hoogstwaarschijnlijk door metrisch worden vertegenwoordigd die kolom sommen `B`. 

Laten we eens kijken naar een concreet voorbeeld van hoe een `Total Revenue` Metrisch kan worden gedefinieerd in [!DNL MBI]. Kijk hieronder naar de vraag die we zullen proberen te vertalen:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (kolom) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrisch `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Metrisch `timestamp` (en rapportage `time range`) |

Navigeren naar de metrische bouwer door te klikken **[!UICONTROL Manage Data** > ** Metrisch **> **Nieuwe metrisch maken]**, moeten wij eerst de juiste `source` de tabel, die in dit geval de `orders` tabel. Dan zou metrisch opstelling zoals hieronder getoond zijn:

![Metrische aggregatie](../../assets/Metric_aggregation.png)

## Kolomaggregaties

Een berekende kolom wordt vereist wanneer het samenvoegen van een kolom die van een andere lijst wordt aangesloten. U kunt bijvoorbeeld een kolom in uw `customer` table called `Customer LTV`, die de totale waarde opsommen van alle orders die aan die klant in de `orders` tabel.

De query voor deze aggregatie kan er ongeveer als volgt uitzien:

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | Geaggregeerde eigenaar |
| `SUM(o.order_total) as "Customer LTV"` | Samengevoegde bewerking (kolom) |
| `FROM customers c` | Aggregate owner table |
| `JOIN orders o` | Aggregatiebrontabel |
| `ON c.customer_id = o.customer_id` | Pad |
| `WHERE o.status = 'success'` | Samenvoegen, filter |

Deze instelling instellen in [!DNL MBI] vereist het gebruik van uw manager van de Data Warehouse, waar u een weg tussen uw zult bouwen `orders` en `customers` tabel maakt vervolgens een nieuwe kolom met de naam `Customer LTV` in de tabel van uw klant.

Laten we eerst eens bekijken hoe we een nieuwe weg kunnen inslaan tussen de `customers` en `orders`. Ons einddoel is een nieuwe samengevoegde kolom te maken in de `customers` tabel, dus navigeer eerst naar de `customers` tabel in uw Data Warehouse en klik vervolgens op **[!UICONTROL Create a Column** > ** Een definitie selecteren **> **SUM]**.

Vervolgens moet u de brontabel selecteren. Als er al een pad bestaat naar uw `orders` in de vervolgkeuzelijst. Als u echter een nieuw pad maakt, klikt u op **[!UICONTROL Create new path]** en u wordt hieronder met het scherm weergegeven:

![Nieuw pad maken](../../assets/Create_new_path.png)

Hier moet u zorgvuldig het verband tussen de twee lijsten overwegen u probeert samen te voegen. In dit geval kunnen er `Many` orders gekoppeld aan `One` de `orders` tabel staat in de lijst `Many` aan de `customers` tabel geselecteerd op `One` zijde.

>[!NOTE]
>
>In [!DNL MBI], *pad* is gelijk aan `Join` in SQL.

Nadat het pad is opgeslagen, kunt u het nieuwe pad maken `Customer LTV` kolom! Kijk hieronder naar:

![](../../assets/Customer_LTV.gif)

Nu hebt u de nieuwe `Customer LTV` kolom in uw `customers` tabel, kunt u een [metrische aggregatie](#aggregate) door deze kolom te gebruiken (bijvoorbeeld om de gemiddelde LTV per klant te vinden) of eenvoudig `group by` of `filter` door de berekende kolom in een rapport gebruikend bestaande metriek die op wordt voortgebouwd `customers` tabel.

>[!NOTE]
>
>Voor laatstgenoemde, om het even welke tijd u een nieuwe berekende kolom bouwt zult u moeten [de dimensie toevoegen aan bestaande metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) voordat het als `filter` of `group by`.

Zie [berekende kolommen maken](../data-warehouse-mgr/creating-calculated-columns.md) met uw Data Warehouse manager.

## `Group By` clausules

`Group By` functies in query&#39;s worden vaak weergegeven in [!DNL MBI] als kolom die wordt gebruikt om een visueel rapport te segmenteren of te filteren. Als voorbeeld kunnen we de `Total Revenue` query die we eerder hebben onderzocht, maar deze keer laten we de inkomsten segmenteren door de `coupon\_code` om beter te begrijpen welke coupons de meeste inkomsten genereren.

Eerst beginnen we met de onderstaande query:

|  |  |
|--- |--- |
| `SELECT coupon_code,` | Rapport `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(kolom) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrisch `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Metrisch `timestamp` (en rapportage `time range`) |
| `GROUP BY coupon_code` | Rapport `group by` |

>[!NOTE]
>
>Het enige verschil met de query waarmee we eerder zijn begonnen, is de toevoeging van de &#39;coupon\_code&#39; als groep door._

Hetzelfde gebruiken `Total Revenue` We zijn nu klaar om ons rapport met inkomsten te maken dat is gesegmenteerd door couponcode. Bekijk een blik bij gif hieronder dat toont hoe te opstelling dit visuele rapport die gegevens van september tot november bekijkt:

![Opbrengsten per couponcode](../../assets/Revenue_by_coupon_code.gif)

## Formulas

In sommige gevallen, kan een vraag veelvoudige samenvoegingen impliceren om het verband tussen afzonderlijke kolommen te berekenen. U kunt bijvoorbeeld op twee manieren de gemiddelde orderwaarde in een query berekenen:

* `AVG('order\_total')` OF
* `SUM('order\_total')/COUNT('order\_id')`

De eerste methode zou de creatie van een nieuwe metrieke omvatten die een gemiddelde op de `order\_total` kolom. Nochtans kon de laatstgenoemde methode direct in de rapportbouwer worden gecreeerd veronderstellend u reeds metriek opstelling hebt om te berekenen `Total Revenue` en `Number of orders`.

Laten we een stap terug doen en kijken naar de algemene vraag naar `Average order value`:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Metrisch `operation` (kolom) |
| `COUNT(order_id) as "Number of orders"` | Metrisch `operation` (kolom) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Metrisch `operation` (kolom) / Metrische bewerking (kolom) |
| `FROM orders` | Metrisch `source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrisch `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Metrische tijdstempel (en tijdbereik van rapportage) |

En laten we er ook van uitgaan dat we al metriek hebben opgezet om de `Total Revenue` en `Number of orders`. Aangezien deze gegevens al bestaan, kunnen we de `Report Builder` en maak een ad-hocberekening met behulp van de `Formula` functie:

![AOV forumula](../../assets/AOV_forumula.gif)

## Omloop omhoog

Zoals we aan het begin van dit artikel hebben vermeld, als u een zware SQL-gebruiker bent, die nadenkt over hoe query&#39;s worden vertaald in [!DNL MBI] Hiermee kunt u berekende kolommen, metriek en rapporten maken.

Voor een snelle referentie kunt u de onderstaande matrix uitchecken. Dit toont het equivalent van een SQL-component [!DNL MBI] element en hoe het aan meer dan één element kan in kaart brengen, afhankelijk van hoe het in de vraag wordt gebruikt.

## MBI Elements

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| |—|—|—|—|—|—|—|—|—| |`SELECT`|X|-|X|-|-|X|-|- |`FROM`|-|-|-|-|-|-|X| |`WHERE`|-|X|-|-|-|-|-|-|- |`WHERE` (met tijdelementen)|-|-|-|X|-|-|-|- |`JOIN...ON`|-|X|-|-|X|X|-| |`GROUP BY`|-|-|X|-|-|-|-|-|
