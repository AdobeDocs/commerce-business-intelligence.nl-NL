---
title: Gegevensafmetingen beheren
description: Leer wat een afmeting is en het kan worden gebruikt om grafieken te filtreren of te segmenteren die op metrisch worden gebaseerd.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Gegevensafmetingen beheren

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

Een dimensie is een gebied in de zelfde lijst zoals metrisch die aan filter of segmentgrafieken kan worden gebruikt die op dat metrisch worden gebaseerd. Een maatstaf voor omzet kan bijvoorbeeld plaats, staat, land, orderstatus, couponcode en andere soorten afmetingen bevatten.

## Afmetingen toevoegen aan meerdere metrics

Een of meer dimensies tegelijk toevoegen aan meerdere metrics:

1. Ga naar **[!UICONTROL Manage Data > Metrics]**.

1. Klikken **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Kies de tabel die de afmetingen bevat.

1. In het dialoogvenster `Choose Metric(s) to Add Dimensions` , selecteert u de metrics waaraan u afmetingen wilt toevoegen. Als deze optie is geselecteerd, wordt `Choose Dimensions to Add` rechts in het scherm. Controleer de afmetingen die u aan de geselecteerde metrisch wilt toevoegen.

   ![](../../assets/Add_Dimensions.png)

1. Als u door om het even welke gegevensdimensies op rapporten wilt segmenteren of groeperen, zorg ervoor om erop te wijzen zij zijn _Groeperen_.

1. Klikken **[!UICONTROL Add]**.

## Afmetingen van meerdere meeteenheden verwijderen

Een of meer dimensies uit meerdere metrics verwijderen:

1. Ga naar **[!UICONTROL Data > Metrics]**.

1. Klikken **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Kies de tabel die de afmetingen bevat.

1. Selecteer de metrics die u aan de linkerkant wilt verwijderen en de afmetingen die u aan de rechterkant wilt verwijderen.

1. Klikken **[!UICONTROL Remove]**.

1. Als de afmetingen in gebruik zijn in rapporten, wordt een waarschuwing weergegeven met de lijst met diagrammen die de afmetingen gebruiken. Klikken **[!UICONTROL Delete]** om de gecontroleerde afmetingen en al hun afhankelijke personen, met inbegrip van rapporten te schrappen.

## Dimensies beheren in metriek

**Dimensies toevoegen in metrisch:**

1. Ga naar **[!UICONTROL Data > Metrics]**.

1. Klikken **[!UICONTROL Edit]** op metrisch wilt u een nieuwe afmeting.

1. In het dialoogvenster `Dimensions` gebruiken `Add a dimension` vervolgkeuzelijst om de dimensie te selecteren die u wilt toevoegen.

>[!NOTE]
>
>Elke dimensie waarop u wilt filteren of groeperen, moet al worden bijgehouden [!DNL Commerce Intelligence]. Als u niet de gewenste afmeting vindt, moet u mogelijk een nieuwe gegevenskolom in uw database volgen via de [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.


**Dimensie(s) verwijderen uit metrisch:**

1. Ga naar **[!UICONTROL Manage Data > Metrics]**.

1. Klikken **[!UICONTROL Edit]** op de metrische basis wilt u een nieuwe dimensie.

1. Onder de `Dimensions` schakelt u het selectievakje in de kolom Verwijderen in naast de afmetingen die u wilt verwijderen.

>[!NOTE]
>
>Zelfs na het schrappen van een afmeting, bestaat het nog als kolom op uw lijst in uw Data Warehouse. U kunt het aan om het even welke metrisch toevoegen, en nieuwe metriek bouwen gebruikend deze afmetingen. Om de gegevenskolom te verwijderen waarvan een afmeting beantwoordt aan [!DNL Commerce Intelligence], maakt u de gegevenskolom eenvoudig ongedaan via de [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.

## Gerelateerde documentatie

* [Aanbevolen procedures voor segmentatie en filteren](../../best-practices/segment-filter.md)
