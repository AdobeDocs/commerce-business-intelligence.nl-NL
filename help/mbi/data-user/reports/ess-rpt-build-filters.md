---
title: Filters
description: Leer hoe u filters kunt gebruiken.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Filters

Een of meer filters kunnen worden toegevoegd om de gegevens te beperken die worden gebruikt om een rapport te maken. Elk filter is een expressie die een kolom uit de bijbehorende tabel, een operator en een waarde bevat. Bijvoorbeeld om slechts herhaalde klanten te omvatten, zou u een filter kunnen tot stand brengen dat slechts klanten omvat die meer dan één orde hebben geplaatst. U kunt meerdere filters gebruiken met logische `AND/OR` om logica aan het rapport toe te voegen.

>[!TIP]
>
>Een rapport kan een maximum van 3.500 gegevenspunten hebben. Om het aantal gegevenspunten te verminderen, gebruik een filter om de hoeveelheid gegevens te verminderen die wordt gebruikt om het rapport te produceren.

MBI bevat een selectie met filters die u &#39;buiten het vak&#39; kunt gebruiken of naar wens kunt wijzigen. Het aantal filters dat u kunt maken, is onbeperkt.

## Een filter toevoegen:

1. Houd de muisaanwijzer boven elk gegevenspunt in het diagram.

   In dit rapport, toont elk gegevenspunt het totale aantal klanten voor de maand.

1. Klik in het linkerdeelvenster op de filters (![](../../assets/magento-bi-btn-filter.png)).

   ![Filter toevoegen](../../assets/magento-bi-report-builder-filter-add.png)

1. Klikken **[!UICONTROL Add Filter]**.

   Filters worden alfabetisch genummerd en het eerste is `[A]`. De eerste twee delen van het filter zijn vervolgkeuzemogelijkheden en het derde deel is een waarde.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Klik op het eerste deel van het filter en kies de kolom die u als het onderwerp van de expressie wilt gebruiken.

      ![Eerste deel van filter kiezen](../../assets/magento-bi-report-builder-filter-part1.png)

   * Klik op het tweede deel van het filter en kies de operator.

      ![De operator kiezen](../../assets/magento-bi-report-builder-filter-part2.png)

   * Voer in het derde deel van het filter de waarde in die nodig is om de expressie te voltooien.

      ![Voer de waarde in](../../assets/magento-bi-report-builder-filter-part3.png)

   * Wanneer het filter is voltooid, klikt u op **[!UICONTROL Apply]**.

      Het rapport omvat nu slechts herhaalde klanten, en het aantal klantenverslagen die voor het rapport zijn teruggewonnen is verminderd van 33K tot 12.6k.

      ![Gefilterd rapport](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. Klik in het zijpaneel op het perspectief ( ![](../../assets/magento-bi-btn-perspective.png)).

   ![Perspectief](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. Kies in de lijst met instellingen de optie `Cumulative`. Klik vervolgens op **[!UICONTROL Apply]**.

   ![Cumulatief perspectief](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   De `Cumulative` perspectief verdeelt de verandering in tijd, eerder dan het tonen van de gekartelde omhoog en downs voor elke maand.

1. Voer een `Title` voor het rapport en klik op **[!UICONTROL Save]** als een `Chart` naar het dashboard.

   ![Opslaan naar dashboard](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
