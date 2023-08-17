---
title: Raw-gegevens exporteren
description: Leer records uit uw [!DNL Commerce Intelligence] Data Warehouse om nader te bekijken wat uw dashboard aandrijft.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Raw-gegevens exporteren

Met onbewerkte gegevensexportbewerkingen kunt u records uit uw Data Warehouse exporteren om beter te zien wat het dashboard van stroom voorziet. Ook onbewerkte gegevensexport kan u helpen [discrepanties tussen puntgegevens](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

De uitvoer van ruwe gegevens verleent toegang tot extra kolommen en dimensies die door de-normalisatie en pre-samenvoeging van relevante metriek worden geproduceerd. Bijvoorbeeld: `User's first order date` is een dimensie die u voor elke gebruiker binnen kunt uitvoeren [!DNL Commerce Intelligence], terwijl deze mogelijk niet beschikbaar is in uw database.

Deze zelfstudie behandelt het volgende:

* [Te exporteren gegevens selecteren](#select)
* [De exportbewerking downloaden (](#download)
* [Toegang tot historische exportbewerkingen](#historical)

## Stap 1: Te exporteren gegevens selecteren {#select}

Er zijn twee manieren waarop u onbewerkte gegevens kunt exporteren in [!DNL Commerce Intelligence]:

1. op diagramniveau
1. op tabelniveau

### Exporteren op tabelniveau in uw [!UICONTROL Manage Data] Tab

Als u de tabel wilt exporteren [!UICONTROL Manage Data] tabblad, hebt u [Beheerder](../administrator/user-management/user-management.md) machtigingen.

1. Klikken **[!UICONTROL Manage Data** > ** Gegevens exporteren **> **Raw-gegevens exporteren]**.
1. U ziet een `Export List` van recent gecreëerde uitvoer van gegevens, indien van toepassing. Klikken **[!UICONTROL Add Export]** om een exportbewerking te maken.
1. De `New Raw Data Export` wordt weergegeven. Hier kunt u het exporteren aanpassen door kolommen en filters te selecteren of te deselecteren:

   * `Table` - de `Table` wordt de tabel geselecteerd waaruit gegevens worden geëxporteerd. Standaard wordt hiermee de tabel weergegeven waarin u hebt genavigeerd.
   * `Export Name` - Voer in dit veld de naam van de exportbewerking in. Bijvoorbeeld: `Philadelphia - Daily Revenue`.
   * `Available Columns` - In dit veld worden de kolommen (afmetingen) in de database weergegeven die u kunt opnemen in de exportbewerking. Klik op de naam van een kolom om deze toe te voegen.
   * `Selected Columns` - In dit veld worden de kolommen (afmetingen) weergegeven die momenteel zijn opgenomen in de exportbewerking. Klik op de naam van een kolom om deze te verwijderen.
   * `Filter` - In deze sectie worden de filters weergegeven die momenteel op het exporteren worden toegepast. Deze filters kunnen worden gewijzigd; de nieuwe filters kunnen ook worden toegevoegd om een bepaalde dataset uit te voeren.
   * Klik op **[!UICONTROL Export Data]**.

### Exporteren op grafiekniveau vanaf het dashboard

1. Klik op het tandwielpictogram in de rechterbovenhoek van een diagram.

1. Selecteren `Raw Export` van de vervolgkeuzelijst om de `Raw Export` in.

1. U kunt de exportbewerking aanpassen door de opdracht `table`, `columns`, en `filters` op te nemen of uit te sluiten. Raadpleeg de vorige sectie voor meer informatie over de velden in deze module.

   >[!NOTE]
   >
   >De tabel die wordt weergegeven in het dialoogvenster `Table` field is, door gebrek, de lijst die de grafiek aandrijft.

1. Klik op **[!UICONTROL Export Data]**.

Bekijk het volledige proces op het grafiekniveau.

![](../assets/Chart-level_export.gif)

## Stap 2: De export downloaden {#download}

Het exporteren wordt direct verwerkt nadat u de selecties in het dialoogvenster `Raw Data Export` in. Omdat sommige exporten groot kunnen zijn, zijn ze beperkt tot 10 miljoen rijen en kunnen ze enige tijd in beslag nemen.

Als u wilt controleren of uw export gereed is, klikt u op **[!UICONTROL Raw Data Exports]** rechtsboven in het scherm. Klikken **[!UICONTROL Download]** om een gecomprimeerd bestand te downloaden `.csv` bestand van uw exportbewerking.

![](../assets/Downloading_export.gif)

## Stap 3: Toegang tot Historische uitvoer {#historical}

Klik op **[!UICONTROL Raw Data Export]** rechtsboven in het scherm. Rapporten die in behandeling zijn en die voltooid zijn, zijn maximaal zeven dagen toegankelijk.
