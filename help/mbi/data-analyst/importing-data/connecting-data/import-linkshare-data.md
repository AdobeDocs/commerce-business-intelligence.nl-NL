---
title: Koppelingsgegevens importeren
description: Leer om gegevens van Linksys in  [!DNL Commerce Intelligence] in te voeren.
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---

# [!DNL Linkshare] -gegevens importeren

Als u uw [!DNL Linkshare] gegevens wilt overbrengen naar [!DNL Adobe Commerce Intelligence] , moet u twee dingen doen:

1. [De gegevens van Linksys uitvoeren in ](#export)
1. [De spreadsheet uploaden naar  [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Gegevens exporteren uit Linkshare {#export}

1. Ga in uw [!DNL Linkshare] -account naar **[!UICONTROL Reports** > **Run Reports].**

1. Selecteer **[!UICONTROL Sales & Activity Report]** in het vervolgkeuzemenu `Report` .

1. Laat alle andere vervolgkeuzemogelijkheden de standaardselectie.

1. Selecteer in het vervolgkeuzemenu `Date Range` de optie ( `Sun - Sat` , `Mon - Sun` ) die overeenkomt met de instellingen in `Start of Week` [!DNL Commerce Intelligence] .

1. Schakel het selectievakje `Compare Year-Over-Year Data` uit.

1. Selecteer onder `Data Type` de optie `Transaction Date` .

   ![ het invoeren \_linkshare\_data.png ](../../../assets/importing_linkshare_data.png)

1. Klik op **[!UICONTROL View Report]**.

1. Klik op **[!UICONTROL Download]**.

   Op dit punt wordt een `.csv` -bestand gedownload.

Nadat het dossier wordt gedownload, kunt u het aan [!DNL Commerce Intelligence] uploaden gebruikend de [`File Upload` eigenschap ](../connecting-data/using-file-uploader.md).
