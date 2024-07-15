---
title: Toegang tot metriek beperken
description: Leer hoe u met metrische toegang en beperkingen werkt.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Gebruikers van metriek beheren

Naast het plaatsen van de niveaus van de gebruikerstoestemming, kunt u toegang tot metriek op een gebruiker-door-gebruiker basis ook beperken. Bijvoorbeeld, als u uw boekhoudingsafdeling toegang tot opbrengst-verwante metriek maar niet gebruiker-verwervingsmetriek wilt hebben, kunt u toegang tot die metriek beperken.

In dergelijke gevallen raadt de Adobe aan het account van die gebruiker in te stellen op **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)** . **[!UICONTROL Standard]** de toestemmingen zouden aan gebruikers moeten worden gegeven die metriek, berekende kolommen, integraties, of gebruikers niet te hoeven tot stand te brengen of te veranderen, maar zij hebben toegang tot gegevens in de Data Warehouse nodig. Als u de toegang tot gegevens volledig wilt beperken, gebruikt u in plaats daarvan de **[!UICONTROL Read Only]** -machtigingen.

Nadat u het machtigingsniveau hebt ingesteld, kunt u de meetgegevens selecteren waartoe een **[!UICONTROL Standard]** -gebruiker toegang heeft door het volgende te doen:

1. Ga naar **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]** .
1. Selecteer de gewenste gebruikersaccount.
1. Op het tabblad **[!UICONTROL Metrics]** wordt een lijst met beschikbare maatstaven weergegeven. Controleer de meetgegevens waartoe de gebruiker toegang moet hebben en hef de selectie op van de gegevens waartoe de gebruiker geen toegang mag hebben.
1. [!DNL Adobe Commerce Intelligence] slaat de wijzigingen automatisch op. Als de wijziging is gelukt, wordt [!DNL Commerce Intelligence] boven aan de pagina **[!UICONTROL Saved!]** weergegeven.

>[!NOTE]
>
>Alle gebruikers met **[!UICONTROL Standard]** -machtigingen hebben toegang tot alle gegevens in de Data Warehouse via Gegevens exporteren, naast alle gegevens uit [!DNL Google Analytics] .

U kunt de toegang tot metrische informatie ook beperken door metrisch te bewerken en **[!UICONTROL Standard]** gebruikers te selecteren in de sectie **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** .

>[!NOTE]
>
>Als u een metrische waarde dupliceert, kopieert [!DNL Commerce Intelligence] de gebruikersmachtigingen die in de oorspronkelijke metrische waarde zijn ingesteld.
