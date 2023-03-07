---
title: Gegevens van Mixpanel verwacht
description: De belangrijkste gegevenstabellen verkennen die u vanuit het deelvenster Mixen kunt importeren in uw [!DNL MBI] account.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Verwacht [!DNL Mixpanel] data

Na [u hebt verbinding gemaakt met uw [!DNL Mixpanel] account](../integrations/mixpanel.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

In dit artikel worden de belangrijkste gegevenstabellen besproken waaruit u kunt importeren [!DNL Mixpanel] in uw [!DNL MBI] account. De volgende tabellen worden in uw Data Warehouse gemaakt nadat u het deelvenster Mixer hebt verbonden. Als u alle velden wilt weergeven die u kunt bijhouden, klikt u op de koppelingen in de kolom Tabelnaam.

>[!NOTE]
>
>Vanwege de beperkingen van de [!DNL Mixpanel] API, historische gegevens - gegevens ouder dan zeven (7) dagen vanaf de datum van verbinding aan [!DNL MBI] - niet wordt gerepliceerd.

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Deze tabel bevat onbewerkte gebeurtenisgegevens, zoals de gebeurtenis, gebeurtenisdatums en het platformemmertje. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Deze tabel bevat gegevens over uw trechters, waaronder de trechter-id, de trechter-lengte (# dagen dat de gebruiker de trechter moet aanvullen) en de begin- en einddatum van de trechter. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Dit bevat gegevens van de Analyse van Mensen, met inbegrip van zitting IDs, pagina en gebruikersinformatie, en de datum/de tijd de gebruiker het laatst werd gezien. |

{style="table-layout:auto"}

## Gerelateerde documentatie

* [Verbinding maken [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
