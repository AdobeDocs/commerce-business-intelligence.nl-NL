---
title: Importeren van CJ-filiaal (Commission Juncate)
description: Leer CJ-gelieerde gegevens (Commission Junction) importeren in  [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack;.
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# [!DNL CJ Affiliate] -gegevens importeren

Om [!DNL CJ Affiliate (Commission Junction)] gegevens in [!DNL Adobe Commerce Intelligence] in te voeren, volg eenvoudig de stappen hieronder en maak het resulterende dossier aan a [ steunkaartje ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) vast. Met Adobe wordt de datatabel voor uw account ingesteld en kunt u gegevens onafhankelijk blijven uploaden.

## [!DNL CJ Affiliate] -gegevens exporteren

1. Ga in uw [!DNL CJ Affiliate] -account naar de tab `Reports` .

1. Selecteer op het tabblad `Performance` de optie `Report Options` .

1. Stel `Performance By` in op `Program` `Trend` gelijk aan `Daily` en `Date Range` gelijk aan het datumbereik dat wordt gecontroleerd.

   ![ uitvoer-cj-gelieerde-gegevens ](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecteer `Run Report` .

1. Selecteer `CSV` in het vervolgkeuzemenu `File Format` .  Klik op **[!UICONTROL Download]**.

   ![ uitvoer cj partnergegevens ](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Nadat u het dossier hebt gedownload, kunt u [ het dossier ](../connecting-data/using-file-uploader.md) aan uw [!DNL Commerce Intelligence] Data Warehouse uploaden.

   Zo maakt u in de Data Warehouse [!DNL Commerce Intelligence] een tabel waarin u regelmatig nieuwe gegevens kunt uploaden. Wanneer het uploaden van het dossier, volg de het formatteren vereisten die in [ worden vermeld Gebruikend het Dossier uploader ](../connecting-data/using-file-uploader.md).
