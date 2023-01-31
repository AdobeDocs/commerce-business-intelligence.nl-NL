---
title: Replicatiemethoden configureren
description: Leer hoe de lijsten worden georganiseerd, en hoe het gedrag van de lijstgegevens u zal toestaan om de beste replicatiemethode voor uw lijsten te kiezen.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Replicatiemethoden configureren

`Replication` methoden en [hercontroles](../data-warehouse-mgr/cfg-data-rechecks.md) worden gebruikt om nieuwe of bijgewerkte gegevens in uw gegevensbestandlijsten te identificeren. Een juiste instelling is van cruciaal belang voor zowel de nauwkeurigheid van de gegevens als de geoptimaliseerde updatetijden. In dit artikel richten we ons alleen op replicatiemethoden.

Wanneer de nieuwe lijsten in de Manager van de Data Warehouse worden gesynchroniseerd, zal een replicatiemethode automatisch voor de lijst worden gekozen. Het begrip van de diverse replicatiemethodes, hoe de lijsten worden georganiseerd, en hoe het gedrag van de lijstgegevens u zal toestaan om de beste replicatiemethode voor uw lijsten te kiezen.

## Wat zijn de replicatiemethoden?

`Replication` de methoden vallen onder drie groepen - `Incremental`, `Full Table`, en `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) betekent dat [!DNL MBI] alleen nieuwe of bijgewerkte gegevens repliceren bij elke replicatiepoging. Aangezien deze methodes zeer latentie zullen verminderen, adviseren wij hoogst gebruikend het waar mogelijk.

[**[!UICONTROL Full Table Replication]**](#fulltable) betekent dat [!DNL MBI] zal de volledige inhoud van een lijst op elke replicatiepoging herhalen. Vanwege de mogelijk grote hoeveelheid gegevens die moet worden gerepliceerd, kunnen deze methoden de latentie en updatetijden verhogen. Als een lijst om het even welke timestamped of datetime kolommen bevat, adviseren wij in plaats daarvan gebruikend een Incrementele methode.

**[!UICONTROL Paused]** Hiermee wordt aangegeven dat de replicatie voor de tabel wordt gestopt of gepauzeerd. [!DNL MBI] tijdens een updatecyclus niet op nieuwe of bijgewerkte gegevens zal controleren; dit betekent geen gegevens van een lijst zullen worden herhaald die dit als zijn Methode van de Replicatie heeft.

## Incrementele replicatiemethoden {#incremental}

### Gewijzigd bij (meest ideaal)

De `Modified At` De replicatiemethode gebruikt een datetime kolom - die wordt bevolkt wanneer een rij wordt gecreeerd en dan bijgewerkt wanneer de gegevens veranderen - om gegevens te vinden om te herhalen. Deze methode is ontworpen voor het werken met tabellen die aan de volgende criteria voldoen:

* bevat een `datetime` kolom die aanvankelijk wordt gevuld wanneer een rij wordt gecreeerd en bijgewerkt wanneer de rij wordt gewijzigd;
* de `datetime` de kolom is nooit null;
* rijen worden niet uit de tabel verwijderd

Naast deze criteria bevelen wij ook ten zeerste aan **indexeren** de `datetime` kolom gebruikt voor `Modified At` replicatie, aangezien dit zal helpen replicatiesnelheid optimaliseren.

Wanneer de update wordt uitgevoerd, worden nieuwe of gewijzigde gegevens geïdentificeerd door te zoeken naar rijen met een waarde in het dialoogvenster `datetime` kolom die is opgetreden na de meest recente update. Wanneer nieuwe rijen worden ontdekt, worden zij herhaald aan uw Data Warehouse. Als de Data Warehouse al rijen bevat, worden deze overschreven met de huidige databasewaarden.

Een tabel kan bijvoorbeeld een kolom met de naam `modified\_at` dat aangeeft wanneer de laatste gegevens zijn gewijzigd. Als de meest recente update dinsdag om 12.00 uur heeft plaatsgevonden, wordt in de update naar alle rijen gezocht met een `modified\_at` waarde groter dan dinsdag om 12.00 uur. Alle ontdekte rijen die zijn gemaakt of gewijzigd sinds dinsdag om 12.00 uur, worden gerepliceerd naar de Data Warehouse.

**Wist je dat?**
Zelfs als uw database momenteel geen ondersteuning biedt voor een `Incremental` Replicatiemethode: [Breng enkele wijzigingen aan in uw database](../../best-practices/mod-db-inc-replication.md) dat het gebruik van `Modified At` of `Single Auto Incrementing PK`.

`Modified At` is niet alleen de meest ideale replicatiemethode, maar ook de snelste. Deze methode veroorzaakt niet alleen merkbare snelheidsverhogingen met grote gegevensreeksen, het vereist ook het vormen van geen recheck optie. Andere methoden moeten een hele tabel doorlopen om wijzigingen te identificeren, zelfs als een kleine subset van gegevens is gewijzigd. `Modified At` Hiermee doorloopt u alleen die kleine subset.

### Eén automatische verhogende primaire sleutel

`Auto Incrementing` is een gedrag dat opeenvolgende primaire sleutels aan rijen toewijst. Als een tabel `Auto Incrementing` en de hoogste primaire sleutel in de lijst momenteel 1000 is, dan zal de volgende primaire waarde 1001 of hoger zijn. Een tabel die niet wordt gebruikt `Auto Incrementing` gedrag kan een primaire-sleutelwaarde toewijzen die lager is dan 1000 of naar een veel groter getal springen, maar dit wordt niet vaak gebruikt.

Deze methode is ontworpen voor het repliceren van nieuwe gegevens uit tabellen die aan de volgende criteria voldoen:

* `single-column primary key`; en
* `primary key` datatype is `integer`; en
* `auto incrementing` waarden van primaire sleutels.

Wanneer een tabel wordt gebruikt `Single Auto Incrementing Primary Key` replicatie, worden de nieuwe gegevens ontdekt door naar primaire zeer belangrijke waarden te zoeken die hoger zijn dan de huidige hoogste waarde in uw Data Warehouse. Als de hoogste waarde voor de primaire sleutel in de Data Warehouse bijvoorbeeld 500 is, zoekt de volgende update naar rijen met de primaire sleutel waarden 501 of hoger.

### Datum toevoegen

De `Add Date` methodefuncties die vergelijkbaar zijn met de `Single Auto Incrementing Primary Key` methode. In plaats van een geheel getal voor de primaire sleutel van de tabel te gebruiken, wordt bij deze methode een `timestamped` te controleren op nieuwe rijen.

Wanneer een tabel `Add Date` replicatie, worden de nieuwe gegevens ontdekt door timestamped waarden te zoeken die groter zijn dan de recentste datum die aan uw Data Warehouse wordt gesynchroniseerd. Bijvoorbeeld, als een laatste update op 20/12/2015 09 liep:00:00, worden rijen met een tijdstempel die groter is dan dit, gemarkeerd als nieuwe gegevens en gerepliceerd.

>[!NOTE]
>
>In tegenstelling tot `Modified At` methode, `Add Date` Bestaande rijen worden niet gecontroleerd op bijgewerkte informatie. Er worden alleen nieuwe rijen weergegeven.

## Volledige tabelreplicatiemethoden {#fulltable}

### Volledige tabel

`Full table` de replicatie verfrist de volledige lijst wanneer de nieuwe rijen worden ontdekt. Dit is verreweg de minst efficiënte replicatiemethode, toe te schrijven aan het feit dat alle gegevens tijdens elke update moeten worden opnieuw verwerkt, veronderstellend er nieuwe rijen zijn.

Nieuwe rijen worden ontdekt door uw gegevensbestand bij het begin van het synchronisatieproces te vragen en het aantal rijen te tellen. Als uw lokale database meer rijen bevat dan [!DNL MBI]Dan wordt de tabel vernieuwd. Als het aantal rijen identiek is of als [!DNL MBI] contains *meer* De tabel wordt overgeslagen als de lokale database geen rijen bevat.

Dit brengt het belangrijke punt aan de orde dat **`Full Table`replicatie is niet compatibel wanneer:**

* er tussen volgende updatecycli meer rijen worden verwijderd dan in uw lokale databasetabel zijn gemaakt, of
* kolomwaarden worden gewijzigd, maar er worden geen extra rijen gemaakt

In beide bovengenoemde scenario&#39;s `Full Table` de replicatie zal geen veranderingen ontdekken en uw gegevens zullen verouderd worden. Door de inefficiëntie van deze replicatiemethode en de hierboven vermelde vereisten, `Full Table` replicatie wordt alleen aanbevolen als laatste redmiddel.

### Batch primaire sleutel

Wanneer een tabel `Primary Key Batch` (PK-batch), worden nieuwe gegevens gedetecteerd door rijen binnen bereiken, of batches, van primaire-sleutelwaarden te tellen. Terwijl wij typisch denken dat dit met gehelen wordt gebruikt, zelfs kunnen de tekstwaarden op een manier worden bevolen die het systeem toestaat om constante waaiers te bepalen.

Stel bijvoorbeeld dat een update wordt uitgevoerd en dat een rij wordt geteld voor het bereik van toetsen van 1 tot en met 100. In deze update zoekt en registreert het systeem 37 rijen. In de volgende update wordt opnieuw een rijtelling uitgevoerd voor het bereik 1-100 en worden 41 rijen gevonden. Omdat er een verschil is in het aantal rijen in vergelijking met de laatste update, zal het systeem dat waaier (of partij) meer in detail inspecteren.

Deze methode is bedoeld voor het repliceren van gegevens uit tabellen die aan de volgende criteria voldoen:

* één kolom, niet geheel getal; of
* samengestelde sleutels (meerdere kolommen die de primaire sleutel vormen) - houd er rekening mee dat kolommen die in een samengestelde primaire sleutel worden gebruikt nooit null-waarden kunnen hebben; of
* waarden voor één kolom, gehele getallen, niet automatisch incrementele primaire sleutels.

Deze methode is niet ideaal, omdat het ongelooflijk langzaam is door de hoeveelheid verwerking die moet plaatsvinden om partijen te onderzoeken en veranderingen te vinden. Wij adviseren niet gebruikend deze methode tenzij het niet mogelijk is om de noodzakelijke wijzigingen te maken om de andere replicatiemethodes te steunen. Verwacht dat de updatetijden zullen stijgen als deze methode moet worden gebruikt.

## Replicatiemethoden instellen

De methodes van de replicatie worden geplaatst op een lijst-door-lijst basis. Om een replicatiemethode voor een lijst te plaatsen, hebt u nodig [`Admin`](../../administrator/user-management/user-management.md) machtigingen zodat u toegang hebt tot Data Warehouse Manager.

1. Eenmaal in Beheer Data Warehouse selecteert u de tabel in het menu `Synced Tables` om het schema van de tabel weer te geven.
1. De huidige replicatiemethode wordt vermeld onder de lijstnaam. Klik op de koppeling om deze te wijzigen.
1. Klik in het pop-upvenster dat wordt weergegeven op het keuzerondje naast een van de twee `Incremental` of `Full Table` replicatie om een replicatietype te selecteren.
1. Klik op de knop **[!UICONTROL Replication Method]** vervolgkeuzelijst om een methode te selecteren, bijvoorbeeld `Paused` of `Modified At`.

   >[!NOTE]
   >
   >**Voor sommige incrementele methoden moet u een`Replication Key`**. [!DNL MBI] zal deze sleutel gebruiken om te bepalen waar de volgende updatecyclus zou moeten beginnen.
   >
   >Als u bijvoorbeeld de opdracht `modified at` methode voor onze `orders` aan tafel, moeten we een `date column` als replicatietoets. Er kunnen verschillende opties voor replicatietoetsen bestaan, maar we selecteren `created at`of de tijd waarop de bestelling is gemaakt. Als de laatste updatecyclus op 12-1-2015 00 is gestopt:10:00, de volgende cyclus zou beginnen gegevens te repliceren met een `created at` datum groter dan deze.

1. Klik op **[!UICONTROL Save]**.

Bekijk het hele proces:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Omloop

Om klaar te zijn, hebben wij deze lijst samengebracht die de diverse replicatiemethodes vergelijkt. Wij vinden het ongelooflijk handig wanneer het selecteren van een methode voor de lijsten in ons gegevenspakhuis.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Sneller | Langzaam | Nee | Nee | Nee | Ja |
| `Primary Key Batch Monitoring` | Langzaam | Langzaam | Ja | Ja | Ja | Ja |
| `Modified At` | Sneller | Sneller | Ja | Ja | Ja | Nee |

{style=&quot;table-layout:auto&quot;}

## Gerelateerde documentatie

* [Gegevens opnieuw controleren](../data-warehouse-mgr/cfg-data-rechecks.md)
* [De database aanpassen voor ondersteuning ](../../best-practices/mod-db-inc-replication.md)
* [De database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md)
* [Bijwerktijden reduceren](../../best-practices/reduce-update-cycle-time.md)
