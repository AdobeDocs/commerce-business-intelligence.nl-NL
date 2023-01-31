---
title: Financiële gegevens opmaken en importeren
description: Leer hoe u financiële gegevens opmaakt en importeert.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Financiële gegevens opmaken en importeren

Dit onderwerp bespreekt de beste manier om financiële gegevens voor analyse in te voeren [!DNL MBI].

Een tweedimensionale, cross-tab gegevenstabel is vaak de indeling die wordt gebruikt voor financiële gegevens. Met waarden die door labels in zowel kolommen als rijen worden gecategoriseerd, kan dit type lay-out gemakkelijk zijn om met menselijke ogen en spreadsheethulpmiddelen te bekijken, maar het is niet zeer vriendelijk aan gegevensbestanden.

![](../../mbi/assets/crosstab.png)

Deze gegevens importeren en analyseren in [!DNL MBI], moet de tabel worden samengevoegd tot een eendimensionale lijst. Wanneer samengevoegd, wordt elke gegevenswaarde gecategoriseerd door veelvoudige etiketten die allen in één enkele rij zijn, waar elke rij uniek is of een uniek herkenningsteken, bijvoorbeeld een primaire zeer belangrijke kolom zou hebben.

![](../../mbi/assets/flattened.png)

## Excel-bestanden opmaken voor importeren

Een tweedimensionale tabel samenvoegen met een Excel-draaientabel:

1. Open het bestand met de tweedimensionale gegevenstabel.
1. Open de Wizard draaitabellen. In Windows is de sneltoets `Alt-D`. Typ in Mac OSX `Command-Option-P`.
1. Selecteren **[!UICONTROL Multiple consolidated ranges]** en klik op **[!UICONTROL Next]**.
1. Selecteren **[!UICONTROL I will create the page fields]** en klik op **[!UICONTROL Next]**.
1. Selecteer de volledige gegevensset in de tweedimensionale tabel, inclusief de labels. Zorg ervoor dat `0` is geselecteerd voor het aantal gewenste paginavelden en klik op **[!UICONTROL Next]**.
1. De draaientabel maken in een nieuw vel en klikken op **[!UICONTROL Finish]**.
1. Schakel de kolom- en rijvelden uit in de veldlijst.
1. Dubbelklik op de resulterende numerieke waarde om de samengevoegde brongegevens in een nieuw blad weer te geven.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Opslaan als een `CSV` bestand.

Dat is het! De gegevenstabel is omgezet in een lijstformaat, dat al zijn originele informatie bewaart, en kan nu worden [geïmporteerd in [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) voor analyse.
