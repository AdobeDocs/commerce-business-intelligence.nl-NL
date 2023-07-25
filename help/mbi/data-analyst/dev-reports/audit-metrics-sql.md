---
title: Werken met SQL Report Builder
description: Leer hoe te om gegevens en metriek te controleren gebruikend SQL Report Builder zodat u de resultaten met de gegevens van uw lokale gegevensbestand kunt vergelijken.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

De [!DNL SQL Report Builder] wordt hoofdzakelijk gebruikt om nieuwe rapporten te bouwen en op analyses te herhalen, maar het kan ook worden gebruikt om gegevens en metriek effectief te controleren. De volgende informatie verklaart hoe te om gegevens en metriek te controleren gebruikend [!DNL SQL Report Builder] zodat u de resultaten kunt vergelijken met de gegevens uit uw lokale database.

## Metrisch zoeken

Om aan de slag te gaan, opent u de [!DNL SQL Report Builder] door te navigeren naar **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. U kunt de zijbalk in het dialoogvenster [!DNL SQL] redacteur om metrisch direct in uw vraag op te nemen door over metrisch te hangen en te klikken **[!UICONTROL Insert]**. Dit voegt de vraagdefinitie van dat metrisch aan de redacteur toe. De definitie omvat de volgende componenten:

- De **metrische bewerking** wordt uitgevoerd, aangeduid door `SUM()` in het onderstaande voorbeeld.
- De **tabel op** die de metrische waarde wordt opgebouwd, aangegeven door de `FROM` clausule.
- Alle **filters (en filtersets)** die aan de metrische waarde zijn toegevoegd, aangegeven door de `WHERE` in het onderstaande voorbeeld.
- De component van de **tijdstempel** (jaar, maand) waarop de gegevens moeten worden besteld, aangegeven door de `ORDER BY` in het onderstaande voorbeeld.

Als u een duidelijkere weergave van de query wilt, kunt u de opmaak van de query wijzigen in het queryveld. Indien gereed, selecteert u `Run Query`. De resultaten bevolken als lijst in het rapportpaneel onder de vraag.

![](../../assets/run-query-results.gif)

## De query beperken

Als u probeert om een specifieke discrepantie of een reeks gegevens te identificeren, zou u de vraag tot een specifieke steekproef moeten beperken om tegen uw lokale gegevensbestand te controleren. U kunt dit doen door de vraag uit te geven om uw gewenste beperkingen aan te passen. In het volgende voorbeeld, beperkt u de vraag om slechts opbrengst van 1 Januari, 2013 of later te omvatten. Nadat u de query hebt bijgewerkt, selecteert u **[!UICONTROL Run Query]** om de resultaten bij te werken.

![](../../assets/restricting-query.gif)

## Opslaan en exporteren

Als het rapport aan uw behoeften voldoet, geeft u het rapport een andere naam. Klik op **[!UICONTROL Save]** en selecteer het type rapport dat u wilt opslaan en het dashboard. Adobe raadt aan het rapport op te slaan als een `Table` en het opslaan naar een testdashboard.

Nadat het rapport is opgeslagen, navigeert u naar dat dashboard door `Go to Dashboard`. Van daar kunt u de gegevens uitvoeren door het rapport te vinden en te selecteren **[!UICONTROL Options gear > Full `.csv`Exporteren]** of **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Aangepaste query&#39;s

U kunt ook aangepaste query&#39;s schrijven en de resultaten exporteren die u wilt vergelijken met uw lokale database. Na de [richtlijnen voor queryoptimalisatie](../../best-practices/optimizing-your-sql-queries.md), schrijft u een query in de SQL-editor. U kunt de knoppen boven aan het zijpaneel gebruiken om te schakelen tussen lijsten met tabellen en metriek die beschikbaar zijn voor gebruik in het dialoogvenster [!DNL SQL Report Builder] en voeg deze toe aan uw query. Wanneer uw douanequery uw behoeften past, kunt u het rapport opslaan en die gegevens van het dashboard uitvoeren.

>[!NOTE]
>
>Als u na het controleren van uw gegevens een discrepantie vindt, bekijkt u [Contact opnemen met ondersteuning: Gegevensdiscrepanties](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) onderwerp van de steun voor meer informatie over wat te doen daarna.
