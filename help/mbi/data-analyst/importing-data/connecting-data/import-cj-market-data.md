---
title: Importeren van CJ-filiaal (Commission Juncate)
description: Leer om CJ gelieerde gegevens (Commission Junction) in te voeren [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Importeren `CJ Affiliate` data

Om te importeren `CJ Affiliate` (Commission Junction) gegevens in [!DNL MBI]Volg gewoon de onderstaande stappen en koppel het resulterende bestand aan een ondersteuningsticket. Adobe zal de datatabel voor uw account instellen en u kunt gegevens onafhankelijk blijven uploaden.

## Exporteren `CJ Affiliate` Gegevens

1. In uw `CJ Affiliate` account, ga naar `Reports` tab.

1. In de `Performance` tab, selecteert u `Report Options`.

1. Set `Performance By` gelijk aan `Program`, `Trend` gelijk aan `Daily`, en `Date Range` gelijk aan het datumbereik dat wordt gecontroleerd.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecteren `Run Report`.

1. In de `File Format` vervolgkeuzelijst, selecteren `CSV`.  Klikken **[!UICONTROL Download]**.

   ![cj-filiaalgegevens exporteren](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Nadat u het bestand hebt gedownload, kunt u [uploadt het bestand](../connecting-data/using-file-uploader.md) aan uw [!DNL MBI] Data Warehouse.

   Hiermee maakt u een tabel in uw [!DNL MBI] Data Warehouse dat u regelmatig nieuwe gegevens kunt blijven uploaden. Houd er bij het uploaden van het bestand rekening mee dat u de opmaakvereisten van [Bestanden uploader gebruiken](../connecting-data/using-file-uploader.md).
