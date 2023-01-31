---
title: Gegevensafmetingen beheren
description: Leer hoe gegevens worden geproduceerd, wat precies veroorzaakt dat een nieuwe rij in één van de Handel van de Kern wordt opgenomen hoe acties zoals het maken van een aankoop of het creëren van een rekening in het gegevensbestand van de Handel wordt geregistreerd.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Gegevensafmetingen beheren

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

Een dimensie is een gebied in de zelfde lijst zoals metrisch die aan filter of segmentgrafieken kan worden gebruikt die op dat metrisch worden gebaseerd. Een maatstaf van inkomsten kan bijvoorbeeld stad, staat, land, orderstatus, couponcode en andere soorten dimensies bevatten.

## Afmetingen toevoegen aan meerdere metriek

Een of meer afmetingen tegelijk toevoegen aan meerdere metriek:

1. Ga op de hoofdnavigatiebalk naar **[!UICONTROL Manage Data > Metrics]**.

1. Klik boven aan de pagina op **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Kies de tabel die de afmetingen bevat.

1. In de `Choose Metric(s) to Add Dimensions` selecteert u de metriek waaraan u afmetingen wilt toevoegen. Als deze optie is geselecteerd, wordt `Choose Dimensions to Add` wordt rechts in de kolom weergegeven. Controleer de afmetingen die u aan de geselecteerde metrische waarde wilt toevoegen.

   ![](../../assets/Add_Dimensions.png)

1. Als u door om het even welke gegevensdimensies op rapporten wilt segmenteren of groeperen, zorg ervoor om erop te wijzen zij zijn _Groeperen_.

1. Klikken **[!UICONTROL Add]**.

## Afmetingen van meerdere meeteenheden verwijderen

Een of meer afmetingen uit meerdere meeteenheden verwijderen:

1. Ga op de hoofdnavigatiebalk naar **[!UICONTROL Data > Metrics]**.

1. Klik boven aan de pagina op **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Kies de tabel die de afmetingen bevat.

1. Selecteer de metriek u de afmetingen van op de linkerzijde, en de afmetingen wilt verwijderen u op het recht.

1. Klikken **[!UICONTROL Remove]**.

1. Als de afmetingen in gebruik zijn in rapporten, zult u een waarschuwing en een lijst van grafieken worden getoond die de afmetingen gebruiken. Klikken **[!UICONTROL Delete]** om de gecontroleerde afmetingen en al hun afhankelijke personen, met inbegrip van rapporten te schrappen.

## Dimensies beheren in metriek

**Dimensies toevoegen in metrisch:**

1. Ga op de hoofdnavigatiebalk naar **[!UICONTROL Data > Metrics]**.

1. Klikken **[!UICONTROL Edit]** op metrisch wilt u een nieuwe afmeting.

1. Onder de `Dimensions` de sectie gebruiken `Add a dimension` vervolgkeuzelijst om een dimensie te selecteren die u wilt toevoegen.

>[!NOTE]
>
>Elke dimensie waarop u wilt filteren of groeperen, moet al worden bijgehouden [!DNL MBI]. Als u niet de gewenste afmeting vindt, moeten wij misschien beginnen een nieuwe gegevenskolom in uw gegevensbestand via te volgen [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.


**Dimensies verwijderen uit metrische gegevens:**

1. Ga op de hoofdnavigatiebalk naar **[!UICONTROL Manage Data > Metrics]**.

1. Klikken **[!UICONTROL Edit]** op metrisch wilt u een nieuwe afmeting.

1. Onder de `Dimensions` selecteert u het selectievakje in de kolom Verwijderen naast de dimensie(en) die u wilt verwijderen.

>[!NOTE]
>
>Zelfs na het schrappen van een afmeting, bestaat het nog als kolom op uw lijst in ons gegevenspakhuis. U kunt het aan om het even welke metrisch toevoegen, en nieuwe metriek bouwen gebruikend deze afmetingen. Als u de gegevenskolom wilt verwijderen, komt een dimensie overeen met [!DNL MBI], maakt u de gegevenskolom eenvoudig ongedaan via de [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.

## Gerelateerde documentatie

* [Aanbevolen procedures voor segmentatie en filteren](../../best-practices/segment-filter.md)
