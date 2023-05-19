---
title: Toegang tot metriek beperken
description: Leer hoe u met metrische toegang en beperkingen werkt.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Gebruikers van metriek beheren

Naast het plaatsen van de niveaus van de gebruikerstoestemming, kunt u toegang tot metriek op een gebruiker-door-gebruiker basis ook beperken. Bijvoorbeeld, als u uw boekhoudingsafdeling toegang tot opbrengst-verwante metriek maar niet gebruiker-verwervingsmetriek wilt hebben, kunt u toegang tot die metriek beperken.

In dergelijke gevallen raadt Adobe aan om de account van die gebruiker in te stellen op **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** de toestemmingen zouden aan gebruikers moeten worden gegeven die metriek, berekende kolommen, integraties, of gebruikers niet hoeven tot stand te brengen of te veranderen, maar zij hebben toegang tot gegevens in de Data Warehouse nodig. Als u de toegang tot gegevens volledig wilt beperken, gebruikt u de **[!UICONTROL Read Only]** in plaats daarvan machtigingen.

Nadat u het machtigingsniveau hebt ingesteld, kunt u de metriek selecteren als **[!UICONTROL Standard]** kan de gebruiker toegang krijgen door het volgende te doen:

1. Ga naar **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Selecteer de gewenste gebruikersaccount.
1. De **[!UICONTROL Metrics]** wordt een lijst weergegeven met beschikbare maatstaven. Controleer de meetgegevens waartoe de gebruiker toegang moet hebben en hef de selectie op van de gegevens waartoe de gebruiker geen toegang mag hebben.
1. [!DNL Adobe Commerce Intelligence] Hiermee worden de wijzigingen automatisch opgeslagen. Als de wijziging is gelukt, [!DNL Commerce Intelligence] displays **[!UICONTROL Saved!]** boven aan de pagina.

>[!NOTE]
>
>Alle gebruikers met **[!UICONTROL Standard]** rechten hebben toegang tot alle gegevens in de Data Warehouse via Data Export, naast alle gegevens van [!DNL Google Analytics].

U kunt toegang tot metrisch ook beperken door metrisch uit te geven en **[!UICONTROL Standard]** gebruikers selecteren in het dialoogvenster **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** sectie.

>[!NOTE]
>
>Als u een metrische waarde dupliceert, [!DNL Commerce Intelligence] kopieert de gebruikerstoestemmingen die in originele metrisch worden geplaatst.
