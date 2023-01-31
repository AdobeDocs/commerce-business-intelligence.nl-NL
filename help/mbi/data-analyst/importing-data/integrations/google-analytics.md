---
title: Google Analytics verbinden
description: Leer Google Analytics te verbinden met [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Verbinden [!DNL Google Analytics]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is de meest gebruikte webanalysedienst op internet. Implementatie [!DNL Google Analytics] op uw website kunt u bijhouden hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en nog veel meer. Deze gegevens analyseren in [!DNL MBI], naast andere gegevens, zal de algemene gezondheid en bruikbaarheid van uw site verbeteren.

Laten we beginnen met het invoeren van onze [!DNL Google Analytics] inloggegevens [!DNL MBI]:

1. Ga naar de **[!UICONTROL Manage Data** > **Integrations]** pagina.
1. Klikken **[!UICONTROL Add Integration]**, die zich aan de rechterkant van het scherm bevindt.
1. Klik op de knop [!DNL Google Analytics] pictogram. Hierdoor wordt de [!DNL Google Analytics] aanmeldingspagina.
1. Voer uw [!DNL Google Analytics] referenties. Als het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL MBI].
1. Er wordt een lijst met profiel-id&#39;s weergegeven. Controleer de profielen waarmee u verbinding wilt maken [!DNL MBI]. Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u het dialoogvenster Meerdere verbindingen [!DNL Google Analytics] in de onderstaande sectie Profielen.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Wijzigingen worden automatisch opgeslagen, dus klik op **Terug naar Verbindingen** als u klaar bent.

## Meerdere verbindingen maken [!DNL Google Analytics] profielen

U hebt mogelijk meerdere websites verbonden met één [!DNL Google Analytics] eigen rekening [!DNL Google Analytics] profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL MBI]. Controleer gewoon de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

Om een bepaalde website te identificeren [!DNL Google Analytics] Profiel-id:

1. Aanmelden [!DNL Google Analytics]
1. Ga naar de specifieke website [!DNL Google Analytics] dashboard
1. Kijk naar de URL. De profiel-id komt overeen met de volgende 8 nummers `p` aan het einde van de regel:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Verbinding verbreken [!DNL Google Analytics] van [!DNL MBI] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [accountinstellingen](https://www.google.com/accounts/) pagina.
1. Onder de `Security` en klik op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klikken **[!UICONTROL revoke access]** naast [!DNL MBI].

## Verwante:

* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151)
* [Verbinding maken [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Websiteactiviteiten en conversietarieven van klanten analyseren](../../analysis/web-act-cust-conversion.md)
* [Verzamelingsgegevens van gebruikers bijhouden met [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
* [Gebruikersapparaat en browsergegevens bijhouden met [!DNL Google Analytics] cookies](https://support.magento.com/hc/en-us/articles/360016732911)
