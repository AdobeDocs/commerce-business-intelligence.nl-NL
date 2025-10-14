---
title: Google Adwords-gegevens verwacht
description: Leer hoe u Data Warehouse Manager kunt gebruiken om relevante gegevensvelden gemakkelijk bij te houden voor analyse.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# [!DNL Google Adwords] gegevens verwacht

Nadat [&#x200B; u uw  [!DNL Google Adwords]  rekening &#x200B;](../integrations/google-adwords.md) hebt verbonden, kunt u de [&#x200B; Manager van Data Warehouse &#x200B;](../../data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.

Er zijn twee tabellen beschikbaar voor replicatie naar uw Data Warehouse:

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
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Totaal aantal klikken voor de dag |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Totale kosten van de campagne voor de dag |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] Campagne-id |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | De naam van de campagne (bijvoorbeeld, [&#x200B; utm \_campagne &#x200B;](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | De datum waarop de campagne is gestart |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Aantal indrukken voor de dag |
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
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Totaal aantal klikken voor de dag |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Totale kosten van de campagne voor de dag |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] Campagne-id |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | De naam van de campagne (bijvoorbeeld, [&#x200B; utm \_campagne &#x200B;](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | De datum waarop de campagne is gestart |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Aantal indrukken voor de dag |
| `profileId` | Profiel-id |
| `profileName` | De profielnaam |
| `\_updated\_at` | De datum en tijd van de laatste update voor deze rij |
| `keyword` | Het sleutelwoord van de campagne |
| `adContent` | De eerste regel van de tekst voor de online campagne |
| `adDestinationUrl` | De URL waarnaar de [!DNL Adwords] verwijst, verwijst naar verkeer |
| `adGroup` | De naam van de ad-groep [!DNL Adwords] |

{style="table-layout:auto"}

Gebruikend deze gegevens, kunt u beginnen [&#x200B; metriek &#x200B;](../../../data-user/reports/ess-manage-data-metrics.md) en [&#x200B; rapporten &#x200B;](../../../tutorials/using-visual-report-builder.md) te creëren die op het uitgeven van gegevens worden gebaseerd en [&#x200B; het te trouwen met uw levensinkomsten om ROI &#x200B;](../../analysis/roi-ad-camp.md) te berekenen.

## Geconsolideerde tabellen

[!DNL Adobe] raadt u aan een `consolidated ad spend` -tabel te maken waarin de gegevens uit al uw verschillende advertentiebronnen worden gecombineerd tot één tabel. Hierdoor kunt u één set meetgegevens gebruiken voor de analyse van advertenties.

Als u geen geconsolideerde tabel hebt en u maakt een mooi dashboard op de `adwords` -tabel, moet u de rapportage repliceren of dubbele metriek maken om die gegevens te vergelijken met uw [!DNL Facebook Ads] -gegevens. Met behulp van een geconsolideerde tabel kunt u naadloos [!DNL Facebook Ads] -gegevens opnemen in uw bestaande [!DNL Adwords] -rapporten. U kunt ook segmenteren op advertentieplatform.

Als u reeds de gebieden hierboven hebt gesynchroniseerd, [&#x200B; contacteer ons &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) om uw advertentie uit te breiden.
