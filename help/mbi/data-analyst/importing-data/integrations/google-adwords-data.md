---
title: Google Adwords-gegevens verwacht
description: Leer hoe u de Manager van de Data Warehouse kunt gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Verwacht [!DNL Google Adwords] data

Na [u hebt verbinding gemaakt met uw [!DNL Google Adwords] account](../integrations/google-adwords.md)kunt u de [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

Daar, merkt u twee lijsten beschikbaar voor replicatie in uw Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

De `campaigns` table *moet standaard worden gebruikt*, dus u kunt beginnen door alle relevante velden uit die tabel te synchroniseren.

De `adwords` tabel bevat vier kolommen die niet in de `campaigns` tabel:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Wanneer u in het uitvoeren van een analyse geinteresseerd bent die deze attributen overweegt, moet u gebruiken `adwords` tabel.

>[!IMPORTANT]
>
>In deze tabel worden rijen uitgesloten waarvan alle vier deze kolommen bestaan `null`.

Hieronder ziet u het verwachte schema voor beide tabellen.

## [!DNL Campaigns] table

De `campaigns` tabel bevat de volgende kolommen:

| **Kolom** | **Beschrijving** |
|-----|-----|
| `\_id` | De primaire sleutel voor de tabel |
| `accountId` | De account-id |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totaal aantal klikken voor de dag |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Totale kosten van de campagne voor de dag |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Campagne-id |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Campagnenaam (bijvoorbeeld [utm\_campagne](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | De datum waarop de campagne is gestart |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Aantal indrukken voor de dag |
| `profileId` | Profiel-id |
| `profileName` | De profielnaam |
| `\_updated\_at` | De datum en tijd van de laatste update voor deze rij |

{style="table-layout:auto"}

## [!DNL AdWords] table

De `adwords` tabel bevat de volgende kolommen:

| **Kolom** | **Beschrijving** |
|-----|-----|
| `\_id` | De primaire sleutel voor de tabel |
| `accountId` | De account-id |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totaal aantal klikken voor de dag |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Totale kosten van de campagne voor de dag |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Campagne-id |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Campagnenaam (bijvoorbeeld [utm\_campagne](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | De datum waarop de campagne is gestart |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Aantal indrukken voor de dag |
| `profileId` | Profiel-id |
| `profileName` | De profielnaam |
| `\_updated\_at` | De datum en tijd van de laatste update voor deze rij |
| `keyword` | Het sleutelwoord van de campagne |
| `adContent` | De eerste regel van de tekst voor de online campagne |
| `adDestinationUrl` | De URL waaraan de [!DNL Adwords] doorverwezen verkeer |
| `adGroup` | De naam van de [!DNL Adwords] ad-groep |

{style="table-layout:auto"}

Met deze gegevens kunt u beginnen met het maken van [cijfers](../../../data-user/reports/ess-manage-data-metrics.md) en [rapporten](../../../tutorials/using-visual-report-builder.md) op basis van uitgavengegevens en [Sluit het aan uw levensinkomsten aan om ROI te berekenen](../../analysis/roi-ad-camp.md).

## Geconsolideerde tabellen

[!DNL Adobe] raadt u aan een `consolidated ad spend` tabel om de gegevens van al uw verschillende advertentiebronnen te combineren tot één tabel. Hierdoor kunt u één set meetgegevens gebruiken voor de analyse van advertenties.

Als u geen geconsolideerde tafel hebt en u bouwt een mooi dashboard op het `adwords` tabel, moet u de rapportering herhalen of dubbele metriek creëren om die gegevens met uw te vergelijken [!DNL Facebook Ads] gegevens. Door een geconsolideerde tabel te gebruiken, kunt u deze naadloos integreren [!DNL Facebook Ads] gegevens met uw bestaande [!DNL Adwords] rapporten. U kunt ook segmenteren op advertentieplatform.

Als u de bovenstaande velden al hebt gesynchroniseerd, [contact opnemen met ons](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om je advertentieformaat te consolideren.
