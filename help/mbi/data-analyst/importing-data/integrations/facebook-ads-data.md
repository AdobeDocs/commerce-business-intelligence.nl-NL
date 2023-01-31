---
title: Facebook Ads-gegevens verwacht
description: Leer een kort overzicht van de lijsten wij u adviseren om met uw gegevenspakhuis te synchroniseren
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Verwacht [!DNL Facebook Ads] data

![](../../../assets/Facebook_Logo.png)

Nadat u [heeft uw [!DNL Facebook Ads] account](../integrations/facebook-ads.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

In dit artikel, geven wij u een kort overzicht van de lijsten wij u adviseren om met uw gegevenspakhuis te synchroniseren. Dit is geen volledige lijst, aangezien er vrij een paar subtables zijn. We markeren alleen de kerntabellen.

## Kerntabellen en campagnemetabellen

Deze lijsten bevatten gegevens over kern en campagnecomponenten.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

Deze tabel is de belangrijkste tabel voor campagnes in een [!DNL Facebook Ads] account. Kolommen opnemen `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Deze tabelrecords vormen de kern van de tabel [!DNL Facebook Ads] Stelt in een [!DNL Facebook Ads] account. Kolommen bevatten de advertentie `Campaign id/name` de advertentieset behoort tot, de budgettering, het soort bod, de planning en het doelpubliek.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

In deze tabel worden alle advertenties in een [!DNL Facebook Ads] account. Kolommen bevatten de advertentiemateriaal, waaronder de advertentieset en de advertentiecampagne waartoe deze behoort, de advertentie, de advertentie en het zoeken naar en verwijzen naar specifieke creatieve (afbeelding/tekst) die de advertentie gebruikt.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

In deze tabel worden alle creatieve elementen weergegeven die worden gebruikt in [!DNL Facebook Ads]. Deze omvatten, waar van toepassing, creatieve naam, beschrijving en relevante URL&#39;s voor afbeeldingen.

## Gesegmenteerde campagnemetabellen

De volgende tabellen bevatten een vermelding voor elke campagne/set/advertentiecombinatie voor elke dag, uitgesplitst naar afmetingen zoals leeftijd, geslacht en land.

### `facebook _ads insights_ (account-id)`

Deze lijst omvat een ingang voor elke campagne/reeks/ad combinatie voor elke dag, samen met statistieken met inbegrip van beelden, kliks, kosten, cpc, cpm, cpp, ctr, bereik, sociaal bereik, en uitgaven.

### `facebook _ads insights_ (account-id)_~\_actions`

Dit is een subtabel van het dialoogvenster `facebook_ads_insights_{account_id}` tabel. Dit omvat conversiegegevens voor acties die op verschillende campagnes zijn gebaseerd.

### `facebook _ads insights country_ (account-id)`

Deze tabel bevat dezelfde gegevens als de `facebook_ads_insights_{account_id}` de tabel en de segmenten per land.

### `facebook ads insights age and gender (account-id)`

Deze tabel bevat dezelfde gegevens als de `facebook_ads_insights_{account_id}` tabel en segmenteert deze naar leeftijd en geslacht.

## Verwante

* [Verbinding maken [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
