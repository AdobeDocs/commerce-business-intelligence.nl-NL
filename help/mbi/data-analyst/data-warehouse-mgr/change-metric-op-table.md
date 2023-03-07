---
title: De operationele tabel van een metrische waarde wijzigen
description: Leer hoe te om de gegevenslijst te veranderen die metrisch gebruikt om zijn verrichting uit te voeren.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# De operationele tabel van een metrische waarde wijzigen

In bepaalde gevallen, kunt u besluiten om de gegevenslijst te veranderen die metrisch gebruikt om zijn verrichting uit te voeren. Als u bijvoorbeeld een nieuwe gebruikerstabel hebt, wilt u de gegevens die betrekking hebben op de gebruiker migreren uit de tabel &quot;Gebruikers\_Oud&quot; om in plaats daarvan de tabel &quot;Gebruikers\_Nieuw&quot; te gebruiken.

1. Ga naar **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Klikken **[!UICONTROL Edit]** naast metrisch waarvoor u zou willen schakelen `operational` tabel.
1. Klik in de editor op **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Selecteer nu de nieuwe lijst die u deze metrisch op wilt baseren.
1. Vervolgens moet u de bestaande gegevensafmetingen aanpassen aan de corresponderende in de nieuwe tabel. Als u bijvoorbeeld een kolom hebt met de naam `User's registration date`selecteert u gewoon welke kolom in de nieuwe tabel dezelfde datumgegevens bevat. (Zie de volgende stap als de nieuwe tabel geen overeenkomende kolommen bevat.)

   ![](../../assets/change-metrics-2.png)

1. Als de nieuwe tabel geen overeenkomende kolom bevat, kunt u **maken in uw datatabel** of [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) als het een berekeningskolom of -dimensie betreft, gemaakt door [!DNL MBI]). U kunt ook **de dimensie verwijderen uit de metrische**. Om een afmeting te schrappen die u niet meer nodig hebt, ga eenvoudig terug naar de metrische redacteur en selecteer welke afmetingen onder te schrappen `Dimensions`.

   ![](../../assets/change-metrics-3.png)
