---
title: Connect Google Analytics
description: Leer om Google Analytics met  [!DNL Commerce Intelligence] te verbinden.
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Verbinden [!DNL Google Analytics]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![ het embleem van Google Analytics ](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is de meest gebruikte service voor webanalyse op internet. Als u [!DNL Google Analytics] op uw website implementeert, kunt u bijhouden hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en nog veel meer. Als u deze gegevens in [!DNL Commerce Intelligence] analyseert, worden de algemene gezondheid en bruikbaarheid van uw site verbeterd, samen met andere gegevens.

Ga aan de slag door uw [!DNL Google Analytics] -gegevens in te voeren in [!DNL Commerce Intelligence] :

1. Ga naar **[!UICONTROL Manage Data** > **Integrations]** .

1. Klik op **[!UICONTROL Add Integration]** aan de rechterkant van het scherm.

1. Klik op het pictogram [!DNL Google Analytics] . Hierdoor wordt de aanmeldingspagina van [!DNL Google Analytics] geopend.

1. Voer uw [!DNL Google Analytics] referenties in. Als het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence] .

1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence] . Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de sectie Meerdere [!DNL Google Analytics] profielen verbinden hieronder.

   ![ Google Analytics Admin pagina die profielidentiteitskaart in URL tonen ](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. De veranderingen worden opgeslagen automatisch, zodat klik **terug naar Verbindingen** wanneer u wordt gedaan.

## Meerdere [!DNL Google Analytics] -profielen verbinden

U kunt meerdere websites hebben die zijn verbonden met één [!DNL Google Analytics] -account, geïdentificeerd door hun eigen [!DNL Google Analytics] -profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence] . Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

De profiel-id [!DNL Google Analytics] van een bepaalde website identificeren:

1. Aanmelden bij [!DNL Google Analytics]
1. Naar het [!DNL Google Analytics] dashboard van de specifieke website gaan
1. Kijk naar de URL. De profiel-id komt overeen met de acht nummers na `p` aan het einde van de regel:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics] loskoppelen van [!DNL Commerce Intelligence] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [ pagina van de rekeningsmontages ](https://accounts.google.com/).
1. Klik onder de sectie `Security` op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klik op **[!UICONTROL revoke access]** naast [!DNL Commerce Intelligence] .

## Verwante:

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Verbinding maken  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Websiteactiviteiten en conversietarieven van klanten analyseren](../../analysis/web-act-cust-conversion.md)
* [De gegevens van de gebruikersverwerving van het spoor gebruikend  [!DNL Google Analytics]  koekjes](../../analysis/google-track-user-acq.md)
