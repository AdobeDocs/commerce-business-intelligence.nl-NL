---
title: De status van de updatecyclus controleren
description: Leer hoe u de status van de updatecyclus kunt controleren.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Voortgang van cyclus bijwerken

Wanneer u zich aanmeldt bij het [!DNL Adobe Commerce Intelligence] -dashboard, kunt u de status van de laatste updatecyclus op verschillende manieren controleren. Het hangt allemaal van het type van [ gebruikerstoestemmingen ](../administrator/user-management/user-management.md) af dat u hebt.

## Waarom zou ik de status van de Update Cycle controleren?

Het controleren van de statusupdatecyclus is nuttig wanneer u de gegevens in uw [!DNL Commerce Intelligence] rekening controleert. Als u [ resultaten ziet die uw verwachtingen ](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md) niet ontmoeten, bijvoorbeeld, passen de dagelijkse verkoop in [!DNL Commerce Intelligence] niet aan wat u in uw e-commerceplatform of in uw [[!DNL Google]  e-commerceopbrengst ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) ziet u het laatste gegevenspunt kunt controleren om te zien of wordt de kwestie opgelost zodra een update voltooit.

## [!UICONTROL Read-Only] en [!UICONTROL Standard] Users

`Read-only` -gebruikers kunnen zich aanmelden bij hun dashboard en zien hoe recent de gegevens zijn bijgewerkt door de muisaanwijzer op het pictogram rechtsboven op de pagina te plaatsen. Dit toont wanneer het laatste gegevenspunt werd getrokken.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Gebruikers

`Admin` -gebruikers kunnen zich aanmelden bij het dashboard en het laatste gegevenspunt hierboven zien, samen met een kort statuspictogram van hun accountintegratie.

Voor meer informatie kunnen beheerders op **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** klikken.

![](../../mbi/assets/detail-manage-data-integrations.png)

Op deze pagina ziet u de huidige updatestatus en de tijd van de laatste voltooide update.

Als er een update wordt uitgevoerd, ziet u een koppeling waarmee u een e-mailmelding kunt aanvragen zodra de update is voltooid.

Als er geen update wordt uitgevoerd, ziet u een koppeling waarmee een update wordt geforceerd om te starten.

>[!NOTE]
>
>Als u brainstormuren hebt (tijd waarop u niet wilt dat [!DNL Commerce Intelligence] uw gegevens bijwerkt), kunt u door een update te forceren een updatecyclus starten die niet voldoet aan de beperkingen van deze brainstormuren.
