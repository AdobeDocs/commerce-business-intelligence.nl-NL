---
title: Gegevensafmetingen beheren
description: Leer wat een afmeting is en het kan worden gebruikt om grafieken te filtreren of te segmenteren die op metrisch worden gebaseerd.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Gegevensafmetingen beheren

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

Een dimensie is een gebied in de zelfde lijst zoals metrisch die aan filter of segmentgrafieken kan worden gebruikt die op dat metrisch worden gebaseerd. Een maatstaf voor inkomsten kan bijvoorbeeld stad, staat, land, orderstatus, couponcode en andere typen afmetingen bevatten.

## Afmetingen toevoegen aan meerdere metriek

Een of meer afmetingen tegelijk toevoegen aan meerdere metriek:

1. Ga naar **[!UICONTROL Manage Data > Metrics]**.

1. Klik op **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Kies de tabel die de afmetingen bevat.

1. In de `Choose Metric(s) to Add Dimensions` selecteert u de metriek waaraan u afmetingen wilt toevoegen. Als deze optie is geselecteerd, wordt `Choose Dimensions to Add` wordt rechts in het scherm weergegeven. Controleer de afmetingen die u aan geselecteerde metrisch wilt toevoegen.

   ![](../../assets/Add_Dimensions.png)

1. Als u door om het even welke gegevensdimensies op rapporten wilt segmenteren of groeperen, zorg ervoor om erop te wijzen zij zijn _Groeperen_.

1. Klik op **[!UICONTROL Add]**.

## Afmetingen van meerdere meeteenheden verwijderen

Een of meer afmetingen uit meerdere meeteenheden verwijderen:

1. Ga naar **[!UICONTROL Data > Metrics]**.

1. Klik op **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Kies de tabel die de afmetingen bevat.

1. Selecteer de afmetingen die u links wilt verwijderen en de afmetingen die u wilt verwijderen aan de rechterkant.

1. Klik op **[!UICONTROL Remove]**.

1. Als de afmetingen in gebruik zijn in rapporten, wordt een waarschuwing weergegeven met de lijst met grafieken die de afmetingen gebruiken. Klikken **[!UICONTROL Delete]** om de gecontroleerde afmetingen en al hun afhankelijke personen, met inbegrip van rapporten te schrappen.

## Dimensies beheren in metriek

**Dimensies toevoegen in metrische vorm:**

1. Ga naar **[!UICONTROL Data > Metrics]**.

1. Klikken **[!UICONTROL Edit]** op metrisch wilt u een nieuwe afmeting.

1. In de `Dimensions` de sectie gebruiken `Add a dimension` vervolgkeuzelijst om een dimensie te selecteren die u wilt toevoegen.

>[!NOTE]
>
>Elke dimensie waarop u wilt filteren of groeperen, moet al worden bijgehouden [!DNL Commerce Intelligence]. Als u de gewenste dimensie niet vindt, moet u mogelijk een nieuwe gegevenskolom in uw database volgen via de [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.


**Dimensies verwijderen uit metrische gegevens:**

1. Ga naar **[!UICONTROL Manage Data > Metrics]**.

1. Klikken **[!UICONTROL Edit]** op metrisch wilt u een nieuwe afmeting.

1. Onder de `Dimensions` selecteert u het selectievakje in de kolom Verwijderen naast de dimensie(en) die u wilt verwijderen.

>[!NOTE]
>
>Zelfs na het schrappen van een afmeting, bestaat het nog als kolom op uw lijst in uw Data Warehouse. U kunt het aan om het even welke metrisch toevoegen, en nieuwe metriek bouwen gebruikend deze dimensies. Om de gegevenskolom te verwijderen waarvan een afmeting beantwoordt aan [!DNL Commerce Intelligence], maakt u de gegevenskolom eenvoudig ongedaan via de [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.

## Gerelateerde documentatie

* [Aanbevolen procedures voor segmentatie en filteren](../../best-practices/segment-filter.md)
