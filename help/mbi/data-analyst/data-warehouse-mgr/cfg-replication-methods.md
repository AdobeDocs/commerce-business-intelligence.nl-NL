---
title: Replicatiemethoden configureren
description: Leer hoe de lijsten worden georganiseerd, en hoe het gedrag van de lijstgegevens u toestaat om de beste replicatiemethode voor uw lijsten te kiezen.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Replicatiemethoden configureren

`Replication` de methodes en [ hercontroles ](../data-warehouse-mgr/cfg-data-rechecks.md) worden gebruikt om nieuwe of bijgewerkte gegevens in uw gegevensbestandlijsten te identificeren. Een juiste instelling is van cruciaal belang voor zowel de nauwkeurigheid van de gegevens als de geoptimaliseerde updatetijden. Dit onderwerp concentreert zich op replicatiemethodes.

Wanneer de nieuwe lijsten in de [ Manager van Data Warehouse ](../data-warehouse-mgr/tour-dwm.md) worden gesynchroniseerd, wordt een replicatiemethode automatisch gekozen voor de lijst. Het begrip van de diverse replicatiemethodes, hoe de lijsten worden georganiseerd, en hoe het gedrag van de lijstgegevens u toestaat om de beste replicatiemethode voor uw lijsten te kiezen.

## Wat zijn de replicatiemethoden?

`Replication` -methoden vallen in drie groepen: `Incremental` , `Full Table` en `Paused` .

