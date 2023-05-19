---
title: Koppelingsgegevens importeren
description: Leer linkshare-gegevens importeren in [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importeren [!DNL Linkshare] data

Om uw [!DNL Linkshare] gegevens in [!DNL Adobe Commerce Intelligence]U moet twee dingen doen:

1. [De gegevens van Linksys uitvoeren in ](#export)
1. [De spreadsheet uploaden naar [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Gegevens exporteren uit Linkshare {#export}

1. In uw [!DNL Linkshare] account, ga naar **[!UICONTROL Reports** > **Run Reports].**

1. In de `Report` vervolgkeuzelijst, selecteren **[!UICONTROL Sales & Activity Report]**.

1. Laat alle andere vervolgkeuzemogelijkheden de standaardselectie.

1. In de `Date Range` vervolgkeuzelijst, selecteer de optie (`Sun - Sat`, `Mon - Sun`) komt overeen met uw `Start of Week` instellingen in [!DNL Commerce Intelligence].

1. Wis de `Compare Year-Over-Year Data` selectievakje.

1. Onder `Data Type`, selecteert u `Transaction Date`.

   ![importeren\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Klikken **[!UICONTROL View Report]**.

1. Klikken **[!UICONTROL Download]**.

   Op dit moment kan een `.csv` en gedownload.

Nadat het bestand is gedownload, kunt u het uploaden naar [!DNL Commerce Intelligence] met de [`File Upload` functie](../connecting-data/using-file-uploader.md).
