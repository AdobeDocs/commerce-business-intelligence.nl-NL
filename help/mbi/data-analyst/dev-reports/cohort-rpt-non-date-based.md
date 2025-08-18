---
title: Cohort Report Builder for Non-Date Based Cohorts
description: Leer gebruikers te groeperen door een gelijkaardige activiteit of een attribuut.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] voor Cohorts die niet op datum zijn gebaseerd

[`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) is ideaal om handelaren te helpen onderzoeken hoe verschillende subsets van gebruikers zich in de loop der tijd gedragen. In het verleden is `Cohort Report Builder` geoptimaliseerd voor het groeperen van gebruikers door een algemene `cohort date` (bijvoorbeeld de set van alle klanten die hun eerste aankoop in een bepaalde maand hebben gedaan). Met de functie `Non-Date Based Cohort` kunt u nu gebruikers groeperen op basis van een vergelijkbare activiteit of een vergelijkbaar kenmerk. Bekijk een paar gebruiksgevallen voor deze functie.

## Gevallen gebruiken

Dit is geen uitgebreide lijst, maar er zijn enkele potentiële analyses die met deze functie kunnen worden uitgevoerd.

* De inkomsten van klanten controleren die zijn aangeschaft vanuit [!DNL Google] versus [!DNL Facebook]
* Klanten wier eerste aankoop in de VS en Canada is gedaan, analyseren
* Kijken naar het gedrag van klanten die via verschillende advertentiecampagnes zijn aangeschaft

## Hoe te om Uw Analyse te creëren

1. Klik op **[!UICONTROL Report Builder]** op het linkertabblad of op **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. Klik in het `Report Builder Selection` -scherm op **[!UICONTROL Create Report]** naast de optie `Visual Report Builder` .

### Metrisch toevoegen

Nu u in `Report Builder` bent, voegt u metrisch toe dat u de analyse wilt uitvoeren (bijvoorbeeld: `Revenue` of `Orders`).

>[!NOTE]
>
>Eigen [!DNL Google Analytics] metriek zijn niet compatibel met `Cohort Report Builder` . Het doel voor dit voorbeeld is om na verloop van tijd te kijken naar de inkomsten van klanten van de eerste bestelling die via verschillende [!DNL Google Analytics] -bronnen zijn aangeschaft.

### Schakelen `Metric View` naar `Cohort`

![ 1 - knevel metrische mening om te cohort ](../../assets/1-toggle-metric-view-to-cohort.png)

Dit opent omhoog een nieuw venster waar u de details van het Rapport van het Cohort kunt vormen.

Er zijn vijf specificaties nodig om een verslag van Cohort op te stellen:

1. De cohorten groeperen
1. Cohorten selecteren
1. Tijdstempel voor handeling
1. Tijdbereik eerste handeling van Cohort
1. Tijdbereik na cohort-instantie

![ cohort-groepen ](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### &#x200B;1. Groeperen `cohorts`

`Cohorts` worden gegroepeerd op een gedragskenmerk, in dit voorbeeld `Customer's first order GA source` . De hier beschikbare opties zijn kolommen die al als `groupable` voor metrisch zijn aangewezen.

#### &#x200B;2. Cohorten selecteren

U kunt alle resultaten voor het gegeven kenmerk tonen. Omdat dit veel `cohorts` kan opleveren, kunt u de specifieke `cohorts` (die overeenkomt met de verschillende waarden die beschikbaar zijn voor `Customer's first order GA source` ) selecteren die u nodig hebt.

![ cohort-groepen ](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

Dit staat u toe om een op datum-gebaseerde kolom buiten de kolom te kiezen waarop metrisch wordt gecreeerd. Hieronder ziet u hoe u het tijdbereik selecteert dat van toepassing is op de opgegeven `action timestamp` .

#### 4. `Cohort first action time range`

Hier is waar u de datumwaaier selecteert die `cohorts action timestamp` bevat (zo, klanten die de eerste orde van november 2017 tot Oktober 2018 hadden). Dit kan een bewegend datumbereik of een vast datumbereik zijn.

#### 5. `Time range after cohort occurrence`

Wilt u de `cohorts` in de loop van de tijd per maand, week of jaar zien? Hier maakt u deze selecties. Onder die sectie selecteert u de `time range` nadat `cohort action timestamp` is opgetreden. Bijvoorbeeld, toont dit u 12 maanden van gegevens voor de klanten die de eerste orde tijdens de waaier van de actietermijn plaatsten.

![ cohort-eerste-actie-tijd-waaier ](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] die op uw metriek wordt toegepast, blijft intact wanneer u schakelt tussen de weergaven `Standard` en `Cohort` .

### Verwante

Zie [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md) .
