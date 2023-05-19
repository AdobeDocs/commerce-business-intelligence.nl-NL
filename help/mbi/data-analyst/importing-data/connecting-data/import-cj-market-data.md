---
title: Importeren van CJ-filiaal (Commission Juncate)
description: Leer om CJ gelieerde gegevens (Commission Junction) in te voeren [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Importeren [!DNL CJ Affiliate] data

Om te importeren [!DNL CJ Affiliate (Commission Junction)] gegevens in [!DNL Adobe Commerce Intelligence]volgt u gewoon de onderstaande stappen en voegt u het resulterende bestand toe aan een [ondersteuningsticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe zal de datatabel voor uw account instellen en u kunt gegevens onafhankelijk blijven uploaden.

## Exporteren [!DNL CJ Affiliate] Gegevens

1. In uw [!DNL CJ Affiliate] account, ga naar `Reports` tab.

1. In de `Performance` tab, selecteert u `Report Options`.

1. Set `Performance By` gelijk aan `Program`, `Trend` gelijk aan `Daily`, en `Date Range` gelijk aan het datumbereik dat wordt gecontroleerd.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecteren `Run Report`.

1. In de `File Format` vervolgkeuzelijst, selecteren `CSV`.  Klikken **[!UICONTROL Download]**.

   ![cj-filiaalgegevens exporteren](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Nadat u het bestand hebt gedownload, kunt u [uploadt het bestand](../connecting-data/using-file-uploader.md) aan uw [!DNL Commerce Intelligence] Data Warehouse.

   Hiermee maakt u een tabel in uw [!DNL Commerce Intelligence] Data Warehouse dat u regelmatig nieuwe gegevens kunt blijven uploaden. Volg bij het uploaden van het bestand de opmaakvereisten van [Bestanden uploader gebruiken](../connecting-data/using-file-uploader.md).
