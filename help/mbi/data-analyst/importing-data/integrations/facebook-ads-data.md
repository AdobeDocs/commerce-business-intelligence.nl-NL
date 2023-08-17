---
title: Facebook Ads-gegevens verwacht
description: Leer een kort overzicht van de tabellen die u kunt synchroniseren met uw Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Verwacht [!DNL Facebook Ads] data

Nadat u [heeft uw [!DNL Facebook Ads] account](../integrations/facebook-ads.md), kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

Dit onderwerp geeft u een kort overzicht van de lijsten Adobe adviseert u aan uw Data Warehouse synchroniseren. Dit benadrukt slechts de kernlijsten, aangezien er vrij een paar subtables zijn.

## Kern- en campagnemetabellen

Deze lijsten bevatten gegevens over kern en campagnecomponenten.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Deze tabel is de belangrijkste tabel voor campagnes in een [!DNL Facebook Ads] account. Kolommen opnemen `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Deze tabelrecord is de kerntabel [!DNL Facebook Ads] Stelt in een [!DNL Facebook Ads] account. Kolommen bevatten de advertentie `Campaign id/name` de advertentieset behoort tot, de budgettering, het type bod, de planning en doelgerichte informatie.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

In deze tabel worden alle advertenties in een [!DNL Facebook Ads] account. Kolommen bevatten de advertentiemateriaal, waaronder de advertentieset en de advertentiecampagne waartoe deze behoort, de advertentie, het adverteren en het aanwijzen, en een verwijzing naar specifieke creatieve (beeld/tekst) die de advertentie gebruikt.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

In deze tabel worden de creatieve elementen vastgelegd die worden gebruikt in [!DNL Facebook Ads]. Creatieve producten bevatten waar nodig creatieve namen, beschrijvingen en relevante URL&#39;s voor afbeeldingen.

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
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
