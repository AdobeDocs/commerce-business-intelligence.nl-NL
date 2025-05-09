---
title: Connect Google ECommerce
description: Meer informatie over uw meest gewaardeerde verwijzingskanalen.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Verbinden [!DNL Google ECommerce]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

U hebt gestage stroom van verkeer en orden, wat betekent u effectief bereikend en klanten verwerft. Maar wat zijn uw meest waardevolle verwijzingskanalen? Wat is de gemiddelde levenwaarde van klanten die van één bron tegenover een andere worden verworven? Door uw van de ordeverwijzing bron gegevens van [!DNL Google ECommerce] aan [!DNL Commerce Intelligence] aan te sluiten, kunt u analyses bouwen die u helpen uw [ waardevolste marketing kanalen ](../../../data-analyst/analysis/most-value-source-channel.md) identificeren.

Ga aan de slag door uw [!DNL Google ECommerce] -gegevens in te voeren in [!DNL Commerce Intelligence] :

1. Ga naar de pagina `Connections` onder **[!UICONTROL Admin** > **Connections]** .

1. Klik op **[!UICONTROL Add a New Source]** rechts van het scherm boven de `Data Sources` -tabel.

1. Klik op het pictogram [!DNL Google ECommerce] . Hierdoor wordt de aanmeldingspagina van [!DNL Google ECommerce] geopend.

1. Voer uw [!DNL Google Analytics] referenties in. Als het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence] .

1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence] .

   Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de sectie **Meerdere profielen verbinden [!DNL Google Analytics] hieronder.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Wijzigingen worden automatisch opgeslagen. Klik dus op **[!UICONTROL Back to Connections]** als u klaar bent.

## Meerdere [!DNL Google Analytics] -profielen verbinden met [!DNL Commerce Intelligence]

U kunt meerdere websites hebben die zijn verbonden met één [!DNL Google Analytics] -account, geïdentificeerd door hun eigen [!DNL Google Analytics] -profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence] . Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

De profiel-id [!DNL Google Analytics] van een bepaalde website identificeren:

1. Meld u aan bij [!DNL Google Analytics] .
1. Ga naar het [!DNL Google Analytics] dashboard van de specifieke website.
1. Kijk naar de URL. De profiel-id komt overeen met de acht nummers die volgen op `p` aan het einde van de regel.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google ECommerce] loskoppelen van [!DNL Commerce Intelligence] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [ pagina van de rekeningsmontages ](https://www.google.com/account/about/?hl=en).
1. Klik onder de sectie `Security` op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klik op **[!UICONTROL revoke access]** naast [!DNL Commerce Intelligence] .

## Verwante:

* [Verwachte  [!DNL Google ECommerce]  gegevens](../integrations/google-ecommerce-data.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
* [ Vestiging  [!DNL Google ECommerce]  het volgen ](https://support.google.com/analytics/answer/1009612?hl=en)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
