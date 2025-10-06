---
title: Financiële gegevens opmaken en importeren
description: Leer hoe u financiële gegevens opmaakt en importeert.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Financiële gegevens opmaken en importeren

In dit onderwerp wordt de beste manier besproken om financiële gegevens te importeren voor analyse in [!DNL Adobe Commerce Intelligence] .

Een tweedimensionale, cross-tab gegevenstabel is vaak de indeling die wordt gebruikt voor financiële gegevens. Met waarden die door labels in zowel kolommen als rijen worden gecategoriseerd, zou dit type lay-out gemakkelijk met menselijke ogen en spreadsheethulpmiddelen kunnen zijn, maar het is niet vriendschappelijk aan gegevensbestanden.

![&#x200B; formaat Crosstab dat gegevens in de lay-out van de spillijst toont &#x200B;](../../mbi/assets/crosstab.png)

Als u deze gegevens wilt importeren en analyseren in [!DNL Commerce Intelligence] , moet u de tabel samenvoegen tot een eendimensionale lijst. Wanneer samengevoegd, wordt elke gegevenswaarde gecategoriseerd door veelvoudige etiketten die allen in één enkele rij zijn, waar elke rij uniek is of een uniek herkenningsteken, bijvoorbeeld een primaire zeer belangrijke kolom zou hebben.

![&#x200B; afgevlakt formaat dat gegevens in kolomlay-out toont &#x200B;](../../mbi/assets/flattened.png)

## Excel-bestanden opmaken voor importeren

Een tweedimensionale tabel afvlakken met een [!DNL Excel] draaientabel:

1. Open het bestand met de tweedimensionale gegevenstabel.
1. Open de Wizard draaitabellen. In [!DNL Windows] is de sneltoets `Alt-D` . Voer in [!DNL Mac OS] `Command-Option-P` in.
1. Selecteer **[!UICONTROL Multiple consolidated ranges]** en klik op **[!UICONTROL Next]** .
1. Selecteer **[!UICONTROL I will create the page fields]** en klik op **[!UICONTROL Next]** .
1. Selecteer de volledige gegevensset in de tweedimensionale tabel, inclusief de labels. Zorg ervoor dat `0` is geselecteerd voor het aantal gewenste paginavelden en klik op **[!UICONTROL Next]** .
1. Maak de draaitabel in een nieuw vel en klik op **[!UICONTROL Finish]** .
1. Schakel de kolom- en rijvelden uit in de veldlijst.
1. Dubbelklik op de resulterende numerieke waarde om de samengevoegde brongegevens in een nieuw blad weer te geven.
   ![&#x200B; de lijst van het het kantellijstgebied van Excel die tweemaal klikken om uit te breiden &#x200B;](../../mbi/assets/pivot-table-double-click.png)
1. Opslaan als een `CSV` -bestand.

## Omloop omhoog

De gegevenslijst is omgezet in een lijstformaat, dat al zijn originele informatie bewaart, en kan nu [&#x200B; worden ingevoerd aan  [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) voor analyse.
