---
title: Weergaven van Data Warehouse maken en gebruiken
description: Leer over een methode om nieuwe gestreken lijsten tot stand te brengen door een bestaande lijst te wijzigen, of het samenvoegen van of het consolideren van veelvoudige lijsten samen door SQL te gebruiken.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 6%

---

# Werken met weergaven van Data Warehouse

In dit document worden het doel en het gebruik van `Data Warehouse Views` dat toegankelijk is, beschreven door naar **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]** te navigeren. Hieronder vindt u een uitleg van wat het doet en hoe u weergaven kunt maken. Ook ziet u hoe u `Data Warehouse Views` kunt gebruiken om [!DNL Facebook] -gegevens te consolideren en [!DNL AdWords] om gegevens uit te geven.

## Algemeen doel

De functie `Data Warehouse Views` is een methode om nieuwe geagendeerde tabellen te maken door een bestaande tabel te wijzigen of door meerdere tabellen samen te voegen of te consolideren met SQL. Nadat een `Data Warehouse View` is gemaakt en verwerkt door een updatecyclus, wordt het in uw Data Warehouse gevuld als een nieuwe tabel onder het vervolgkeuzemenu `Data Warehouse Views` , zoals hieronder wordt getoond:

![](../../assets/Data_Warehouse.png)

Van hier, functioneert uw nieuwe mening zoals een andere lijst, die u de macht geven om nieuwe berekende kolommen tot stand te brengen of metriek en rapporten bovenop het te bouwen.

`Data Warehouse Views` worden vooral gebruikt om meerdere vergelijkbare maar verschillende tabellen samen te voegen, zodat alle rapporten op één nieuwe tabel kunnen worden gebaseerd. Enkele voorbeelden die veel voorkomen, zijn het consolideren van de tabellen vanuit een bestaande database en een live database om historische en huidige gegevens te combineren, of het combineren van meerdere advertentiebronnen zoals Facebook en AdWords in een enkelvoudige `Consolidated ad spend` tabel.

Als u bekend bent met SQL, gebruiken beide consolidatievoorbeelden de `UNION` functie, maar u kunt om het even welke syntaxis en functies gebruiken PostgreSQL wanneer het bouwen van een nieuwe mening.

## Weergaven van Data Warehouse maken en beheren

U kunt nieuwe `Data Warehouse Views` maken en bestaande weergaven verwijderen door naar **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]** te navigeren, zoals hieronder wordt getoond:

![](../../assets/Data_Warehouse_Views.png)

Hier kunt u een weergave maken door de voorbeeldinstructies hieronder te volgen:

1. Als u een bestaande weergave observeert, klikt u op **[!UICONTROL New Data Warehouse View]** om een leeg queryvenster te openen. Als er al een leeg queryvenster is geopend, gaat u verder met de volgende stap.
1. Geef de weergave een naam door in het veld `View Name` te typen. De hier opgegeven naam bepaalt de weergavenaam voor de weergave in de Data Warehouse. `View names` zijn beperkt tot kleine letters, cijfers en onderstrepingstekens (_). Alle andere tekens zijn verboden.
1. Voer uw query in het venster met de naam `Select Query` in met de standaardsyntaxis van PostgreSQL.

   >[!NOTE]
   >
   >Uw query moet verwijzen naar specifieke kolomnamen. Het gebruik van het `*` karakter om alle kolommen te selecteren wordt niet toegestaan.

1. Als u klaar bent, klikt u op **[!UICONTROL Save]** om de weergave op te slaan. Uw weergave heeft tijdelijk de status `Pending` totdat deze wordt verwerkt door de volgende volledige updatecyclus, waarna de status verandert in `Active` . Nadat uw weergave door een update is verwerkt, kunt u deze gebruiken in rapporten.

Het is belangrijk om te vermelden dat de onderliggende query die wordt gebruikt om een `Data Warehouse View` te genereren, na het opslaan niet kan worden bewerkt. Als u de structuur van een `Data Warehouse View` moet aanpassen, moet u een mening tot stand brengen en manueel om het even welke berekende kolommen, metriek, of rapporten van de originele mening aan nieuwe migreren. Wanneer de migratie is voltooid, kunt u de oorspronkelijke weergave veilig verwijderen. Omdat `Data Warehouse Views` niet bewerkbaar zijn, raadt de Adobe u aan de uitvoer van uw query te testen met de `SQL Report Builder` voordat u de query opslaat als een weergave voor Data Warehouse.