[**[!UICONTROL Incremental Replication]**](#incremental) betekent dat in [!DNL Commerce Intelligence] alleen nieuwe of bijgewerkte gegevens worden gerepliceerd bij elke replicatiepoging. Aangezien deze methoden de latentie aanzienlijk verkleinen, raadt Adobe aan deze zo veel mogelijk te gebruiken.

[**[!UICONTROL Full Table Replication]**](#fulltable) betekent dat [!DNL Commerce Intelligence] de volledige inhoud van een tabel dupliceert bij elke replicatiepoging. Vanwege de mogelijk grote hoeveelheid gegevens die moet worden gerepliceerd, kunnen deze methoden de latentie en updatetijden verhogen. Als een tabel tijdstempels of datetime-kolommen bevat, raadt Adobe aan een incrementele methode te gebruiken.

**[!UICONTROL Paused]** geeft aan dat replicatie voor de tabel is gestopt of gepauzeerd. [!DNL Commerce Intelligence] controleert niet op nieuwe of bijgewerkte gegevens tijdens een updatecyclus; dit betekent dat geen gegevens van een lijst worden herhaald die dit als zijn Methode van de Replicatie heeft.

## Incrementele replicatiemethoden {#incremental}

### Gewijzigd bij (meest ideaal)

De `Modified At` replicatiemethode gebruikt een datetime kolom - die wordt bevolkt wanneer een rij wordt gecreeerd en dan bijgewerkt wanneer de gegevens veranderen - om te herhalen gegevens te vinden. Deze methode is ontworpen voor het werken met tabellen die aan de volgende criteria voldoen:

* bevat een `datetime` -kolom die aanvankelijk wordt gevuld wanneer een rij wordt gemaakt en die wordt bijgewerkt wanneer de rij wordt gewijzigd;
* de `datetime` -kolom is nooit null;
* rijen worden niet uit de tabel verwijderd

Naast die criteria, adviseert Adobe **indexerend** de `datetime` kolom die voor `Modified At` replicatie wordt gebruikt, aangezien dit hulp replicatiesnelheid optimaliseert.

Wanneer de update wordt uitgevoerd, worden nieuwe of gewijzigde gegevens geïdentificeerd door te zoeken naar rijen met een waarde in de kolom `datetime` die na de meest recente update is opgetreden. Wanneer nieuwe rijen worden ontdekt, worden zij herhaald aan uw Data Warehouse. Als om het even welke rijen in de [ Manager van Data Warehouse ](../data-warehouse-mgr/tour-dwm.md) bestaan, worden zij met de huidige gegevensbestandwaarden beschreven.

Een tabel kan bijvoorbeeld een kolom met de naam `modified\_at` hebben die de laatste keer aangeeft dat gegevens zijn gewijzigd. Als de meest recente update dinsdag om 12.00 uur liep, zoekt de update naar alle rijen met een `modified\_at` waarde groter dan dinsdag 12.00 uur. Alle ontdekte rijen die zijn gemaakt of gewijzigd sinds 12.00 uur op dinsdag, worden gerepliceerd naar de Data Warehouse.

**Wist u het?**
Zelfs als uw gegevensbestand momenteel geen `Incremental` methode van de Replicatie kan steunen, kunt u veranderingen in uw gegevensbestand [ kunnen aanbrengen ](../../best-practices/mod-db-inc-replication.md) die gebruik van `Modified At` of `Single Auto Incrementing PK` zou toelaten.

`Modified At` is niet alleen de meest ideale replicatiemethode, maar ook de snelste. Deze methode veroorzaakt niet alleen merkbare snelheidsverhogingen met grote gegevensreeksen, het vereist ook het vormen van geen recheck optie. Andere methoden moeten een hele tabel doorlopen om wijzigingen te identificeren, zelfs als een kleine subset van gegevens is gewijzigd. `Modified At` doorloopt alleen die kleine subset.

### Eén automatische incrementele primaire sleutel

`Auto Incrementing` is een gedrag dat achtereenvolgens primaire sleutels aan rijen toewijst. Als een tabel `Auto Incrementing` is en de hoogste primaire sleutel in de tabel 1000 is, is de volgende primaire waarde 1001 of hoger. Een tabel die het gedrag `Auto Incrementing` niet gebruikt, kan een waarde voor de primaire sleutel toewijzen die lager is dan 1000 of naar een veel groter getal springen, maar dit wordt niet vaak gebruikt.

Deze methode is ontworpen voor het repliceren van nieuwe gegevens uit tabellen die aan de volgende criteria voldoen:

* `single-column primary key` en
* `primary key` datatype is `integer` ; en
* `auto incrementing` waarden van primaire sleutels.

Wanneer een tabel gebruikmaakt van `Single Auto Incrementing Primary Key` -replicatie, worden nieuwe gegevens gedetecteerd door te zoeken naar waarden voor primaire sleutels die hoger zijn dan de huidige hoogste waarde in uw Data Warehouse. Als de hoogste waarde voor de primaire sleutel in uw Data Warehouse bijvoorbeeld 500 is, zoekt de volgende update naar rijen met de primaire-sleutelwaarden 501 of hoger.

### Datum toevoegen

De methode `Add Date` werkt ongeveer op dezelfde manier als de methode `Single Auto Incrementing Primary Key` . In plaats van een geheel getal voor de primaire sleutel van de tabel te gebruiken, gebruikt deze methode een kolom `timestamped` om te controleren op nieuwe rijen.

Wanneer een tabel gebruikmaakt van `Add Date` -replicatie, worden nieuwe gegevens gedetecteerd door te zoeken naar waarden met een tijdstempel die groter zijn dan de laatste datum die is gesynchroniseerd met uw Data Warehouse. Bijvoorbeeld, als een update het laatst op 20/12/2015 09 :00: 00 liep, om het even welke rijen met een timestamp groter dan dit zullen als nieuwe gegevens worden gemerkt en worden herhaald.

>[!NOTE]
>
>In tegenstelling tot de methode `Modified At` controleert `Add Date` bestaande rijen niet op bijgewerkte informatie - het kijkt slechts naar nieuwe rijen uit.

## Volledige tabelreplicatiemethoden {#fulltable}

### Volledige tabel

Met `Full table` vernieuwt u de volledige tabel wanneer nieuwe rijen worden gedetecteerd. Dit is verreweg de minst efficiënte replicatiemethode, omdat alle gegevens tijdens elke update moeten worden opnieuw verwerkt, veronderstellend er nieuwe rijen zijn.

Nieuwe rijen worden ontdekt door uw gegevensbestand bij het begin van het synchronisatieproces te vragen en het aantal rijen te tellen. Als uw lokale database meer rijen bevat dan [!DNL Commerce Intelligence] , wordt de tabel vernieuwd. Als de rijtellingen identiek zijn, of als [!DNL Commerce Intelligence] *meer* rijen dan uw lokaal gegevensbestand bevat, dan wordt de lijst overgeslagen.

Dit werpt het belangrijke punt op dat replicatie in **`Full Table`niet compatibel is wanneer:**

* er tussen volgende updatecycli meer rijen worden verwijderd dan in uw lokale databasetabel zijn gemaakt, of
* kolomwaarden worden gewijzigd, maar er worden geen extra rijen gemaakt

In beide bovenstaande scenario&#39;s worden door `Full Table` -replicatie geen wijzigingen gedetecteerd en worden uw gegevens verouderd. Vanwege de inefficiëntie van deze replicatiemethode en de hierboven vermelde vereisten wordt `Full Table` -replicatie alleen aanbevolen als laatste redmiddel.

### Batch primaire sleutel

Wanneer een tabel `Primary Key Batch` (PK-batch) gebruikt, worden nieuwe gegevens gedetecteerd door rijen binnen bereiken, of batches, van waarden voor primaire sleutels te tellen. Terwijl u typisch denkt dat dit met gehelen wordt gebruikt, zelfs kunnen de tekstwaarden op een manier worden bevolen die het systeem toestaat om constante waaiers te bepalen.

Bijvoorbeeld, zeg dat een update looppas en een rijtelling voor de waaier van sleutels van 1 tot 100 uitvoert. In deze update zoekt en registreert het systeem 37 rijen. In de volgende update wordt opnieuw een rijtelling uitgevoerd voor het bereik 1-100 en worden 41 rijen gevonden. Omdat er een verschil is in het aantal rijen in vergelijking met de laatste update, inspecteert het systeem die waaier (of partij) meer in detail.

Deze methode is bedoeld voor het repliceren van gegevens uit tabellen die aan de volgende criteria voldoen:

* één kolom, niet geheel getal; of
* samengestelde sleutels (meerdere kolommen die de primaire sleutel vormen) - houd er rekening mee dat kolommen die in een samengestelde primaire sleutel worden gebruikt nooit null-waarden kunnen hebben; of
* waarden voor één kolom, gehele getallen, niet automatisch incrementele primaire sleutels.

Deze methode is niet ideaal, omdat het ongelooflijk langzaam is door de hoeveelheid verwerking die moet plaatsvinden om partijen te onderzoeken en veranderingen te vinden. Adobe raadt u aan deze methode alleen te gebruiken als het niet mogelijk is de benodigde wijzigingen aan te brengen om de andere replicatiemethoden te ondersteunen. Verwacht dat de updatetijden zullen stijgen als deze methode moet worden gebruikt.

## Replicatiemethoden instellen

De methodes van de replicatie worden geplaatst op een lijst-door-lijst basis. Als u een replicatiemethode voor een tabel wilt instellen, hebt u [`Admin`](../../administrator/user-management/user-management.md) -machtigingen nodig, zodat u toegang kunt krijgen tot Data Warehouse Manager.

1. Selecteer eenmaal in Data Warehouse Manager de tabel in de lijst `Synced Tables` om het tabelschema weer te geven.
1. De huidige replicatiemethode wordt vermeld onder de lijstnaam. Klik op de koppeling om deze te wijzigen.
1. Klik in het pop-upvenster dat wordt weergegeven op het keuzerondje naast `Incremental` of `Full Table` replicatie om een replicatietype te selecteren.
1. Klik vervolgens op het vervolgkeuzemenu **[!UICONTROL Replication Method]** om een methode te selecteren. Bijvoorbeeld `Paused` of `Modified At` .

   >[!NOTE]
   >
   >**sommige Incrementele methodes vereisen u om a`Replication Key`** te plaatsen. [!DNL Commerce Intelligence] gebruikt deze sleutel om te bepalen waar de volgende updatecyclus moet beginnen.
   >
   >Als u bijvoorbeeld de methode `modified at` voor uw `orders` -tabel wilt gebruiken, moet u een `date column` als replicatietoets instellen. Er kunnen verschillende opties voor replicatietoetsen bestaan, maar u selecteert `created at` of het tijdstip waarop de volgorde is gemaakt. Als de laatste updatecyclus bij 12/1/2015 00 :10: 00 werd tegengehouden, zou de volgende cyclus beginnen herhalend gegevens met een `created at` datum groter dan dit.

1. Klik op **[!UICONTROL Save]** als u klaar bent.

Kijk naar het hele proces:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Omloop

Om omhoog te beëindigen, hebt u deze lijst samengebracht die de diverse replicatiemethodes vergelijkt. Het is ongelooflijk handig als u een methode selecteert voor de tabellen in uw Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Sneller | Langzaam | Nee | Nee | Nee | Ja |
| `Primary Key Batch Monitoring` | Langzaam | Langzaam | Ja | Ja | Ja | Ja |
| `Modified At` | Sneller | Sneller | Ja | Ja | Ja | Nee |

{style="table-layout:auto"}

## Gerelateerde documentatie

* [Hercontroles van gegevens](../data-warehouse-mgr/cfg-data-rechecks.md)
* [De database aanpassen voor ondersteuning ](../../best-practices/mod-db-inc-replication.md)
* [De database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md)
* [Bijwerktijden reduceren](../../best-practices/reduce-update-cycle-time.md)
