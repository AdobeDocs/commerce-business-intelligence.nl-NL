---
title: Facebook-advertentiegegevens verwacht
description: Leer een kort overzicht van de tabellen die u kunt synchroniseren met uw Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Facebook Ads] gegevens verwacht

Nadat u uw [ rekening  [!DNL Facebook Ads]  hebt verbonden ](../integrations/facebook-ads.md), kunt u de [ Manager van Data Warehouse ](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.

In dit onderwerp vindt u een kort overzicht van de tabellen die Adobe aanbeveelt te synchroniseren met uw Data Warehouse. Dit benadrukt slechts de kernlijsten, aangezien er vrij een paar subtables zijn.

## Kern- en campagnemetabellen

Deze lijsten bevatten gegevens over kern en campagnecomponenten.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Deze tabel is de kerntabel met campagnes in een [!DNL Facebook Ads] -account. Kolommen bevatten `campaign id` , `name` , `status (active/paused)` , `objective` .

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Deze tabelrecord is de kerntabel van [!DNL Facebook Ads] Sets in een [!DNL Facebook Ads] -account. Tot de kolommen behoren de advertentie `Campaign id/name` waartoe de advertentieset behoort, de budgettering, het type bod, de planning en doelgerichte informatie.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

In deze tabel worden alle advertenties in een [!DNL Facebook Ads] -account vastgelegd. Kolommen bevatten de advertentiemateriaal, waaronder de advertentieset en de advertentiecampagne waartoe deze behoort, de advertentie, het adverteren en het aanwijzen, en een verwijzing naar specifieke creatieve (beeld/tekst) die de advertentie gebruikt.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

In deze tabel worden de creatieve elementen vastgelegd die in [!DNL Facebook Ads] worden gebruikt. Creatieve producten bevatten waar nodig creatieve namen, beschrijvingen en relevante URL&#39;s voor afbeeldingen.

## Gesegmenteerde campagnemetabellen

De volgende tabellen bevatten een vermelding voor elke campagne/set/advertentiecombinatie voor elke dag, uitgesplitst naar afmetingen zoals leeftijd, geslacht en land.

### `facebook _ads insights_ (account-id)`

Deze lijst omvat een ingang voor elke campagne/reeks/ad combinatie voor elke dag, samen met statistieken met inbegrip van beelden, kliks, kosten, cpc, cpm, cpp, ctr, bereik, sociaal bereik, en uitgaven.

### `facebook _ads insights_ (account-id)_~\_actions`

Dit is een subtabel van de tabel `facebook_ads_insights_{account_id}` . Dit omvat conversiegegevens voor acties die op verschillende campagnes zijn gebaseerd.

### `facebook _ads insights country_ (account-id)`

Deze tabel bevat dezelfde informatie als de tabel `facebook_ads_insights_{account_id}` en segmenteert deze per land.

### `facebook ads insights age and gender (account-id)`

Deze tabel bevat dezelfde informatie als de tabel `facebook_ads_insights_{account_id}` en segmenteert deze op leeftijd en geslacht.

## Verwante

* [Verbinding maken  [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
