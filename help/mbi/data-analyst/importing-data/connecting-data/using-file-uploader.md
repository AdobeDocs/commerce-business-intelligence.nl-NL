---
title: Bestandsuploader gebruiken
description: Leer hoe te om al uw gegevens in één enkel gegevenspakhuis te zetten.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# Bestandsuploader gebruiken

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

[!DNL MBI] is krachtig niet alleen wegens zijn visualisatiefuncties, maar omdat het u de capaciteit geeft om al uw gegevens in één enkel gegevenspakhuis te zetten. Zelfs de gegevens die buiten uw gegevensbestanden en de integratie leven kunnen in worden gebracht [!DNL MBI] met het gereedschap Bestand uploaden in Data Warehouse Manager.

Laten we advertentiecampagnes als voorbeeld gebruiken. Als u zowel online als offline campagnes voert, kunt u niet het volledige beeld krijgen als u slechts gegevens van een online integratie analyseert. Door een spreadsheet te uploaden met de offlinecampagne kunt u beide sets gegevens analyseren en een beter inzicht krijgen in de prestaties van uw campagne.

## Beperkingen en eisen {#require}

1. **De enige ondersteunde indeling voor het uploaden van bestanden is `CSV` of`comma separated values`**. Als u in Excel werkt, kunt u de functie Opslaan als gebruiken om het bestand op te slaan in `.csv` gebruiken.
1. **`CSV`bestanden moeten`UTF-8 encoding`**. Het grootste deel van de tijd zal dit geen kwestie zijn. Als deze fout optreedt tijdens het uploaden van een bestand, [raadpleeg dit ondersteuningsartikel](https://support.magento.com/hc/en-us/articles/360016730591).
1. **Bestanden mogen niet groter zijn dan 100 MB**. Als het bestand groter is dan dit, scheidt u de tabel in delen en slaat u deze op als afzonderlijke bestanden. U kunt de gegevens toevoegen nadat het eerste bestand is geladen.
1. **Alle tabellen moeten een`primary key`**. Er moet minstens één kolom in uw lijst zijn die als `primary key`of een unieke id voor elke rij in de tabel. Elke kolom die als een `primary key` kan *nooit* is null. A `primary key` kan eenvoudig zijn zoals het toevoegen van een kolom die een aantal aan elke rij geeft, of kan twee kolommen zijn samengevoegd om een kolom van unieke waarden (bijvoorbeeld, `campaign name` en `date`).

   Als een kolom (of kolommen) als uniek zijn aangeduid maar er duplicaten zijn, worden de dubbele rijen niet geïmporteerd.

## Gegevens opmaken voor uploaden {#formatting}

Voordat u uw gegevens kunt uploaden naar [!DNL MBI], controleert u of de notatie is gebaseerd op de richtlijnen in deze sectie.

### Koptekstrij {#header}

Om ervoor te zorgen dat de kolommen worden geëtiketteerd en behoorlijk ingevoerd, zorg ervoor de eerste rij van uw spreadsheet een kopbal is die de gegevens in elke kolom beschrijft.

Kolomnamen moeten uniek zijn en alleen letters, cijfers, spaties en deze symbolen bevatten: `$ % # /`. Als een kolomnaam een komma bevat, wordt deze bij het uploaden van het bestand in twee kolommen gesplitst. Bovendien raden we aan dat het bestand minder dan 85 kolommen bevat om de updatesnelheid te optimaliseren.

### Gegevens met komma&#39;s {#commas}

Omdat bestanden moeten zijn `CSV` kan het gebruik van komma&#39;s problemen veroorzaken bij het uploaden van gegevens. `CSV` bestanden gebruiken komma&#39;s om nieuwe waarden aan te geven, dus een kolom met een naam zoals `Campaigns`, `August` wordt gelezen als twee kolommen (`Campaigns` en `August`) in plaats van één, alle gegevens over één rij verplaatsen. We raden u aan om waar mogelijk komma&#39;s te vermijden. U kunt `Data Preview` om te controleren of uw gegevens correct worden weergegeven wanneer een update is voltooid.

### Datums

Voor elke gegevensset met datums moet de optie [standaarddatumnotatie](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` of `MM/DD/YYYY`.

### Speciale tekens

Bepaalde speciale tekens worden niet geaccepteerd. Bijvoorbeeld het pijlsymbool `& # 1 2 4` wordt geïnterpreteerd als het maken van een nieuwe kolom en veroorzaken fouten bij het uploaden van een bestand.

### Decimale getallen

Valuta-waarden moeten het gegevenstype hebben `Decimal Number` geselecteerd, en deze kolommen zullen automatisch aan twee decimale plaatsen in uw gegevenspakhuis worden rond. Als u uw decimale getallen niet wilt afronden of als u een grotere precisie wilt hebben dan dit, selecteert u de optie `Non-Currency Decimal Number` datatype.

### Percentage

Percentages moeten als decimalen worden ingevoerd. Bijvoorbeeld:

| **Rechts:** | **Onjuist:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style=&quot;table-layout:auto&quot;}

### Waarden met voorloopnullen en/of volgnullen {#zeroes}

Sommige waarden in het bestand (zoals ZIP-codes en id&#39;s) kunnen met nullen beginnen of eindigen. Om ervoor te zorgen dat de nullen op de juiste wijze worden bewaard en geüpload, kunt u het opmaaktype wijzigen (bijvoorbeeld [van getal naar tekst](https://support.office.com/en-US/article/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4)) of nummeropmaak afdwingen.

Laten we gebruiken `US ZIP codes` als voorbeeld van het wijzigen van de getalnotatie. In [!DNL Excel], markeert u de kolom die de `ZIP codes` en [de getalnotatie wijzigen](https://support.office.com/en-za/article/Display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d) tot `ZIP code`. U kunt ook een aangepaste getalnotatie selecteren in het dialoogvenster `Type` venster, Enter `00000`. Houd er rekening mee dat deze methode problemen kan veroorzaken als bepaalde codes zijn opgemaakt als `00000` en andere `00000-0000`.

De `Type` kan [verschillend opgemaakt om andere gegevenstypen aan te passen](https://support.office.com/en-us/article/Keep-leading-zeros-in-number-codes-1bf7b935-36e1-4985-842f-5dfa51f85fe7?CorrelationId=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-US&amp;rs=en-US&amp;ad=US), zoals id&#39;s. Als een `ID` is negen cijfers lang, bijvoorbeeld `Type` kan `000000000` of `000-000-000`. Dit zou veranderen `123456` tot `000-123-456`.

Voor [!DNL Google Docs] en [!DNL Apple Numbers] bronnen, raadpleegt u de [Verwante](#related) onder aan deze pagina.

## Gegevens uploaden {#uploading}

Nu de spreadsheet correct is opgemaakt en [!DNL MBI]- vriendelijk, laten wij het aan uw gegevenspakhuis toevoegen.

1. Ga om aan de slag te gaan naar **[!UICONTROL Data** > **File Uploads]**.

1. Klik op de knop **[!UICONTROL Upload to New Table]** tab.

1. Klikken **[!UICONTROL Choose File]** en selecteert u het bestand. Klikken **[!UICONTROL Open]** om het uploaden te starten.

   Nadat het uploaden is voltooid, wordt een lijst met de kolommen weergegeven [!DNL MBI] gevonden in uw bestand.

1. Controleer of de kolomnamen en gegevenstypen correct zijn. Controleer met name of datumkolommen worden gelezen als datums en niet als getallen.

   >[!NOTE]
   >
   >De `datatype` is uiterst belangrijk, dus vergeet deze stap niet!

1. Selecteer de kolom (of kolommen) waaruit de `primary key` voor de tabel met de selectievakjes onder het sleutelpictogram.

1. Geef de tabel een naam.

1. Klikken **[!UICONTROL Save Table]**.

A *Succes!* verschijnt boven aan het scherm nadat de tabel is opgeslagen.

Als u een visueel hulpmiddel nodig hebt, is hier een blik op het volledige proces:

![](../../../assets/fileupload.gif)

Geüploade tabellen worden weergegeven onder de **Bestand uploaden** sectie van de lijstlijst (in zowel de Alle Lijsten als de Gesynchroniseerde opties van Lijsten) in de Manager van de Data Warehouse:

![](../../../assets/upload-tables.png)

## Gegevens bijwerken of toevoegen aan een bestaande tabel {#appending}

Wilt u nieuwe gegevens toevoegen aan een bestand dat u al hebt geüpload? Geen probleem - u kunt gegevens eenvoudig bijwerken en toevoegen in [!DNL MBI].

1. Ga om aan de slag te gaan naar **[!UICONTROL Manage Data** > **File Uploads]**.

1. Klik op de knop **[!UICONTROL Edit/Upload `.csv`Naar bestaande tabellen]** tab.

1. Klik in het vervolgkeuzemenu op de naam van de tabel die u wilt bijwerken of toevoegen.

1. Gebruik het vervolgkeuzemenu om de optie voor de afhandeling van dubbele rijen te selecteren:

   |  |  |
   |---|---|
   | `Overwrite old row with new row` | Hierdoor worden bestaande gegevens overschreven door nieuwe gegevens als een rij dezelfde primaire sleutel heeft in zowel de bestaande tabel als het nieuwe bestand. Dit is de methode die moet worden gebruikt voor kolommen met waarden die in de loop der tijd veranderen, bijvoorbeeld een kolom Status. Bestaande gegevens worden overschreven en bijgewerkt met de nieuwe gegevens. Rijen met primaire sleutels die niet in de bestaande lijst zijn zullen als nieuwe rijen worden toegevoegd. |
   | `Retain old row; discard new row` | Hierdoor worden nieuwe gegevens genegeerd als een rij dezelfde primaire sleutel heeft in zowel de bestaande tabel als het nieuwe bestand. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Hiermee worden alle bestaande gegevens verwijderd en vervangen door de nieuwe gegevens uit het bestand. Gebruik deze optie alleen als u geen gegevens in de bestaande tabel nodig hebt. |

1. Klikken **[!UICONTROL Choose File]** en selecteert u het bestand.

1. Klikken **[!UICONTROL Open]** om het uploaden te starten.

   Nadat het uploaden is voltooid, [!DNL MBI] zal de gegevensstructuur in het bestand valideren. A *Succes!* verschijnt boven aan het scherm nadat de tabel is opgeslagen.

## Beschikbaarheid van gegevens {#availability}

Net als berekende kolommen, zijn de gegevens van dossier uploadt beschikbaar nadat de volgende updatecyclus voltooit. Als er een update wordt uitgevoerd tijdens het uploaden van het bestand, zijn de gegevens pas beschikbaar na de volgende update. Nadat een updatecyclus is voltooid, kunt u naar de `Data Preview` in uw gegevenspakhuis om ervoor te zorgen dat het dossier correct wordt geupload en de gegevens zoals verwacht tonen.

## Omloop {#wrapup}

In dit artikel worden alleen de basisbeginselen voor het importeren van gegevens besproken, maar we hopen dat u iets geavanceerder wilt doen. Lees de verwante artikelen voor hulp bij het formatteren en invoeren van financiële, eCommerce, en uitgaven, en andere soorten gegevens.

Bovendien is het uploaden van bestanden niet de enige manier om uw gegevens in te voeren [!DNL MBI]. De [API voor gegevensimport](https://developer.adobe.com/commerce/services/reporting/import-api/) Met functies kunt u willekeurige gegevens in uw [!DNL MBI] data-entrepot.

## Verwante {#related}

* [Financiële gegevens opmaken en importeren](../../../best-practices/format-import-financial-data.md)
* [Offline/andere gegevens importeren en gegevens besteden](../connecting-data/import-offline-ad-data.md)
* [Verwacht[!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)

## Bronnen van derden

* [Handleiding voor gegevensopmaak voor nummers](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Handleiding voor gegevensopmaak](https://support.google.com/docs/answer/56470?hl=en)
