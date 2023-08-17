---
title: Weergaven van Data Warehouse maken en gebruiken
description: Leer over een methode om nieuwe gestreken lijsten tot stand te brengen door een bestaande lijst te wijzigen, of het samenvoegen van of het consolideren van veelvoudige lijsten samen door SQL te gebruiken.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 9%

---

# Werken met weergaven van Data Warehouse

In dit document worden het doel en het gebruik van `Data Warehouse Views` toegankelijk door te navigeren naar **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Hieronder vindt u een uitleg van wat het doet en hoe u weergaven kunt maken, en een voorbeeld van hoe het moet worden gebruikt `Data Warehouse Views` consolideren [!DNL Facebook] en [!DNL AdWords] besteed gegevens.

## Algemeen doel

De `Data Warehouse Views` Deze functie is een methode om nieuwe geagendeerde tabellen te maken door een bestaande tabel te wijzigen of door meerdere tabellen samen te voegen of te consolideren met SQL. Eenmaal `Data Warehouse View` is gemaakt en verwerkt door een updatecyclus, wordt deze in uw Data Warehouse gevuld als een nieuwe tabel onder de `Data Warehouse Views` vervolgkeuzelijst, zoals hieronder weergegeven:

![](../../assets/Data_Warehouse.png)

Van hier, functioneert uw nieuwe mening zoals een andere lijst, die u de macht geven om nieuwe berekende kolommen tot stand te brengen of metriek en rapporten bovenop het te bouwen.

`Data Warehouse Views` worden hoofdzakelijk gebruikt om veelvoudige gelijkaardige maar ongelijke lijsten samen te verenigen, zodat al het melden op één enkele nieuwe lijst kan worden voortgebouwd. Enkele voorbeelden die veel voorkomen, zijn het consolideren van de tabellen vanuit een bestaande database en een live database om historische en huidige gegevens te combineren, of het combineren van meerdere advertentiebronnen zoals Facebook en AdWords tot één enkele `Consolidated ad spend` tabel.

Als u vertrouwd bent met SQL, gebruiken beide consolidatievoorbeelden `UNION` maar u kunt elke PostSQL-syntaxis en -functies gebruiken wanneer u een nieuwe weergave maakt.

## Weergaven van Data Warehouse maken en beheren

Nieuw `Data Warehouse Views` kan worden gemaakt en bestaande weergaven kunnen worden verwijderd door naar **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, zoals hieronder weergegeven:

![](../../assets/Data_Warehouse_Views.png)

Hier kunt u een weergave maken door de voorbeeldinstructies hieronder te volgen:

1. Als u een bestaande weergave wilt bekijken, klikt u op **[!UICONTROL New Data Warehouse View]** om een leeg vraagvenster te openen. Als er al een leeg queryvenster is geopend, gaat u verder met de volgende stap.
1. Geef de weergave een naam door in het dialoogvenster `View Name` veld. De hier opgegeven naam bepaalt de weergavenaam voor de weergave in de Data Warehouse. `View names` zijn beperkt tot kleine letters, cijfers en onderstrepingstekens (_). Alle andere tekens zijn verboden.
1. Voer uw query in het venster met de naam `Select Query`, met gebruik van de standaard PostSQL-syntaxis.

   >[!NOTE]
   >
   >Uw query moet verwijzen naar specifieke kolomnamen. Het gebruik van `*`niet toegestaan om alle kolommen te selecteren.

1. Als u klaar bent, klikt u op **[!UICONTROL Save]** om de weergave op te slaan. Je weergave bevat tijdelijk een `Pending` status tot deze wordt verwerkt door de volgende volledige updatecyclus, waarna de status verandert in `Active`. Nadat uw weergave door een update is verwerkt, kunt u deze gebruiken in rapporten.

Het is belangrijk om te vermelden dat na sparen, de onderliggende vraag wordt gebruikt om een te produceren `Data Warehouse View` kan niet worden bewerkt. Als u de structuur van een `Data Warehouse View`, moet u een mening tot stand brengen en manueel om het even welke berekende kolommen, metriek, of rapporten van de originele mening aan nieuwe migreren. Wanneer de migratie is voltooid, kunt u de oorspronkelijke weergave veilig verwijderen. Omdat `Data Warehouse Views` zijn niet bewerkbaar, raadt de Adobe u aan de uitvoer van uw query te testen met de opdracht `SQL Report Builder` voordat u de query opslaat als weergave Data Warehouse.

