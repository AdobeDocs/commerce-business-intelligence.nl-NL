---
title: Werken met SQL Report Builder
description: Leer hoe u gegevens en metriek kunt controleren gebruikend SQL Report Builder zodat u de resultaten met de gegevens van uw lokale gegevensbestand kunt vergelijken.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

[!DNL SQL Report Builder] wordt hoofdzakelijk gebruikt om nieuwe rapporten te bouwen en op analyses te herhalen, maar het kan ook worden gebruikt om gegevens en metriek effectief te controleren. De volgende informatie laat zien hoe u gegevens en metriek kunt controleren met behulp van [!DNL SQL Report Builder] , zodat u de resultaten kunt vergelijken met de gegevens uit uw lokale database.

## Metrisch zoeken

Open om te beginnen de [!DNL SQL Report Builder] door naar **[!UICONTROL Report Builder > SQL Report Builder > Create Report]** te navigeren. Met de zijbalk in de [!DNL SQL] -editor kunt u een metrische waarde rechtstreeks in de query invoegen door de muisaanwijzer boven de metrische waarde te houden en op **[!UICONTROL Insert]** te klikken. Dit voegt de vraagdefinitie van dat metrisch aan de redacteur toe. De definitie omvat de volgende componenten:

- De **metrische verrichting** die, door `SUM()` in het hieronder voorbeeld wordt vermeld wordt uitgevoerd.
- De **lijst op** die metrisch wordt gebouwd, die door de `FROM` clausule wordt vermeld.
- Om het even welke **filters (en filterreeksen)** die aan metrisch zijn toegevoegd, die door de `WHERE` clausule in het hieronder voorbeeld wordt vermeld.
- De component van **timestamp** (jaar, maand) waarop de gegevens moeten worden bevolen, die door de `ORDER BY` clausule in het hieronder voorbeeld wordt vermeld.

Als u een duidelijkere weergave van de query wilt, kunt u de opmaak van de query wijzigen in het queryveld. Selecteer `Run Query` als u klaar bent. De resultaten bevolken als lijst in het rapportpaneel onder de vraag.

![ Geanimeerde demonstratie van het runnen van SQL vraag en het bekijken resultaten ](../../assets/run-query-results.gif)

## De query beperken

Als u probeert om een specifieke discrepantie of een reeks gegevens te identificeren, zou u de vraag tot een specifieke steekproef moeten beperken om tegen uw lokale gegevensbestand te controleren. U kunt dit doen door de vraag uit te geven om uw gewenste beperkingen aan te passen. In het volgende voorbeeld, beperkt u de vraag om slechts opbrengst van 1 Januari, 2013 of later te omvatten. Nadat u de query hebt bijgewerkt, selecteert u nogmaals **[!UICONTROL Run Query]** om de resultaten bij te werken.

![ Geanimeerde demonstratie van het beperken van vraag met filters ](../../assets/restricting-query.gif)

## Opslaan en exporteren

Wanneer het rapport aan uw behoeften voldoet, geeft u het rapport een andere naam, klikt u op **[!UICONTROL Save]** en selecteert u het type rapport dat u wilt opslaan en het dashboard. Bij het controleren van metriek, adviseert Adobe het rapport als `Table` op te slaan en het op een testdashboard te bewaren.

Nadat het rapport is opgeslagen, navigeert u naar dat dashboard door `Go to Dashboard` te selecteren. Daarna kunt u de gegevens exporteren door het rapport te zoeken en **[!UICONTROL Options gear > Full `.csv`Exporteren]** of **[!UICONTROL Full Excel Export]** te selecteren.

![ Geanimeerde demonstratie van het uitvoeren van dashboardgegevens ](../../assets/export-dboard-data.gif)

## Aangepaste query&#39;s

U kunt ook aangepaste query&#39;s schrijven en de resultaten exporteren die u wilt vergelijken met uw lokale database. Na de [ richtlijnen voor vraagoptimalisering ](../../best-practices/optimizing-your-sql-queries.md), schrijf een vraag in de SQL redacteur. U kunt de knopen bij de bovenkant van sidebar gebruiken om tussen lijsten van lijsten van lijsten en metriek van beschikbare voor gebruik in [!DNL SQL Report Builder] van een knevel te voorzien en hen toe te voegen aan uw vraag. Wanneer uw douanequery uw behoeften past, kunt u het rapport opslaan en die gegevens van het dashboard uitvoeren.

>[!NOTE]
>
>Als u een discrepantie na het controleren van uw gegevens vindt, bekijk [ Contact Steun: De discrepanties van gegevens ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) steunonderwerp voor meer informatie over wat te doen daarna.
