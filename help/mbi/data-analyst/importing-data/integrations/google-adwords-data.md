---
title: Google Adwords-gegevens verwacht
description: Leer hoe u de Manager van de Data Warehouse kunt gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# [!DNL Google Adwords] gegevens verwacht

Nadat [ u uw  [!DNL Google Adwords]  rekening ](../integrations/google-adwords.md) hebt verbonden, kunt u de [ Manager van de Data Warehouse ](../../data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.

Daar, merkt u twee lijsten beschikbaar voor replicatie in uw Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

De `campaigns` lijst *zou door gebrek* moeten worden gebruikt, zodat kunt u beginnen door alle relevante gebieden van die lijst te synchroniseren.

De tabel `adwords` bevat vier kolommen die niet in de tabel `campaigns` staan:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Wanneer u geïnteresseerd bent in het uitvoeren van een analyse waarin deze kenmerken in aanmerking worden genomen, moet u de tabel `adwords` gebruiken.

>[!IMPORTANT]
>
>In deze tabel worden rijen uitgesloten waarvan alle vier deze kolommen `null` zijn.

Hieronder ziet u het verwachte schema voor beide tabellen.

## [!DNL Campaigns] table

De tabel `campaigns` bevat de volgende kolommen:

| **Kolom** | **Beschrijving** |
|-----|-----|
| `\_id` | De primaire sleutel voor de tabel |
| `accountId` | De account-id |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totaal aantal klikken voor de dag |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Totale kosten van de campagne voor de dag |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Campagne-id |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | De naam van de campagne (bijvoorbeeld, [ utm \_campagne ](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | De datum waarop de campagne is gestart |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Aantal indrukken voor de dag |
| `profileId` | Profiel-id |
| `profileName` | De profielnaam |
| `\_updated\_at` | De datum en tijd van de laatste update voor deze rij |

{style="table-layout:auto"}

## [!DNL AdWords] table

De tabel `adwords` bevat de volgende kolommen:

| **Kolom** | **Beschrijving** |
|-----|-----|
| `\_id` | De primaire sleutel voor de tabel |
| `accountId` | De account-id |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totaal aantal klikken voor de dag |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Totale kosten van de campagne voor de dag |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Campagne-id |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | De naam van de campagne (bijvoorbeeld, [ utm \_campagne ](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | De datum waarop de campagne is gestart |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Aantal indrukken voor de dag |
| `profileId` | Profiel-id |
| `profileName` | De profielnaam |
| `\_updated\_at` | De datum en tijd van de laatste update voor deze rij |
| `keyword` | Het sleutelwoord van de campagne |
| `adContent` | De eerste regel van de tekst voor de online campagne |
| `adDestinationUrl` | De URL waarnaar de [!DNL Adwords] verwijst, verwijst naar verkeer |
| `adGroup` | De naam van de ad-groep [!DNL Adwords] |

{style="table-layout:auto"}

Gebruikend deze gegevens, kunt u beginnen [ metriek ](../../../data-user/reports/ess-manage-data-metrics.md) en [ rapporten ](../../../tutorials/using-visual-report-builder.md) te creëren die op het uitgeven van gegevens worden gebaseerd en [ het te trouwen met uw levensinkomsten om ROI ](../../analysis/roi-ad-camp.md) te berekenen.

## Geconsolideerde tabellen

[!DNL Adobe] raadt u aan een `consolidated ad spend` -tabel te maken waarin de gegevens uit al uw verschillende advertentiebronnen worden gecombineerd tot één tabel. Hierdoor kunt u één set meetgegevens gebruiken voor de analyse van advertenties.

Als u geen geconsolideerde tabel hebt en u maakt een mooi dashboard op de `adwords` -tabel, moet u de rapportage repliceren of dubbele metriek maken om die gegevens te vergelijken met uw [!DNL Facebook Ads] -gegevens. Met behulp van een geconsolideerde tabel kunt u naadloos [!DNL Facebook Ads] -gegevens opnemen in uw bestaande [!DNL Adwords] -rapporten. U kunt ook segmenteren op advertentieplatform.

Als u reeds de gebieden hierboven hebt gesynchroniseerd, [ contacteer ons ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om uw advertentie uit te breiden.
