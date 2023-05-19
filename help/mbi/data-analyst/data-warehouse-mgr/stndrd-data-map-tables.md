---
title: Gegevens standaardiseren met toewijzingstabellen
description: Leer hoe u met toewijzingstabellen werkt.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Gegevens standaardiseren met toewijzingstabellen

Stel je voor dat je in de `Report Builder` een gebouw `Revenue by State` verslag. Alles gaat goed totdat u een `billing state` groeperen zich aan uw rapport en u ziet dit:

![](../../assets/Messy_State_Segments.png)

## Hoe kan dit gebeuren?

Helaas kan een gebrek aan standaardisering soms leiden tot rommelige gegevens en problemen bij het opstellen van rapporten. In dit voorbeeld is er mogelijk geen vervolgkeuzemenu of standaardmanier voor uw klanten geweest om hun factuurstatusinformatie in te voeren. Dit leidt tot verschillende waarden - `pa`, `PA`, `penna`, `pennsylvania`, en `Pennsylvania` - voor dezelfde staat, wat tot merkwaardige resultaten leidt in de `Report Builder`.

Het is mogelijk dat er een technische bron is die u kan helpen de gegevens op te schonen of de kolommen in te voegen die u rechtstreeks in uw database nodig hebt. Zo niet, dan is er een andere oplossing - **de toewijzingstabel**. Met een toewijzingstabel kunt u snel en eenvoudig alle rommelige gegevens opschonen en standaardiseren door gegevens toe te wijzen aan één uitvoer.

>[!NOTE]
>
>U kunt geen toewijzingstabel voor geconsolideerde lijsten zonder hulp van het team van de Steun van de Adobe tot stand brengen.

## Hoe maak ik het? {#how}

**Hernieuwde gegevensopmaak:**

* Zorg ervoor dat uw spreadsheet een koptekstrij heeft.
* Gebruik geen komma&#39;s! Het veroorzaakt problemen wanneer u het dossier uploadt.
* De standaarddatumnotatie gebruiken `(YYYY-MM-DD HH:MM:SS)` voor datums.
* Percentages moeten als decimalen worden ingevoerd.
* Zorg ervoor dat alle voorloopnullen of volgnullen goed blijven staan.

Voordat u gaat duiken, raadt Adobe u aan [de onbewerkte tabelgegevens exporteren](../../tutorials/export-raw-data.md). Als u eerst de onbewerkte gegevens bekijkt, kunt u alle mogelijke combinaties voor de gegevens onderzoeken die u moet opschonen, zodat alle gegevens in de toewijzingstabel worden opgenomen.

Als u een toewijzingstabel wilt maken, moet u een spreadsheet met twee kolommen maken die volgt op de [opmaakregels voor het uploaden van bestanden](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Voer in de eerste kolom de waarden in die in de database zijn opgeslagen met **slechts één waarde per rij**. Bijvoorbeeld: `pa` en `PA` kan zich niet op dezelfde regel bevinden - elke invoer moet een eigen rij hebben. Zie hieronder voor een voorbeeld.

Voer in de tweede kolom in wat deze waarden zijn **moeten**. Als u wilt doorgaan met het voorbeeld met de factureringsstatus `pa`, `PA`, `Pennsylvania`, en `pennsylvania` eenvoudig `PA`, voert u in `PA` in deze kolom voor elke invoerwaarde.

![](../../assets/Mapping_table_examples.jpg)

## Wat moet ik doen in [!DNL Commerce Intelligence] om het te gebruiken? {#use}

Nadat u de toewijzingstabel hebt gemaakt, moet u [uploadt het bestand](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) in [!DNL Commerce Intelligence] en [een bij elkaar gevoegde kolom maken](../../data-analyst/data-warehouse-mgr/calc-column-types.md) Hiermee verplaatst u het nieuwe veld naar de gewenste tabel. U kunt dit doen nadat het bestand is gesynchroniseerd met uw Data Warehouse.

In dit voorbeeld wordt de kolom verplaatst die u in het dialoogvenster `mapping_state` tabel (`state_input`) aan de `customer_address` tabel met een aangesloten kolom. Hierdoor kunnen we ons scharen achter de schone `state_input` in uw rapporten in plaats van de `state` kolom.

Als u de opdracht `joined` navigeer naar de tabel waarnaar het veld wordt verplaatst in Beheer Data Warehouse. In dit voorbeeld is dit `customer_address` tabel.

1. Klikken **[!UICONTROL Create a Column]**.
1. Selecteren `Joined Column` van de `Definition` vervolgkeuzelijst.
1. Geef de kolom een naam die het van het `state` in uw database. De kolom een naam geven `billing state (mapped)` zodat kunt u zien welke kolom aan gebruik wanneer het segmenteren in de rapportbouwer.
1. Het pad dat u nodig hebt om de tabellen met elkaar te verbinden, bestaat niet. U moet dus een pad maken. Klikken **[!UICONTROL Create new path]**  in de `Select a table and column` vervolgkeuzelijst.

   Als u niet zeker bent wat de lijstverhouding is of hoe te om de primaire en buitenlandse sleutels behoorlijk te bepalen, controleer [de zelfstudie](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) voor wat hulp.

   * Op de `Many` Selecteer de tabel waarnaar u het veld verplaatst (voor ons is dit `customer_address`) en de `Foreign Key` kolom, of `state` in het voorbeeld.
   * Op de `One` zijde, selecteer `mapping` en de `Primary key` kolom. In dit geval selecteert u de optie `state_input` uit de `mapping_state` tabel.
   * Hier is een blik op wat de weg als kijkt:

      ![](../../assets/State_Mapping_Path.png)

1. Klik op **[!UICONTROL Save]** om het pad te maken.
1. Het pad wordt mogelijk niet direct na het opslaan gevuld. Als dit gebeurt, klikt u op de knop `Path` en selecteer het pad dat u hebt gemaakt.
1. Klikken **[!UICONTROL Save]** om de kolom te maken.

## Wat doe ik nu? {#wrapup}

Nadat een updatecyclus voltooit, zult u uw nieuwe aangesloten kolom kunnen gebruiken om uw gegevens behoorlijk te segmenteren in plaats van de berichtkolom van uw gegevensbestand. Kijk nu naar de groeperingsopties - geen stress meer:

![](../../assets/Clean_State_Segments.png)

Tabellen toewijzen is handig voor elk moment waarop u mogelijk onjuiste gegevens in uw Data Warehouse wilt opruimen. Toewijzingstabellen kunnen echter ook worden gebruikt voor andere gebruiksproblemen, zoals [repliceren, [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Verwante

* [Tabelrelaties begrijpen en evalueren](../data-warehouse-mgr/table-relationships.md)
* [Paden voor berekende kolommen maken/verwijderen](../data-warehouse-mgr/create-paths-calc-columns.md)
