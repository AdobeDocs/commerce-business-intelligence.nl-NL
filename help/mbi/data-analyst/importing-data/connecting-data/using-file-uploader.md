---
title: Bestandsuploader gebruiken
description: Leer hoe u al uw gegevens in één Data Warehouse plaatst.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 736dbdc3ea6bc8b7c852f06110705765f040c31f
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 0%

---

# Bestandsuploader gebruiken

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] is niet alleen krachtig vanwege de visualisatiefuncties, maar ook omdat u hiermee alle gegevens in één Data Warehouse kunt plaatsen. Zelfs gegevens die zich buiten uw databases en integraties bevinden, kunnen in [!DNL Commerce Intelligence] worden overgebracht met het gereedschap Bestand uploaden in Data Warehouse Manager.

Gebruik advertentiecampagnes als voorbeeld. Als u zowel online als offline campagnes voert, kunt u niet het volledige beeld krijgen als u slechts gegevens van een online integratie analyseert. Door een spreadsheet te uploaden met de offlinecampagne kunt u beide sets gegevens analyseren en een beter inzicht krijgen in de prestaties van uw campagne.

## Beperkingen en eisen {#require}

1. **de enige ondersteunde indeling voor het uploaden van bestanden is `CSV` of`comma separated values`** . Als u in Excel werkt, kunt u het bestand opslaan in de `.csv` -indeling met de functie Opslaan als.
1. **`CSV`-bestanden moeten`UTF-8 encoding`** gebruiken. Meestal is dit geen probleem. Als u deze fout terwijl het uploaden van een dossier ontmoet, [ raadpleeg dit artikel van Steun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **de Dossiers kunnen niet groter zijn dan 100MB**. Als het bestand groter is dan dit, scheidt u de tabel in delen en slaat u deze op als afzonderlijke bestanden. U kunt de gegevens toevoegen nadat het eerste bestand is geladen.
1. **Alle lijsten moeten a`primary key`** hebben. Er moet ten minste één kolom in de tabel staan die als `primary key` kan worden gebruikt, of een unieke id voor elke rij in de tabel. Om het even welke kolom die als a `primary key` wordt aangewezen kan *nooit* ongeldig zijn. Een `primary key` kan zo eenvoudig zijn als het toevoegen van een kolom die een getal aan elke rij geeft, of kan twee kolommen zijn die worden samengevoegd om een kolom met unieke waarden te maken (bijvoorbeeld `campaign name` en `date` ).

   Als een kolom (of kolommen) uniek is of zijn, maar er duplicaten zijn, worden de dubbele rijen niet geïmporteerd.

## Gegevens opmaken voor uploaden {#formatting}

Voordat u uw gegevens kunt uploaden naar [!DNL Commerce Intelligence] , moet u controleren of de gegevens zijn opgemaakt volgens de richtlijnen in deze sectie.

### Koptekstrij {#header}

Om ervoor te zorgen dat de kolommen worden geëtiketteerd en behoorlijk ingevoerd, zorg ervoor dat de eerste rij van uw spreadsheet een kopbal is die de gegevens in elke kolom beschrijft.

Kolomnamen moeten uniek zijn en alleen letters, cijfers, spaties en deze symbolen bevatten: `$ % # /` . Als een kolomnaam een komma bevat, wordt deze gesplitst in twee kolommen wanneer het bestand wordt geüpload. Bovendien raadt Adobe aan dat het bestand minder dan 85 kolommen bevat voor een optimale updatesnelheid.

### Gegevens met komma&#39;s {#commas}

Omdat bestanden de `CSV` -indeling moeten hebben, kan het gebruik van komma&#39;s problemen veroorzaken bij het uploaden van gegevens. `CSV` bestanden gebruiken komma&#39;s om nieuwe waarden aan te geven. Daarom wordt een kolom met een naam als `Campaigns` , `August` gelezen als twee kolommen (`Campaigns` en `August`) in plaats van als één, waarbij al uw gegevens over één rij worden verplaatst. Adobe raadt aan waar mogelijk komma&#39;s te vermijden. Met `Data Preview` kunt u controleren of de gegevens correct worden weergegeven wanneer een update is voltooid.

### Datums

Om het even welke dataset die data omvat moet het [ standaarddatumformaat ](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) gebruiken `YYYY-MM-DD HH:MM:SS` of `MM/DD/YYYY`.

### Speciale tekens

Bepaalde speciale tekens worden niet geaccepteerd. Het buissymbool `& # 1 2 4` wordt bijvoorbeeld geïnterpreteerd als het maken van een kolom en veroorzaakt fouten bij het uploaden van een bestand.

### Decimale getallen

Bij valutawaarden moet het gegevenstype `Decimal Number` zijn geselecteerd en deze kolommen worden automatisch afgerond tot twee decimalen in uw Data Warehouse. Als u uw decimale getallen niet wilt afronden of als u een grotere nauwkeurigheid dan dit wilt hebben, moet u het gegevenstype `Non-Currency Decimal Number` selecteren.

### Percentage

Percentages moeten als decimalen worden ingevoerd. Bijvoorbeeld:

| **juist:** | **Verkeerd:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Waarden met voorloopnullen en/of volgnullen {#zeroes}

Sommige waarden in het bestand (zoals ZIP-codes en id&#39;s) kunnen met nullen beginnen of eindigen. Om ervoor te zorgen dat nullen behoorlijk worden behouden en geupload, kunt u het formatteren type (bijvoorbeeld, [ van aantal in tekst ](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&rs=en-us&ad=us)) veranderen of aantal het formatteren afdwingen.

Gebruik `US ZIP codes` als voorbeeld van het wijzigen van getalnotatie. In [!DNL Excel], benadruk de kolom die `ZIP codes` bevat en [ verandert het aantalformaat ](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&rs=en-us&ad=us) in `ZIP code`. U kunt ook een aangepaste getalnotatie selecteren en vervolgens `Type` invoeren in het venster `00000` . Houd er rekening mee dat deze methode problemen kan opleveren als sommige codes zijn opgemaakt als `00000` en andere `00000-0000` zijn.

`Type` kan [ verschillend worden geformatteerd om andere gegevenstypes ](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&ui=en-us&rs=en-us&ad=us), zoals IDs aan te passen. Als een `ID` bijvoorbeeld negen cijfers lang is, kan de `Type` zijn `000000000` of `000-000-000` . Dit zou `123456` in `000-123-456` veranderen.

Voor [!DNL Google Docs] en [!DNL Apple Numbers] middelen, verwijs naar de [ Verwante ](#related) lijst bij de bodem van deze pagina.

## Gegevens uploaden {#uploading}

Nu uw spreadsheet correct is opgemaakt en [!DNL Commerce Intelligence] - vriendelijk, voeg het aan uw Data Warehouse toe.

1. Ga naar **[!UICONTROL Data** > **File Uploads]** om aan de slag te gaan.

1. Klik op de tab **[!UICONTROL Upload to New Table]** .

1. Klik op **[!UICONTROL Choose File]** en selecteer het bestand. Klik op **[!UICONTROL Open]** om het uploaden te starten.

   Nadat het uploaden is voltooid, wordt een lijst weergegeven met de kolommen [!DNL Commerce Intelligence] in het bestand.

1. Controleer of de kolomnamen en gegevenstypen correct zijn. Controleer met name of datumkolommen worden gelezen als datums en niet als getallen.

   >[!NOTE]
   >
   >`datatype` is belangrijk, dus sla deze stap niet over!

1. Selecteer de kolom (of kolommen) die de `primary key` voor de tabel vormen door de selectievakjes onder het sleutelpictogram te gebruiken.

1. Geef de tabel een naam.

1. Klik op **[!UICONTROL Save Table]**.

A *Succes!* wordt boven in het scherm weergegeven nadat de tabel is opgeslagen.

Kijk naar het hele proces als u een visuele oplossing nodig hebt:

![ Geanimeerde demonstratie van dossier uploadt proces dat gegevens toont die worden toegevoegd ](../../../assets/fileupload.gif)

De geüploade lijsten tonen onder **Dossier uploadt** sectie van het lijstoverzicht (in zowel Alle Lijsten als de Gesynchroniseerde opties van Lijsten) in de Manager van Data Warehouse:

![ uploadt de interface van lijsten die beschikbare lijsten voor gegevensinvoer tonen ](../../../assets/upload-tables.png)

## Gegevens bijwerken of toevoegen aan een bestaande tabel {#appending}

Wilt u nieuwe gegevens toevoegen aan een bestand dat u al hebt geüpload? Geen probleem - u kunt gegevens eenvoudig bijwerken en toevoegen in [!DNL Commerce Intelligence] .

1. Ga naar **[!UICONTROL Manage Data** > **File Uploads]** om aan de slag te gaan.

1. Klik **[!UICONTROL Edit/Upload `.csv`aan Bestaande Lijsten]** tabel.

1. Klik in het vervolgkeuzemenu op de naam van de tabel die u wilt bijwerken of toevoegen.

1. Gebruik het vervolgkeuzemenu om de optie voor de afhandeling van dubbele rijen te selecteren:

   | Optie | Beschrijving |
   |---|---|
   | `Overwrite old row with new row` | Hierdoor worden bestaande gegevens overschreven door nieuwe gegevens als een rij dezelfde primaire sleutel heeft in zowel de bestaande tabel als het nieuwe bestand. Dit is de methode die moet worden gebruikt voor kolommen met waarden die in de loop der tijd veranderen, bijvoorbeeld een kolom Status. Bestaande gegevens worden overschreven en bijgewerkt met de nieuwe gegevens. Rijen met primaire toetsen die niet in de bestaande tabel staan, worden als nieuwe rijen toegevoegd. |
   | `Retain old row; discard new row` | Hierdoor worden nieuwe gegevens genegeerd als een rij dezelfde primaire sleutel heeft in zowel de bestaande tabel als het nieuwe bestand. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Hiermee worden bestaande gegevens verwijderd en vervangen door de nieuwe gegevens uit het bestand. Gebruik deze optie alleen als u geen gegevens in de bestaande tabel nodig hebt. |

1. Klik op **[!UICONTROL Choose File]** en selecteer het bestand.

1. Klik op **[!UICONTROL Open]** om het uploaden te starten.

   Nadat het uploaden is voltooid, valideert [!DNL Commerce Intelligence] de gegevensstructuur in het bestand. A *Succes!* wordt boven in het scherm weergegeven nadat de tabel is opgeslagen.

## Beschikbaarheid van gegevens {#availability}

Net als berekende kolommen, zijn de gegevens van dossier uploadt beschikbaar nadat de volgende updatecyclus voltooit. Als er een update wordt uitgevoerd tijdens het uploaden van het bestand, zijn de gegevens pas beschikbaar na de volgende update. Nadat een updatecyclus is voltooid, kunt u naar het tabblad `Data Preview` in uw Data Warehouse navigeren om ervoor te zorgen dat het bestand correct is geüpload en de gegevens naar behoren worden weergegeven.

## Omloop {#wrapup}

Dit onderwerp behandelde slechts de grondbeginselen voor het gebruiken van het invoeren van gegevens, maar u kunt iets geavanceerder willen doen. Lees de verwante artikelen voor hulp bij het formatteren en invoeren van financiële, eCommerce, en uitgaven, en andere soorten gegevens.

Uploaden van bestanden is niet de enige manier om uw gegevens in [!DNL Commerce Intelligence] in te voeren. De [ invoer API van Gegevens ](https://developer.adobe.com/commerce/services/reporting/import-api/) functies staan u toe om willekeurige gegevens in uw [!DNL Commerce Intelligence] Data Warehouse te duwen.

## Verwante {#related}

* [Financiële gegevens opmaken en importeren](../../../best-practices/format-import-financial-data.md)
* [Offline/andere gegevens importeren en gegevens besteden](../connecting-data/import-offline-ad-data.md)
* [[!DNL Google ECommerce] gegevens verwacht](../integrations/google-ecommerce-data.md)

## Bron van derden

* [[!DNL Google Docs]  de Formatterende Gids van Gegevens ](https://support.google.com/docs/answer/56470?hl=en)
