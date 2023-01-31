---
title: Connect Google ECommerce
description: Meer informatie over uw meest gewaardeerde verwijzingskanalen.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Verbinden [!DNL Google ECommerce]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

U hebt gestage stroom van verkeer en orden, wat betekent u effectief bereikend en klanten verwerft. Maar wat zijn uw meest waardevolle verwijzingskanalen? wat is de gemiddelde levenswaarde van klanten die van één bron tegenover een andere worden verworven? Door de brongegevens van uw bestelling met elkaar te verbinden vanuit [!DNL Google ECommerce] tot [!DNL MBI]kunt u analyses maken die u helpen uw [meest waardevolle afzetkanalen](../../../data-analyst/analysis/most-value-source-channel.md).

Laten we beginnen met het invoeren van onze [!DNL Google ECommerce] inloggegevens [!DNL MBI]:

1. Ga naar de `Connections` pagina onder **[!UICONTROL Admin** > **Connections]**.
1. Klikken **[!UICONTROL Add a New Source]**, die zich aan de rechterkant van het scherm boven het `Data Sources` tabel.
1. Klik op de knop [!DNL Google ECommerce] pictogram. Hierdoor wordt de [!DNL Google ECommerce] aanmeldingspagina.
1. Voer uw [!DNL Google Analytics] referenties. Als het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL MBI].
1. Er wordt een lijst met profiel-id&#39;s weergegeven. Controleer de profielen waarmee u verbinding wilt maken [!DNL MBI].

   Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u **Meerdere verbindingen [!DNL Google Analytics] in de onderstaande sectie Profielen.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Wijzigingen worden automatisch opgeslagen, dus klik gewoon op **[!UICONTROL Back to Connections]** als u klaar bent.

## Meerdere verbindingen maken [!DNL Google Analytics] profielen naar [!DNL MBI]

U hebt mogelijk meerdere websites verbonden met één [!DNL Google Analytics] eigen rekening [!DNL Google Analytics] profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL MBI]. Controleer gewoon de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

Om een bepaalde website te identificeren [!DNL Google Analytics] Profiel-id:

1. Aanmelden [!DNL Google Analytics]
1. Ga naar de specifieke website [!DNL Google Analytics] dashboard
1. Kijk naar de URL. De profiel-id komt overeen met de volgende 8 nummers `p` aan het einde van de regel

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Verbinding verbreken [!DNL Google ECommerce] van [!DNL MBI] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [accountinstellingen](https://www.google.com/accounts/) pagina.
1. Onder de `Security` sectie, klikt u op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klikken **[!UICONTROL revoke access]** naast [!DNL MBI].

## Verwante:

* [Verwacht [!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)
* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151)
* [Instellen [!DNL Google ECommerce] bijhouden](https://support.google.com/analytics/answer/1009612?hl=en)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
