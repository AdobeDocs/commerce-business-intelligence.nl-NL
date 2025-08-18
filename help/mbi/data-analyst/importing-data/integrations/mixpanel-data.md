---
title: Gegevens van Mixpanel verwacht
description: Onderzoek de belangrijkste gegevenslijsten die u van Mixpanel in uw  [!DNL Commerce Intelligence]  rekening kunt invoeren.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# [!DNL Mixpanel] gegevens verwacht

Nadat [ u uw  [!DNL Mixpanel]  rekening ](../integrations/mixpanel.md) hebt verbonden, kunt u de [ Manager van Data Warehouse ](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.

In dit onderwerp worden de belangrijkste gegevenstabellen besproken die u vanuit [!DNL Mixpanel] kunt importeren in uw [!DNL Commerce Intelligence] -account. De volgende tabellen worden na verbinding met [!DNL Mixpanel] in uw Data Warehouse gemaakt. Als u alle velden wilt weergeven die u kunt bijhouden, klikt u op de koppelingen in de kolom Tabelnaam.

>[!NOTE]
>
>Vanwege de beperkingen van de [!DNL Mixpanel] API worden historische gegevens - gegevens ouder dan zeven (7) dagen vanaf de datum van verbinding met [!DNL Commerce Intelligence] - niet gerepliceerd.

| **Naam van de Lijst** | **Beschrijving** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Deze tabel bevat onbewerkte gebeurtenisgegevens, zoals de gebeurtenis, gebeurtenisdatums en het platformemmertje. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Deze tabel bevat gegevens over uw trechters, waaronder de trechter-id, de trechter-lengte (# dagen dat de gebruiker de trechter moet aanvullen) en de begin- en einddatum van de trechter. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Dit bevat gegevens van de Analyse van Mensen, met inbegrip van zitting IDs, pagina en gebruikersinformatie, en de datum/de tijd de gebruiker het laatst werd gezien. |

{style="table-layout:auto"}

## Gerelateerde documentatie

* [Verbinding maken  [!DNL Mixpanel]](../integrations/mixpanel.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
