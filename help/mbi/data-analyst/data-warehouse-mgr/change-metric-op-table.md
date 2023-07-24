---
title: De operationele tabel van een metrische waarde wijzigen
description: Leer hoe te om de gegevenslijst te veranderen die metrisch gebruikt om zijn verrichting uit te voeren.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# De operationele tabel van een metrische waarde wijzigen

In bepaalde gevallen, kunt u besluiten om de gegevenslijst te veranderen die metrisch gebruikt om zijn verrichting uit te voeren. Als u bijvoorbeeld een nieuwe gebruikerstabel hebt, wilt u de gegevens die betrekking hebben op de gebruiker migreren uit de  `Users\_Old` de tabel `Users\_New` in plaats daarvan.

1. Ga naar **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Klikken **[!UICONTROL Edit]** naast metrisch waarvoor u zou willen schakelen `operational` tabel.
1. Klik in de editor op **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Selecteer de nieuwe lijst die u deze metrisch op wilt baseren.
1. Pas de bestaande gegevensafmetingen aan de corresponderende in de nieuwe tabel aan. Als u bijvoorbeeld een kolom hebt met de naam `User's registration date`selecteert u gewoon welke kolom in de nieuwe tabel dezelfde datumgegevens bevat. (Zie de volgende stap als de nieuwe tabel geen overeenkomende kolommen bevat.)

   ![](../../assets/change-metrics-2.png)

1. Als de nieuwe tabel geen overeenkomende kolom bevat, kunt u **maken in uw datatabel** of [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) als het een berekeningskolom of -dimensie betreft, gemaakt door [!DNL Commerce Intelligence]. U kunt ook **de dimensie verwijderen uit de metrische**. Om een afmeting te schrappen die u niet meer nodig hebt, ga eenvoudig terug naar de metrische redacteur en selecteer welke afmetingen onder te schrappen `Dimensions`.

   ![](../../assets/change-metrics-3.png)
