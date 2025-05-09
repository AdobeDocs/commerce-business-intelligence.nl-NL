---
title: Connect Google Adwords
description: Leer om campagne ROI te meten door uw reclamekosten en de waarde van de klantenlevensduur (CLV) van gebruikers te vergelijken die van uw campagnes worden verworven.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Verbinden [!DNL Google Adwords]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Je hebt onderzoek gedaan, je hebt advertenties gemaakt, je hebt je [!DNL Google] campagne gestart. Nu is het tijd om uw advertentie-uitgaven te analyseren en te zien of wordt uw geld effectief besteed. Gebruikend uw advertentie geeft gegevens uit, kunt u campagne ROI door uw reclamekosten en de waarde van het klantenleven (CLV) [&#128279;](../../analysis/roi-ad-camp.md) van gebruikers te bedienen die van uw campagnes worden verworven.

Ga aan de slag door uw [!DNL Google Adwords] -gegevens in te voeren in [!DNL Commerce Intelligence] .

1. Ga naar de `Connections` pagina onder **leidt Gegevens > Integraties**.
1. Klik **toevoegen Integratie**, die op de hoger-juiste kant van het scherm wordt gevestigd.
1. Klik op het pictogram **[!DNL Google Adwords]** . Hierdoor wordt de aanmeldingspagina van [!DNL Google Adwords] geopend.
1. Voer uw [!DNL Google Analytics] referenties in. Nadat het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence] .
1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence] .

   ![](../../../assets/cnnct-profile.png)

1. Wijzigingen worden automatisch opgeslagen. Klik dus op **[!UICONTROL Back to Connections]** als u klaar bent.

Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de sectie `Connecting Multiple Google Analytics profiles` hieronder.

## Meerdere [!DNL Google Analytics] -profielen verbinden

Er kunnen meerdere websites verbonden zijn met één [!DNL Google Analytics] -account, geïdentificeerd door hun eigen [!DNL Google Analytics] profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence] . Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

**om identiteitskaart van het Profiel van Googles Analytics van een bepaalde website te identificeren:**

1. Aanmelden bij [!DNL Google Analytics]
1. Naar het [!DNL Google Analytics] dashboard van de specifieke website gaan
1. Kijk naar de URL. De profiel-id komt overeen met de acht nummers na `p` aan het einde van de regel:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Verbinding verbreken [!DNL Google Adwords]

1. Bezoek uw [!DNL Google] [ pagina van de rekeningsmontages ](https://www.google.com/account/about/?hl=en).
1. Klik onder de sectie `Security` op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klik op **[!UICONTROL revoke access]**.

## Verwante

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
* [Bron voor verwijzing van de orde van het spoor via  [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
* [Hoe werkt  [!DNL Google Analytics]  UTM attributie?](../../analysis/utm-attributes.md)