## Voorbeeld: [!DNL Facebook] en [!DNL Google AdWords] data

Kijk eens naar een van de voorbeelden die eerder in dit artikel worden genoemd: consolideren [!DNL Facebook] en [!DNL AdWords] besteed gegevens in een nieuwe geconsolideerde advertentietabel. Meestal gaat het hierbij om de consolidatie van twee tabellen, met de volgende voorbeeldgegevenssets:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

Eén advertentietabel maken met beide [!DNL Facebook] en [!DNL Google AdWords] campagnes, moet u een SQL vraag schrijven en gebruiken `UNION ALL` functie. A `UNION ALL` De instructie wordt meestal gebruikt om meerdere verschillende SQL-query&#39;s te combineren terwijl de resultaten van elke query aan één uitvoer worden toegevoegd.

Er zijn enkele vereisten voor een `UNION` instructies die de moeite van het vermelden waard zijn, zoals beschreven in PostgreSQL [documentatie](https://www.postgresql.org/docs/8.3/queries-union.html):

* Alle vragen moeten het zelfde aantal kolommen terugkeren
* Overeenkomende kolommen moeten identieke gegevenstypen hebben

Wanneer u een `UNION` of `UNION ALL` de naam van de kolommen in de uiteindelijke uitvoer weerspiegelt in de naam van de kolommen in de eerste query.

Gewoonlijk consolideert u uw [!DNL Facebook] en [!DNL Google AdWords] gegevens in een `Data Warehouse View` vereisen de verwezenlijking van een lijst met zeven kolommen, met een vraag gelijkend op hieronder:

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

Een paar belangrijke punten in verband met het bovenstaande:

* Voor de duidelijkheid worden alle kolommen hierboven gealiased zodat de namen overeenkomen met alle query&#39;s. Dit is echter geen vereiste. De orde waarin de kolommen in de UITGEZOCHTE vragen worden geroepen dicteert hoe zij op zijn.
* Een nieuwe kolom met de naam `ad_source` is gemaakt om het filteren voor [!DNL AdWords] of [!DNL Facebook] gegevens. Onthoud dat deze query alle gegevens uit beide tabellen combineert. Als u geen kolom zoals creeert `ad_source`Er is echter geen eenvoudige manier om de uitgaven van een bepaalde bron te identificeren.

De bovenstaande query opslaan als een `Data Warehouse View` maakt een tabel met beide [!DNL Facebook] en [!DNL AdWords] uitgaven, vergelijkbaar met de onderstaande uitgaven:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

In plaats van een aparte set marketingmeetgegevens voor elke advertentiebron te maken, kunt u slechts één set meetgegevens maken met de bovenstaande tabel om al uw advertenties vast te leggen.

**Op zoek naar extra hulp?**

SQL schrijven en maken `Data Warehouse Views` wordt niet meegeleverd bij Technische ondersteuning. De [Services-team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) biedt wel hulp bij het oprichten van standpunten . Voor alles van het migreren van een erfenisgegevensbestand met een nieuw gegevensbestand om één enkele Mening van de Data Warehouse voor een specifieke analyse tot stand te brengen, kan het ondersteuningsteam helpen.

Gewoonlijk wordt een nieuwe `Data Warehouse View` voor de consolidatie van 2-3 vergelijkbare gestructureerde tabellen is vijf uur aan diensttijd nodig, wat neerkomt op ongeveer $1.250 aan werk. Hieronder volgen echter een aantal gemeenschappelijke factoren die de verwachte vereiste investeringen kunnen doen toenemen:

* Consolidatie van meer dan drie tabellen in één weergave
* Weergave van meerdere Data Warehouse maken
* Complexe samenvoegende logica of filtervoorwaarden
* Consolidatie van twee of meer tabellen met ongelijke gegevensstructuren
