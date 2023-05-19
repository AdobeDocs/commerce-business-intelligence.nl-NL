---
title: De status van de updatecyclus controleren
description: Leer hoe u de status van de updatecyclus kunt controleren.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Voortgang van cyclus bijwerken

Wanneer u zich aanmeldt bij uw [!DNL Adobe Commerce Intelligence] dashboard, er zijn verscheidene manieren om de status van uw laatste updatecyclus te controleren. Het hangt allemaal af van het type [gebruikersmachtigingen](../administrator/user-management/user-management.md) dat hebt u.

## Waarom zou ik de status van de Update Cycle controleren?

Het controleren van de statusupdatecyclus is nuttig wanneer u de gegevens in uw controleert [!DNL Commerce Intelligence] account. Indien u [resultaten die niet aan uw verwachtingen voldoen](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)bijvoorbeeld de dagelijkse verkoop in [!DNL Commerce Intelligence] komen niet overeen met wat u ziet in uw e-commerceplatform of in uw [[!DNL Google] e-commerceontvangsten](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) U kunt het laatste gegevenspunt controleren om te zien of wordt de kwestie opgelost zodra een update voltooit.

## [!UICONTROL Read-Only] en [!UICONTROL Standard] Gebruikers

`Read-only` gebruikers kunnen zich aanmelden bij hun dashboard en zien hoe recent de gegevens zijn bijgewerkt door de muisaanwijzer op het pictogram rechtsboven op de pagina te plaatsen. Dit toont wanneer het laatste gegevenspunt werd getrokken.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Gebruikers

`Admin` gebruikers kunnen zich aanmelden bij het dashboard en het laatste gegevenspunt hierboven zien, samen met een kort statuspictogram van hun accountintegratie.

Voor meer informatie kunnen beheerders klikken op **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

Op deze pagina ziet u de huidige updatestatus en de tijd van de laatste voltooide update.

Als er een update wordt uitgevoerd, ziet u een koppeling waarmee u een e-mailmelding kunt aanvragen zodra de update is voltooid.

Als er geen update wordt uitgevoerd, ziet u een koppeling waarmee een update wordt geforceerd om te starten.

>[!NOTE]
>
>Als u brainstormuren hebt (tijdstip waarop u dit niet wilt [!DNL Commerce Intelligence] om uw gegevens bij te werken), door een update te forceren wordt een updatecyclus gestart die niet voldoet aan de beperkingen van deze brainstormuren.
