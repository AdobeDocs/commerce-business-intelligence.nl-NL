---
title: Connect Facebook-advertenties
description: Leer hoe u uw advertentie kunt analyseren en kunt zien of uw geld effectief wordt besteed.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Verbinden [!DNL Facebook Ads]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

Je hebt je onderzoek gedaan, je hebt je advertenties gemaakt, je hebt je campagne gestart op [!DNL Facebook]. Nu is het tijd om uw advertentie-uitgaven te analyseren en te zien of wordt uw geld effectief besteed. Met behulp van uw advertentiefoutgegevens kunt u [maatregel campagne ROI door uw reclamekosten en de waarde van het klantenleven (CLV) te vergelijken](../../../data-analyst/analysis/roi-ad-camp.md) van gebruikers die zijn aangeschaft via uw campagnes.

Uw [!DNL Facebook Ad] gegevens naar [!DNL Commerce Intelligence] is een eenvoudig proces in drie stappen:

1. [Toevoegen [!DNL Facebook] als gegevensbron in [!DNL Commerce Intelligence]](#stepone)
1. [Toestaan [!DNL Commerce Intelligence] toegang tot uw [!DNL Facebook Ads] data](#steptwo)
1. [Selecteren [!DNL Facebook Ads] Rekeningen voor het aantrekken van gegevens](#stepthree)

## Toevoegen [!DNL Facebook] als gegevensbron in [!DNL Commerce Intelligence] {#stepone}

1. Als u de opdracht [!DNL Facebook] integratie met uw [!DNL Commerce Intelligence]account, naar de `Connections` pagina onder **[!UICONTROL Manage Data** > **Integrations]**.
1. Klikken **[!UICONTROL Add Integration]**, rechts.
1. Klik op de knop [!DNL Facebook] pictogram. Hierdoor wordt het dialoogvenster [!DNL Facebook] machtigingspagina.
1. Klikken **[!UICONTROL Authorize]**.

## Toestaan [!DNL Commerce Intelligence] toegang tot uw [!DNL Facebook Ads] data {#steptwo}

Na klikken **[!DNL Facebook Authorize]**, wordt een klein pop-upvenster weergegeven:

![](../../../assets/Facebook_Access_Popup.png)

U voert een reeks stappen uit om [!DNL Commerce Intelligence] toegang te krijgen tot gegevens uit uw openbaar profiel, [!DNL Facebook Ads] en, verwante staten. Klikken **[!UICONTROL OK]** over deze stappen om door te gaan.

## Selecteren [!DNL Facebook Ads] Rekeningen voor het aantrekken van gegevens {#stepthree}

1. Nadat de verificatie is voltooid, wordt u gevraagd de [!DNL Facebook Ads] Accounts waarvan u gegevens wilt ophalen. Selecteer de gewenste accounts door op het selectievakje `Connect` kolom.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Klikken **[!UICONTROL Save Connections]**.

   Als de verbinding is gelukt, kunt u *Verbinding gelukt!* wordt boven aan de pagina weergegeven.

## Wat nu? {#next}

Zorg ervoor dat u bijhoudt [!DNL Facebook] campagnes in [!DNL Google Analytics]. Dit zorgt ervoor dat de `utm\_campaign` veld in [!DNL Google Analytics] is correct gevuld voor uw [!DNL Facebook] campagnes.

## Verwante

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Verbind uw [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Referentiebron voor bestelling volgen via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../../analysis/track-usr-dev-browser.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
* [Hoe werkt [!DNL Google Analytics] UTM-toewijzingswerk?](../../analysis/utm-attributes.md)
