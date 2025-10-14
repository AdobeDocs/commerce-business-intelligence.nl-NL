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

Om [!DNL CJ Affiliate (Commission Junction)] gegevens in [!DNL Adobe Commerce Intelligence] in te voeren, volg eenvoudig de stappen hieronder en maak het resulterende dossier aan a [&#x200B; steunkaartje &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) vast. Adobe stelt de datatabel in op uw account en kunt gegevens onafhankelijk blijven uploaden.

## [!DNL CJ Affiliate] -gegevens exporteren

1. Ga in uw [!DNL CJ Affiliate] -account naar de tab `Reports` .

1. Selecteer op het tabblad `Performance` de optie `Report Options` .

1. Stel `Performance By` in op `Program` `Trend` gelijk aan `Daily` en `Date Range` gelijk aan het datumbereik dat wordt gecontroleerd.

   ![&#x200B; uitvoer-cj-gelieerde-gegevens &#x200B;](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selecteer `Run Report` .

1. Selecteer `File Format` in het vervolgkeuzemenu `CSV` .  Klik op **[!UICONTROL Download]**.

   ![&#x200B; uitvoer cj partnergegevens &#x200B;](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Nadat u het dossier hebt gedownload, kunt u [&#x200B; het dossier &#x200B;](../connecting-data/using-file-uploader.md) uploaden aan uw [!DNL Commerce Intelligence] Data Warehouse.

   Zo maakt u een tabel in uw [!DNL Commerce Intelligence] Data Warehouse waarin u regelmatig nieuwe gegevens kunt uploaden. Wanneer het uploaden van het dossier, volg de het formatteren vereisten die in [&#x200B; worden vermeld Gebruikend het Dossier uploader &#x200B;](../connecting-data/using-file-uploader.md).
