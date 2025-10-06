---
title: Raw-gegevens exporteren
description: Leer om verslagen van uw  [!DNL Commerce Intelligence]  Data Warehouse uit te voeren om een dichtere blik te krijgen bij wat uw dashboard aandrijft.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Raw-gegevens exporteren

Met onbewerkte gegevensexportbewerkingen kunt u records uit uw Data Warehouse exporteren om beter te kunnen zien wat het dashboard van kracht maakt. Ook, kunnen de ruwe gegevensuitvoer u [&#x200B; helpen gegevensuitwisselingen &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=nl-NL) aanwijzen.

De uitvoer van ruwe gegevens verleent toegang tot extra kolommen en dimensies die door de-normalisatie en pre-samenvoeging van relevante metriek worden geproduceerd. `User's first order date` is bijvoorbeeld een dimensie die u voor elke gebruiker in [!DNL Commerce Intelligence] kunt exporteren, terwijl deze wellicht niet beschikbaar is in uw database.

Deze zelfstudie behandelt het volgende:

* [Te exporteren gegevens selecteren](#select)
* [De exportbewerking downloaden (](#download)
* [Toegang tot historische exportbewerkingen](#historical)

## Stap 1: Te exporteren gegevens selecteren {#select}

U kunt onbewerkte gegevens op twee manieren exporteren in [!DNL Commerce Intelligence] :

1. op diagramniveau
1. op tabelniveau

### Exporteren op tabelniveau op het tabblad [!UICONTROL Manage Data]

Als u de lijst van [!UICONTROL Manage Data] tabel wilt uitvoeren, hebt u [&#x200B; Admin &#x200B;](../administrator/user-management/user-management.md) toestemmingen nodig.

1. Klik **[!UICONTROL Manage Data** > **&#x200B; de Gegevens van de Uitvoer &#x200B;**> * Onbewerkte Uitvoer van Gegevens]**.
1. Er wordt een `Export List` weergegeven van recent gemaakte gegevens die worden geëxporteerd, indien aanwezig. Klik op **[!UICONTROL Add Export]** om een exportbewerking te maken.
1. Het dialoogvenster `New Raw Data Export` wordt weergegeven. Hier kunt u het exporteren aanpassen door kolommen en filters te selecteren of te deselecteren:

   * `Table` - In het veld `Table` wordt de tabel geselecteerd waaruit gegevens worden geëxporteerd. Standaard wordt hiermee de tabel weergegeven waarin u hebt genavigeerd.
   * `Export Name` - Voer in dit veld de naam van de exportbewerking in. Bijvoorbeeld: `Philadelphia - Daily Revenue` .
   * `Available Columns` - In dit veld worden de kolommen (afmetingen) in uw database weergegeven die beschikbaar zijn voor opname in de exportbewerking. Klik op de naam van een kolom om deze toe te voegen.
   * `Selected Columns` - In dit veld worden de kolommen (afmetingen) weergegeven die momenteel zijn opgenomen in de exportbewerking. Klik op de naam van een kolom om deze te verwijderen.
   * `Filter` - Deze sectie bevat een lijst met de filters die momenteel op het exporteren worden toegepast. Deze filters kunnen worden gewijzigd; de nieuwe filters kunnen ook worden toegevoegd om een bepaalde dataset uit te voeren.
   * Klik op **[!UICONTROL Export Data]** als u klaar bent.

### Exporteren op grafiekniveau vanaf het dashboard

1. Klik op het tandwielpictogram in de rechterbovenhoek van een diagram.

1. Selecteer `Raw Export` in het vervolgkeuzemenu om het dialoogvenster `Raw Export` weer te geven.

1. Pas het exporteren aan door de opties `table` , `columns` en `filters` te kiezen om het exporteren in of uit te sluiten. Raadpleeg de vorige sectie voor meer informatie over de velden in deze module.

   >[!NOTE]
   >
   >De tabel die in het veld `Table` wordt weergegeven, is standaard de tabel die de grafiek aandrijft.

1. Klik op **[!UICONTROL Export Data]** als u klaar bent.

Bekijk het volledige proces op het grafiekniveau.

![&#x200B; Geanimeerde demonstratie van het uitvoeren van ruwe gegevens van een grafiek &#x200B;](../assets/Chart-level_export.gif)

## Stap 2: De export downloaden {#download}

Het exporteren wordt direct na het voltooien van de selecties in het dialoogvenster `Raw Data Export` gestart. Omdat sommige exporten groot kunnen zijn, zijn ze beperkt tot 10 miljoen rijen en kunnen ze enige tijd in beslag nemen.

Als u wilt controleren of het exporteren gereed is, klikt u op **[!UICONTROL Raw Data Exports]** in de rechterbovenhoek van het scherm. Klik op **[!UICONTROL Download]** om een gecomprimeerd `.csv` bestand van uw exportbewerking te downloaden.

![&#x200B; Geanimeerde demonstratie van het downloaden van een uitgevoerd Csv- dossier &#x200B;](../assets/Downloading_export.gif)

## Stap 3: Toegang tot Historische uitvoer {#historical}

Klik op **[!UICONTROL Raw Data Export]** in de rechterbovenhoek van het scherm om uw eerdere exportbewerkingen weer te geven. Rapporten die in behandeling zijn en die voltooid zijn, zijn maximaal zeven dagen toegankelijk.
