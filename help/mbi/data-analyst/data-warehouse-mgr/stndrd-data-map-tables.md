---
title: Gegevens standaardiseren met toewijzingstabellen
description: Leer hoe u met toewijzingstabellen werkt.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Gegevens standaardiseren met toewijzingstabellen

Beeld dit: u bent in `Report Builder`, een `Revenue by State` verslag. Je bent in de zone. Alles gaat zwemmen totdat je een `billing state` groeperen zich aan uw rapport en u ziet dit:

![](../../assets/Messy_State_Segments.png)

## Hoe kan dit gebeuren?

Helaas kan een gebrek aan standaardisering soms leiden tot rommelige gegevens en problemen bij het opstellen van rapporten. In ons voorbeeld is er mogelijk geen vervolgkeuzemenu of standaardmanier voor onze klanten geweest om hun factuurstatusgegevens in te voeren. Dit leidt tot verschillende waarden - `pa`, `PA`, `penna`, `pennsylvania`, en `Pennsylvania` - allemaal voor dezelfde staat, wat ongetwijfeld tot merkwaardige resultaten zal leiden in de `Report Builder`.

Het is mogelijk dat er een technische bron is die u kan helpen de gegevens op te schonen of de kolommen in te voegen die u rechtstreeks in uw database nodig hebt, maar als dat niet het geval is, hebben we een andere oplossing: **de toewijzingstabel**. Met een toewijzingstabel kunt u snel en eenvoudig alle rommelige gegevens opschonen en standaardiseren door gegevens toe te wijzen aan één uitvoer.

>[!NOTE]
>
>U kunt geen toewijzingstabel voor geconsolideerde lijsten zonder hulp van ons team van de Steun tot stand brengen. Lees ons voor meer informatie.

## Hoe maak ik het? {#how}

**Hernieuwde gegevensopmaak:**

* Zorg ervoor dat het werkblad een koptekstrij heeft.
* Gebruik geen komma&#39;s! Dit veroorzaakt problemen wanneer u het bestand uploadt.
* De standaarddatumnotatie gebruiken `(YYYY-MM-DD HH:MM:SS)` voor datums.
* Percentages moeten als decimalen worden ingevoerd.
* Zorg ervoor dat alle voorloopnullen of volgnullen goed blijven staan.

Voordat u gaat duiken, raden we u aan [de onbewerkte tabelgegevens exporteren](../../tutorials/export-raw-data.md). Als u eerst de onbewerkte gegevens bekijkt, kunt u alle mogelijke combinaties voor de gegevens onderzoeken die u moet opschonen, zodat alle gegevens in de toewijzingstabel worden opgenomen.

Om een toewijzingstabel te maken, moet u een twee kolomspreadsheet tot stand brengen die na [opmaakregels voor het uploaden van bestanden](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Voer in de eerste kolom de waarden in die in de database zijn opgeslagen met **slechts één waarde per rij**. Bijvoorbeeld: `pa` en `PA` kan zich niet op dezelfde regel bevinden - elke invoer moet een eigen rij hebben. Zie hieronder voor een voorbeeld.

Voer in de tweede kolom in wat deze waarden zijn **moeten**. Als we willen doorgaan met ons voorbeeld van de factureringsstatus `pa`, `PA`, `Pennsylvania`, en `pennsylvania` eenvoudig `PA`, we gaan `PA` in deze kolom voor elke invoerwaarde.

![](../../assets/Mapping_table_examples.jpg)

## Wat moet ik doen in [!DNL MBI] om het te gebruiken? {#use}

Nadat u de toewijzingstabel hebt gemaakt, moet u [uploadt het bestand](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) in [!DNL MBI] en [een bij elkaar gevoegde kolom maken](../../data-analyst/data-warehouse-mgr/calc-column-types.md) Hiermee verplaatst u het nieuwe veld naar de gewenste tabel. U kunt dit doen nadat het dossier aan uw gegevenspakhuis wordt gesynchroniseerd.

In ons voorbeeld, zullen wij de kolom bewegen wij op `mapping_state` tabel (`state_input`) aan de `customer_address` tabel met een aangesloten kolom. Op die manier kunnen we ons schande maken `state_input` kolom in onze rapporten in plaats van `state` kolom.

Als u de opdracht `joined` navigeer naar de tabel waarnaar het veld wordt verplaatst in Beheer Data Warehouse. In ons voorbeeld zou dit `customer_address` tabel.

1. Klikken **[!UICONTROL Create a Column]**.
1. Selecteren `Joined Column` van de `Definition` vervolgkeuzelijst.
1. Geef de kolom een naam die het van het `state` in uw database. We gaan verder `billing state (mapped)` zodat kunnen wij zien welke kolom aan gebruik wanneer het segmenteren in de rapportbouwer.
1. Het pad dat we nodig hebben om de tabellen met elkaar te verbinden, bestaat niet, dus moeten we een nieuw pad maken. Klikken **[!UICONTROL Create new path]**  in de `Select a table and column` vervolgkeuzelijst.

   Als u niet zeker bent wat de lijstverhouding is of hoe te om de primaire en buitenlandse sleutels behoorlijk te bepalen, controleer [onze zelfstudie](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) voor wat hulp.

   * Op de `Many` Selecteer de tabel waarnaar u het veld verplaatst (voor ons is dit `customer_address`) en de `Foreign Key` kolom, of `state` in ons voorbeeld.
   * Op de `One` zijde, selecteer `mapping` en de `Primary key` kolom. In dit geval selecteren wij de `state_input` uit de `mapping_state` tabel.
   * Hier is een blik op hoe ons pad eruit ziet:

      ![](../../assets/State_Mapping_Path.png)

1. Klik op **[!UICONTROL Save]** om het pad te maken.
1. Het pad wordt mogelijk niet direct na het opslaan gevuld. Als dit gebeurt, klikt u op de knop `Path` en selecteer het pad dat u zojuist hebt gemaakt.
1. Klikken **[!UICONTROL Save]** om de kolom te maken.

Dat is het!

## Wat doe ik nu? {#wrapup}

Nadat een updatecyclus voltooit, zult u uw nieuwe aangesloten kolom kunnen gebruiken om uw gegevens behoorlijk te segmenteren in plaats van de berichtkolom van uw gegevensbestand. Kijk nu eens naar onze groepsopties - geen stress-chaos meer:

![](../../assets/Clean_State_Segments.png)

De lijsten van de afbeelding zijn handig voor om het even welke tijd u sommige potentieel rommelige gegevens in uw gegevenspakhuis wilt opschonen. Toewijzingstabellen kunnen echter ook worden gebruikt voor andere gebruiksproblemen, zoals [het repliceren van uw Google Analytics kanalen in MBI](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Verwante

* [Tabelrelaties begrijpen en evalueren](../data-warehouse-mgr/table-relationships.md)
* [Paden voor berekende kolommen maken/verwijderen](../data-warehouse-mgr/create-paths-calc-columns.md)
