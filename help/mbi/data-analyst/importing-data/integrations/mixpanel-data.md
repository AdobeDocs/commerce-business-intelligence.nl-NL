---
title: Gegevens van Mixpanel verwacht
description: De belangrijkste gegevenstabellen verkennen die u vanuit het deelvenster Mixen kunt importeren in uw [!DNL MBI] account.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Verwacht [!DNL Mixpanel] data

Na [u hebt verbinding gemaakt met uw [!DNL Mixpanel] account](../integrations/mixpanel.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

In dit artikel bekijken we de belangrijkste gegevenstabellen waaruit u kunt importeren [!DNL Mixpanel] in uw [!DNL MBI] account. De volgende lijsten zullen in uw gegevenspakhuis na het verbinden van Mixpanel worden gecreeerd. Als u alle velden wilt weergeven die u kunt bijhouden, klikt u op de koppelingen in de kolom Tabelnaam.

>[!NOTE]
>
>Vanwege de beperkingen van de [!DNL Mixpanel] API, historische gegevens - gegevens ouder dan zeven (7) dagen vanaf de datum van verbinding aan [!DNL MBI] - wordt niet gerepliceerd.

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | Deze tabel bevat onbewerkte gebeurtenisgegevens, zoals de gebeurtenis, gebeurtenisdatums en het platformemmertje. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | Deze tabel bevat gegevens over uw trechters, waaronder de trechter-id, de trechter-lengte (# dagen dat de gebruiker de trechter moet aanvullen) en de begin- en einddatum van de trechter. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | Dit bevat gegevens van de Analyse van Mensen, met inbegrip van zitting IDs, pagina en gebruikersinformatie, en de datum/de tijd de gebruiker het laatst werd gezien. |

{style=&quot;table-layout:auto&quot;}

## Gerelateerde documentatie

* [Verbinding maken [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
