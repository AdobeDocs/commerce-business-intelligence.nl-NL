---
title: Connect Google Adwords
description: Leer om campagne ROI te meten door uw reclamekosten en de waarde van de klantenlevensduur (CLV) van gebruikers te vergelijken die van uw campagnes worden verworven.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Verbinden [!DNL Google Adwords]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![ het embleem van Google AdWords ](../../../assets/Google_Adwords_logo.png)

Je hebt onderzoek gedaan, je hebt advertenties gemaakt, je hebt je [!DNL Google] campagne gestart. Nu is het tijd om uw advertentie-uitgaven te analyseren en te zien of wordt uw geld effectief besteed. Gebruikend uw advertentie geeft gegevens uit, kunt u campagne ROI door uw reclamekosten en de waarde van het klantenleven (CLV) [ van gebruikers te bedienen die van uw campagnes worden verworven.](../../analysis/roi-ad-camp.md)

Ga aan de slag door uw [!DNL Google Adwords] -gegevens in te voeren in [!DNL Commerce Intelligence] .

1. Ga naar de `Connections` pagina onder **leidt Gegevens > Integraties**.
1. Klik **toevoegen Integratie**, die op de hoger-juiste kant van het scherm wordt gevestigd.
1. Klik op het pictogram **[!DNL Google Adwords]** . Hierdoor wordt de aanmeldingspagina van [!DNL Google Adwords] geopend.
1. Voer uw [!DNL Google Analytics] referenties in. Nadat het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence] .
1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence] .

   ![ de verbindingsdialoog van Google AdWords die profielselectie toont ](../../../assets/cnnct-profile.png)

1. Wijzigingen worden automatisch opgeslagen. Klik dus op **[!UICONTROL Back to Connections]** als u klaar bent.

Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de sectie `Connecting Multiple Google Analytics profiles` hieronder.

## Meerdere [!DNL Google Analytics] -profielen verbinden

Er kunnen meerdere websites verbonden zijn met één [!DNL Google Analytics] -account, geïdentificeerd door hun eigen [!DNL Google Analytics] profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence] . Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

**om identiteitskaart van het Profiel van Google Analytics van een bepaalde website te identificeren:**

1. Aanmelden bij [!DNL Google Analytics]
1. Naar het [!DNL Google Analytics] dashboard van de specifieke website gaan
1. Kijk naar de URL. De profiel-id komt overeen met de acht nummers na `p` aan het einde van de regel:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Verbinding verbreken [!DNL Google Adwords]

1. Bezoek uw [!DNL Google] [ pagina van de rekeningsmontages ](https://www.google.com/account/about/?hl=en).
1. Klik onder de sectie `Security` op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klik op **[!UICONTROL revoke access]**.

## Verwante

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Bron voor verwijzing van de orde van het spoor via  [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
* [Hoe werkt  [!DNL Google Analytics]  UTM attributie?](../../analysis/utm-attributes.md)
