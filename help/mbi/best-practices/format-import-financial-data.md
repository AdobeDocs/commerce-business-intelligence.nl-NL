---
title: Financiële gegevens opmaken en importeren
description: Leer hoe u financiële gegevens opmaakt en importeert.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Financiële gegevens opmaken en importeren

Dit onderwerp bespreekt de beste manier om financiële gegevens voor analyse in te voeren [!DNL Adobe Commerce Intelligence].

Een tweedimensionale, cross-tab gegevenstabel is vaak de indeling die wordt gebruikt voor financiële gegevens. Met waarden die door labels in zowel kolommen als rijen worden gecategoriseerd, zou dit type lay-out gemakkelijk met menselijke ogen en spreadsheethulpmiddelen kunnen zijn, maar het is niet vriendschappelijk aan gegevensbestanden.

![](../../mbi/assets/crosstab.png)

Deze gegevens importeren en analyseren in [!DNL Commerce Intelligence], moet de tabel worden samengevoegd tot een eendimensionale lijst. Wanneer samengevoegd, wordt elke gegevenswaarde gecategoriseerd door veelvoudige etiketten die allen in één enkele rij zijn, waar elke rij uniek is of een uniek herkenningsteken, bijvoorbeeld een primaire zeer belangrijke kolom zou hebben.

![](../../mbi/assets/flattened.png)

## Excel-bestanden opmaken voor importeren

Een tweedimensionale tabel afvlakken met een [!DNL Excel] draaitabel:

1. Open het bestand met de tweedimensionale gegevenstabel.
1. Open de Wizard draaitabellen. In [!DNL Windows], de sneltoets is `Alt-D`. In [!DNL Mac OS], enter `Command-Option-P`.
1. Selecteren **[!UICONTROL Multiple consolidated ranges]** en klik op **[!UICONTROL Next]**.
1. Selecteren **[!UICONTROL I will create the page fields]** en klik op **[!UICONTROL Next]**.
1. Selecteer de volledige gegevensset in de tweedimensionale tabel, inclusief de labels. Zorg ervoor dat `0` is geselecteerd voor het aantal gewenste paginavelden en klik op **[!UICONTROL Next]**.
1. De draaientabel maken in een nieuw vel en klikken op **[!UICONTROL Finish]**.
1. Schakel de kolom- en rijvelden uit in de veldlijst.
1. Dubbelklik op de resulterende numerieke waarde om de samengevoegde brongegevens in een nieuw blad weer te geven.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Opslaan als een `CSV` bestand.

## Omloop omhoog

De gegevenstabel is omgezet in een lijstformaat, dat al zijn originele informatie bewaart, en kan nu worden [geïmporteerd in [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) voor analyse.
