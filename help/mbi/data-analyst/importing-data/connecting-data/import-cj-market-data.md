---
title: Importeren van CJ-filiaal (Commission Juncate)
description: Leer om CJ gelieerde gegevens (Commission Junction) in te voeren [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Importeren `CJ Affiliate` data

Om te importeren `CJ Affiliate` (Commission Junction) gegevens in [!DNL MBI]Volg gewoon de onderstaande stappen en koppel het resulterende bestand aan een ondersteuningsticket. We stellen de datatabel voor uw account in en stellen u in staat onafhankelijk gegevens te uploaden.

## Exporteren `CJ Affiliate` Gegevens

1. In uw `CJ Affiliate` account, ga naar `Reports` tab.

1. In de `Performance` tab, selecteert u `Report Options`.

1. Set `Performance By` gelijk aan `Program`, `Trend` gelijk aan `Daily`, en `Date Range` gelijk aan het datumbereik dat wordt gecontroleerd.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecteren `Run Report`.

1. In de `File Format` vervolgkeuzelijst, selecteren `CSV`.  Klikken **[!UICONTROL Download]**.

   ![cj-filiaalgegevens exporteren](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Nadat u het bestand hebt gedownload, kunt u [uploadt het bestand](../connecting-data/using-file-uploader.md) aan uw [!DNL MBI] data-entrepot.

   Hiermee maakt u een nieuwe tabel in uw [!DNL MBI] gegevenspakhuis dat u kunt blijven nieuwe gegevens in periodiek uploaden. Houd er bij het uploaden van het bestand rekening mee dat u de opmaakvereisten van de volgende [Bestanden uploader gebruiken](../connecting-data/using-file-uploader.md).
