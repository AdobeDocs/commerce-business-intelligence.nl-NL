---
title: Gegevens standaardiseren met toewijzingstabellen
description: Leer hoe u met toewijzingstabellen werkt.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Gegevens standaardiseren met toewijzingstabellen

Stel dat u een `Revenue by State` -rapport maakt in `Report Builder` . Alles gaat goed totdat u een `billing state` -groep aan uw rapport probeert toe te voegen en u dit ziet:

![](../../assets/Messy_State_Segments.png)

## Hoe kan dit gebeuren?

Helaas kan een gebrek aan standaardisering soms leiden tot rommelige gegevens en problemen bij het opstellen van rapporten. In dit voorbeeld is er mogelijk geen vervolgkeuzemenu of standaardmanier voor uw klanten geweest om hun factuurstatusinformatie in te voeren. Dit leidt tot verschillende waarden - `pa`, `PA`, `penna`, `pennsylvania` en `Pennsylvania` - allemaal voor dezelfde status, wat tot vreemde resultaten in `Report Builder` leidt.

Het is mogelijk dat er een technische bron is die u kan helpen de gegevens op te schonen of de kolommen in te voegen die u rechtstreeks in uw database nodig hebt. Als niet, is er een andere oplossing - **de mappinglijst**. Met een toewijzingstabel kunt u snel en eenvoudig alle rommelige gegevens opschonen en standaardiseren door gegevens toe te wijzen aan één uitvoer.

>[!NOTE]
>
>U kunt geen toewijzingstabel voor geconsolideerde lijsten zonder hulp van het team van de Steun van de Adobe tot stand brengen.

## Hoe maak ik het? {#how}

**het formatteren van gegevens verfrist zich:**

* Zorg ervoor dat uw spreadsheet een koptekstrij heeft.
* Gebruik geen komma&#39;s! Het veroorzaakt problemen wanneer u het dossier uploadt.
* Gebruik de standaarddatumnotatie `(YYYY-MM-DD HH:MM:SS)` voor datums.
* Percentages moeten als decimalen worden ingevoerd.
* Zorg ervoor dat alle voorloopnullen of volgnullen goed blijven staan.

Alvorens u binnen duikt, adviseert de Adobe dat u [ de ruwe lijstgegevens ](../../tutorials/export-raw-data.md) uitvoert. Als u eerst de onbewerkte gegevens bekijkt, kunt u alle mogelijke combinaties voor de gegevens onderzoeken die u moet opschonen, zodat alle gegevens in de toewijzingstabel worden opgenomen.

Om een mappinglijst te maken, moet u een twee-kolom spreadsheet tot stand brengen die de [ het formatteren regels voor dossier ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) volgt uploadt.

In de eerste kolom, ga de waarden in die in uw gegevensbestand met **worden opgeslagen slechts één waarde in elke rij**. `pa` en `PA` kunnen bijvoorbeeld niet op dezelfde regel staan. Elke invoer moet een eigen rij hebben. Zie hieronder voor een voorbeeld.

In de tweede kolom, ga in wat deze waarden **** zouden moeten zijn. Als u doorgaat met het voorbeeld met de factureringsstatus en `pa` , `PA` , `Pennsylvania` en `pennsylvania` eenvoudig `PA` wilt zijn, voert u `PA` in deze kolom in voor elke invoerwaarde.

![](../../assets/Mapping_table_examples.jpg)

## Wat moet ik doen in [!DNL Commerce Intelligence] om het te gebruiken? {#use}

Nadat u klaar bent met het creëren van de mappinglijst, moet u [ het dossier ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) in [!DNL Commerce Intelligence] uploaden en [ tot een aangesloten kolom ](../../data-analyst/data-warehouse-mgr/calc-column-types.md) leiden die het nieuwe gebied in de gewenste lijst opnieuw vestigt. U kunt dit doen nadat het bestand is gesynchroniseerd met uw Data Warehouse.

In dit voorbeeld wordt de kolom die u in de tabel `mapping_state` ( `state_input` ) hebt gemaakt, met een aangesloten kolom naar de tabel `customer_address` verplaatst. Op deze manier kunnen we groeperen op de lege kolom `state_input` in uw rapporten in plaats van op de kolom `state` .

Als u de kolom `joined` wilt maken, navigeert u naar de tabel waarnaar het veld wordt verplaatst in Beheer Data Warehouse. In dit voorbeeld zou dit de `customer_address` tabel zijn.

1. Klik op **[!UICONTROL Create a Column]**.
1. Selecteer `Joined Column` in de vervolgkeuzelijst `Definition` .
1. Geef de kolom een naam die deze onderscheidt van de kolom `state` in de database. Geef de kolom een naam `billing state (mapped)` zodat u kunt zien welke kolom moet worden gebruikt wanneer u segmenteert in de rapportbuilder.
1. Het pad dat u nodig hebt om de tabellen met elkaar te verbinden, bestaat niet. U moet dus een pad maken. Klik op **[!UICONTROL Create new path]** in de vervolgkeuzelijst `Select a table and column` .

   Als u niet zeker bent wat de lijstverhouding is of hoe te om de primaire en buitenlandse sleutels behoorlijk te bepalen, controleer [ het leerprogramma ](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) voor wat hulp.

   * Selecteer aan de zijde van `Many` de tabel waarnaar u het veld verplaatst (voor ons is dit `customer_address` ) en de kolom `Foreign Key` of `state` in het voorbeeld.
   * Selecteer aan de zijde van `One` de kolommen `mapping` table en `Primary key` . In dat geval selecteert u de kolom `state_input` in de tabel `mapping_state` .
   * Hier is een blik op wat de weg als kijkt:

     ![](../../assets/State_Mapping_Path.png)

1. Als u klaar bent, klikt u op **[!UICONTROL Save]** om het pad te maken.
1. Het pad wordt mogelijk niet direct na het opslaan gevuld. Als dit gebeurt, klikt u op het vak `Path` en selecteert u het pad dat u hebt gemaakt.
1. Klik op **[!UICONTROL Save]** om de kolom te maken.

## Wat doe ik nu? {#wrapup}

Nadat een updatecyclus voltooit, zult u uw nieuwe aangesloten kolom kunnen gebruiken om uw gegevens behoorlijk te segmenteren in plaats van de berichtkolom van uw gegevensbestand. Kijk nu naar de groeperingsopties - geen stress meer:

![](../../assets/Clean_State_Segments.png)

Tabellen toewijzen is handig voor elk moment waarop u mogelijk onjuiste gegevens in uw Data Warehouse wilt opruimen. Nochtans, kunnen de afbeeldingslijsten ook voor sommige andere koele gebruiksgevallen worden gebruikt, als [ het herhalen van uw  [!DNL Google Analytics channels]  in  [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Verwante

* [Tabelrelaties begrijpen en evalueren](../data-warehouse-mgr/table-relationships.md)
* [Paden voor berekende kolommen maken/verwijderen](../data-warehouse-mgr/create-paths-calc-columns.md)