## Voorbeeld: [!DNL Facebook] en [!DNL Google AdWords] data

Bekijk een van de voorbeelden die eerder in dit artikel worden genoemd, nader: [!DNL Facebook] consolideren en [!DNL AdWords] gegevens doorgeven in een nieuwe geconsolideerde tabel voor advertenties. Meestal gaat het hierbij om de consolidatie van twee tabellen, met de volgende voorbeeldgegevenssets:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00 :00: 00 | 2000 | 10,2 |
| 2 | ggg | 40 | 2017-05-23 00 :00: 00 | 900 | 4,6 |
| 3 | aaa | 22 | 2017-06-12 00 :00: 00 | 400 | 2,5 |
| 4 | eee | 350 | 2017-06-30 00 :00: 00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00 :00: 00 | 10200 | 28,5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00 :00: 00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00 :00: 00 | 800 | 2,5 |
| 3 | aaa | 40 | 2017-05-22 00 :00: 00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00 :00: 00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00 :00: 00 | 300 | 1,2 |

Als u één advertentietabel wilt maken die zowel [!DNL Facebook] als [!DNL Google AdWords] -campagnes bevat, moet u een SQL-query schrijven en de functie `UNION ALL` gebruiken. Een instructie `UNION ALL` wordt meestal gebruikt om meerdere verschillende SQL-query&#39;s te combineren terwijl de resultaten van elke query aan één uitvoer worden toegevoegd.

Er zijn een paar vereisten van a `UNION` verklaring vermeldend, zoals die in de [ documentatie ](https://www.postgresql.org/docs/8.3/queries-union.html) wordt geschetst PostgreSQL:

* Alle vragen moeten het zelfde aantal kolommen terugkeren
* Overeenkomende kolommen moeten identieke gegevenstypen hebben

Wanneer u een instructie `UNION` of `UNION ALL` uitvoert, weerspiegelen de namen van de kolommen in de uiteindelijke uitvoer de naamgeving van de kolommen in de eerste query.

Doorgaans moet voor het consolideren van uw [!DNL Facebook] - en [!DNL Google AdWords] gegevens in een `Data Warehouse View` -bestand een tabel met zeven kolommen worden gemaakt, met een query zoals hieronder:

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
* Er wordt een nieuwe kolom met de naam `ad_source` gemaakt, zodat u gemakkelijker kunt filteren op [!DNL AdWords] - of [!DNL Facebook] -gegevens. Onthoud dat deze query alle gegevens uit beide tabellen combineert. Als u geen kolom zoals `ad_source` creeert, is er geen gemakkelijke manier om uitgaven van een bepaalde bron te identificeren.

Als u de bovenstaande query opslaat als een `Data Warehouse View` , wordt een tabel gemaakt met [!DNL Facebook] en [!DNL AdWords] gebruikt, vergelijkbaar met het onderstaande:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00 :00: 00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00 :00: 00 | eee | 10,2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00 :00: 00 | ddd | 2,5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00 :00: 00 | ggg | 4,6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00 :00: 00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00 :00: 00 | aaa | 2,5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00 :00: 00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00 :00: 00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00 :00: 00 | ccc | 1,2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00 :00: 00 | fff | 28,5 | 10200 | 280 |

In plaats van een aparte set marketingmeetgegevens voor elke advertentiebron te maken, kunt u slechts één set meetgegevens maken met de bovenstaande tabel om al uw advertenties vast te leggen.

**zoekend extra hulp?**

Het schrijven van SQL en het creëren van `Data Warehouse Views` is niet inbegrepen met Technische Steun. Nochtans, biedt het [ team van de Diensten ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) hulp in de verwezenlijking van meningen aan. Voor alles van het migreren van een erfenisgegevensbestand met een nieuw gegevensbestand om één enkele Mening van de Data Warehouse voor een specifieke analyse tot stand te brengen, kan het ondersteuningsteam helpen.

Gewoonlijk duurt het maken van een nieuwe `Data Warehouse View` voor het consolideren van 2-3 vergelijkbare gestructureerde tabellen vijf uur aan servicetijd, wat neerkomt op ongeveer $1.250 aan werk. Hieronder volgen echter een aantal gemeenschappelijke factoren die de verwachte vereiste investeringen kunnen doen toenemen:

* Consolidatie van meer dan drie tabellen in één weergave
* Weergave van meerdere Data Warehouse maken
* Complexe samenvoegende logica of filtervoorwaarden
* Consolidatie van twee of meer tabellen met ongelijke gegevensstructuren
