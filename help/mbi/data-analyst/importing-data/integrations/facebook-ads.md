---
title: Connect Facebook-advertenties
description: Leer hoe u uw advertentie kunt analyseren en kunt zien of uw geld effectief wordt besteed.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Verbinden [!DNL Facebook Ads]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

Je hebt onderzoek gedaan, je hebt advertenties gemaakt, je hebt je campagne gestart op [!DNL Facebook] . Nu is het tijd om uw advertentie-uitgaven te analyseren en te zien of wordt uw geld effectief besteed. Gebruikend uw advertentie geeft gegevens uit, kunt u campagne ROI door uw reclamekosten en de waarde van het klantenleven (CLV) [ van gebruikers te bedienen die van uw campagnes worden verworven.](../../../data-analyst/analysis/roi-ad-camp.md)

Het verbinden van uw [!DNL Facebook Ad] gegevens met [!DNL Commerce Intelligence] is een eenvoudig proces in drie stappen:

1. [Voeg  [!DNL Facebook]  als gegevensbron in  [!DNL Commerce Intelligence] toe](#stepone)
1. [Toestaan  [!DNL Commerce Intelligence]  toegang tot uw  [!DNL Facebook Ads]  gegevens](#steptwo)
1. [Selecteer  [!DNL Facebook Ads]  Rekeningen voor het trekken van gegevens](#stepthree)

## [!DNL Facebook] toevoegen als gegevensbron in [!DNL Commerce Intelligence] {#stepone}

1. Als u de [!DNL Facebook] integratie aan uw [!DNL Commerce Intelligence] rekening wilt toevoegen, navigeert u naar de `Connections` pagina onder **[!UICONTROL Manage Data** > **Integrations]**.
1. Klik op **[!UICONTROL Add Integration]** aan de rechterkant.
1. Klik op het pictogram [!DNL Facebook] . Hierdoor wordt de machtigingspagina van [!DNL Facebook] weergegeven.
1. Klik op **[!UICONTROL Authorize]**.

## Toegang van [!DNL Commerce Intelligence] tot uw [!DNL Facebook Ads] -gegevens toestaan {#steptwo}

Nadat u op **[!DNL Facebook Authorize]** hebt geklikt, wordt een klein pop-upvenster weergegeven:

![](../../../assets/Facebook_Access_Popup.png)

U voert een reeks stappen uit om [!DNL Commerce Intelligence] toegang te geven tot gegevens van uw openbare profiel [!DNL Facebook Ads] en verwante status. Klik op **[!UICONTROL OK]** om door te gaan.

## Selecteer [!DNL Facebook Ads] Accounts voor het ophalen van gegevens {#stepthree}

1. Nadat de verificatie is voltooid, wordt u gevraagd om de [!DNL Facebook Ads] -accounts te selecteren waaruit u gegevens wilt ophalen. Selecteer de gewenste accounts door op het selectievakje `Connect` in de kolom te klikken.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Klik op **[!UICONTROL Save Connections]**.

   Als de verbinding succesvol is, succesvol a *Verbinding!* wordt boven aan de pagina weergegeven.

## Wat nu? {#next}

Zorg ervoor dat u [!DNL Facebook] campagnes in [!DNL Google Analytics] volgt. Zo zorgt u ervoor dat het veld `utm\_campaign` in [!DNL Google Analytics] correct is ingevuld voor uw [!DNL Facebook] -campagnes.

## Verwante

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Verbind uw  [!DNL Google Adwords]  rekening](../integrations/google-ecommerce.md)
* [Bron voor verwijzing van de orde van het spoor via  [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../../analysis/track-usr-dev-browser.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
* [Hoe werkt  [!DNL Google Analytics]  UTM attributie?](../../analysis/utm-attributes.md)
