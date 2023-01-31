---
title: Toegang tot metriek beperken
description: Leer hoe u met metrische toegang en beperkingen werkt.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Gebruikers van metriek beheren

Naast het plaatsen van de niveaus van de gebruikerstoestemming, kunt u toegang tot metriek op een gebruiker-door-gebruiker basis ook beperken. Bijvoorbeeld, als u uw boekhoudingsafdeling toegang tot opbrengst-verwante metriek maar niet gebruiker-verwervingsmetriek wilt hebben, kunt u toegang tot die metriek beperken.

In dergelijke gevallen raden we u aan de account van die gebruiker in te stellen op **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** de toestemmingen zouden aan gebruikers moeten worden gegeven die metriek, berekende kolommen, integraties, of gebruikers niet hoeven tot stand te brengen of te veranderen, maar zij hebben toegang tot gegevens in de Data Warehouse nodig. Als u de toegang tot gegevens volledig wilt beperken, gebruikt u de **[!UICONTROL Read Only]** in plaats daarvan machtigingen.

Nadat u het machtigingsniveau hebt ingesteld, kunt u de metriek selecteren als **[!UICONTROL Standard]** kan de gebruiker toegang krijgen door het volgende te doen:

1. Ga naar **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Selecteer de gewenste gebruikersaccount.
1. De **[!UICONTROL Metrics]** wordt een lijst met beschikbare meetgegevens weergegeven. Controleer de meetgegevens waartoe de gebruiker toegang moet hebben; Schakel de opties uit waartoe de gebruiker geen toegang mag hebben.
1. [!DNL MBI] Hiermee worden de wijzigingen automatisch opgeslagen. Als de wijziging is gelukt, [!DNL MBI] displays **[!UICONTROL Saved!]** boven aan de pagina.

>[!NOTE]
>
>Alle gebruikers met **[!UICONTROL Standard]** de toestemmingen kunnen tot alle gegevens in het gegevenspakhuis via de Uitvoer van Gegevens toegang hebben naast alle metriek van [!DNL Google Analytics].

U kunt toegang tot metrisch ook beperken door metrisch uit te geven en **[!UICONTROL Standard]** gebruikers selecteren in het dialoogvenster **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** sectie.

>[!NOTE]
>
>Als u een metrische waarde dupliceert, [!DNL MBI] kopieert de gebruikerstoestemmingen die in originele metrisch worden geplaatst.
