---
title: Replicatiemethoden configureren
description: Leer hoe de lijsten worden georganiseerd, en hoe het gedrag van de lijstgegevens u toestaat om de beste replicatiemethode voor uw lijsten te kiezen.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# Replicatiemethoden configureren

`Replication` methoden en [hercontroles](../data-warehouse-mgr/cfg-data-rechecks.md) worden gebruikt om nieuwe of bijgewerkte gegevens in uw gegevensbestandlijsten te identificeren. Een juiste instelling is van cruciaal belang voor zowel de nauwkeurigheid van de gegevens als de geoptimaliseerde updatetijden. Dit onderwerp concentreert zich op replicatiemethodes.

Wanneer nieuwe tabellen worden gesynchroniseerd in het dialoogvenster [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), wordt automatisch een replicatiemethode gekozen voor de tabel. Het begrip van de diverse replicatiemethodes, hoe de lijsten worden georganiseerd, en hoe het gedrag van de lijstgegevens u toestaat om de beste replicatiemethode voor uw lijsten te kiezen.

## Wat zijn de replicatiemethoden?

`Replication` de methoden vallen onder drie groepen - `Incremental`, `Full Table`, en `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) betekent dat [!DNL Commerce Intelligence] Hiermee kopieert u alleen nieuwe of bijgewerkte gegevens bij elke replicatiepoging. Aangezien deze methoden de latentie aanzienlijk verkleinen, wordt u aangeraden deze zo veel mogelijk te gebruiken.

[**[!UICONTROL Full Table Replication]**](#fulltable) betekent dat [!DNL Commerce Intelligence] repliceert de volledige inhoud van een lijst op elke replicatiepoging. Vanwege de mogelijk grote hoeveelheid gegevens die moet worden gerepliceerd, kunnen deze methoden de latentie en updatetijden verhogen. Als een lijst om het even welke timestamped of datetime kolommen bevat, adviseert Adobe het gebruiken van een Incrementele methode in plaats daarvan.

**[!UICONTROL Paused]** Hiermee wordt aangegeven dat de replicatie voor de tabel wordt gestopt of gepauzeerd. [!DNL Commerce Intelligence] niet controleert op nieuwe of bijgewerkte gegevens tijdens een updatecyclus; dit betekent dat geen gegevens van een lijst worden herhaald die dit als zijn Methode van de Replicatie heeft.

## Incrementele replicatiemethoden {#incremental}

### Gewijzigd bij (meest ideaal)

De `Modified At` De replicatiemethode gebruikt een datetime kolom - die wordt bevolkt wanneer een rij wordt gecreeerd en dan bijgewerkt wanneer de gegevens veranderen - om gegevens te vinden om te herhalen. Deze methode is ontworpen voor het werken met tabellen die aan de volgende criteria voldoen:

* bevat een `datetime` kolom die aanvankelijk wordt gevuld wanneer een rij wordt gecreeerd en bijgewerkt wanneer de rij wordt gewijzigd;
* de `datetime` de kolom is nooit null;
* rijen worden niet uit de tabel verwijderd

Naast deze criteria beveelt Adobe aan **indexeren** de `datetime` kolom gebruikt voor `Modified At` replicatie, aangezien dit de replicatiesnelheid helpt optimaliseren.

Wanneer de update wordt uitgevoerd, worden nieuwe of gewijzigde gegevens geïdentificeerd door te zoeken naar rijen met een waarde in het dialoogvenster `datetime` kolom die is opgetreden na de meest recente update. Wanneer nieuwe rijen worden ontdekt, worden zij herhaald aan uw Data Warehouse. Als er rijen voorkomen in het dialoogvenster [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), worden ze overschreven met de huidige databasewaarden.

Een tabel kan bijvoorbeeld een kolom met de naam `modified\_at` dat aangeeft wanneer de laatste gegevens zijn gewijzigd. Als de meest recente update dinsdag om 12.00 uur liep, zoekt de update naar alle rijen met een `modified\_at` waarde groter dan dinsdag om 12.00 uur. Alle ontdekte rijen die zijn gemaakt of gewijzigd sinds 12.00 uur op dinsdag, worden gerepliceerd naar de Data Warehouse.

**Wist je dat?**
Zelfs als uw database momenteel geen ondersteuning biedt voor een `Incremental` Replicatiemethode: [wijzigingen aanbrengen in uw database](../../best-practices/mod-db-inc-replication.md) dat het gebruik van `Modified At` of `Single Auto Incrementing PK`.

`Modified At` is niet alleen de meest ideale replicatiemethode, maar ook de snelste. Deze methode veroorzaakt niet alleen merkbare snelheidsverhogingen met grote gegevensreeksen, het vereist ook het vormen van geen recheck optie. Andere methoden moeten een hele tabel doorlopen om wijzigingen te identificeren, zelfs als een kleine subset van gegevens is gewijzigd. `Modified At` Hiermee doorloopt u alleen die kleine subset.

### Eén automatische verhogende primaire sleutel

`Auto Incrementing` is een gedrag dat opeenvolgende primaire sleutels aan rijen toewijst. Als een tabel `Auto Incrementing` en de hoogste primaire sleutel in de tabel is 1.000, dan is de volgende primaire waarde 1.001 of hoger. Een tabel die niet wordt gebruikt `Auto Incrementing` kan gedrag een primaire sleutelwaarde toewijzen die minder is dan 1.000 of naar een veel groter getal springen, maar dit wordt niet vaak gebruikt.

Deze methode is ontworpen voor het repliceren van nieuwe gegevens uit tabellen die aan de volgende criteria voldoen:

* `single-column primary key`; en
* `primary key` datatype is `integer`; en
* `auto incrementing` waarden van primaire sleutels.

Wanneer een tabel wordt gebruikt `Single Auto Incrementing Primary Key` replicatie, worden de nieuwe gegevens ontdekt door naar primaire zeer belangrijke waarden te zoeken die hoger zijn dan de huidige hoogste waarde in uw Data Warehouse. Als de hoogste waarde voor de primaire sleutel in de Data Warehouse bijvoorbeeld 500 is, zoekt de volgende update naar rijen met de primaire sleutel waarden 501 of hoger.

### Datum toevoegen

De `Add Date` methodefuncties die vergelijkbaar zijn met de `Single Auto Incrementing Primary Key` methode. In plaats van een geheel getal voor de primaire sleutel van de tabel te gebruiken, gebruikt deze methode een `timestamped` te controleren op nieuwe rijen.

Wanneer een tabel `Add Date` replicatie, worden de nieuwe gegevens ontdekt door timestamped waarden te zoeken die groter zijn dan de recentste datum die aan uw Data Warehouse wordt gesynchroniseerd. Bijvoorbeeld, als een laatste update op 20/12/2015 09 liep:00:00, worden rijen met een tijdstempel die groter is dan dit, gemarkeerd als nieuwe gegevens en gerepliceerd.

>[!NOTE]
>
>In tegenstelling tot `Modified At` methode, `Add Date` controleert bestaande rijen niet op bijgewerkte informatie - het kijkt slechts naar nieuwe rijen uit.

## Volledige tabelreplicatiemethoden {#fulltable}

### Volledige tabel

`Full table` de replicatie verfrist de volledige lijst wanneer de nieuwe rijen worden ontdekt. Dit is verreweg de minst efficiënte replicatiemethode, omdat alle gegevens tijdens elke update moeten worden opnieuw verwerkt, veronderstellend er nieuwe rijen zijn.

Nieuwe rijen worden ontdekt door uw gegevensbestand bij het begin van het synchronisatieproces te vragen en het aantal rijen te tellen. Als uw lokale database meer rijen bevat dan [!DNL Commerce Intelligence]Dan wordt de tabel vernieuwd. Als het aantal rijen identiek is of als [!DNL Commerce Intelligence] contains *meer* De tabel wordt overgeslagen als de lokale database geen rijen bevat.

Dit brengt het belangrijke punt aan de orde dat **`Full Table`replicatie is niet compatibel wanneer:**

* er tussen volgende updatecycli meer rijen worden verwijderd dan in uw lokale databasetabel zijn gemaakt, of
* kolomwaarden worden gewijzigd, maar er worden geen extra rijen gemaakt

In beide bovengenoemde scenario&#39;s `Full Table` de replicatie ontdekt geen veranderingen en uw gegevens worden versleten. Door de inefficiëntie van deze replicatiemethode en de hierboven vermelde vereisten, `Full Table` replicatie wordt alleen aanbevolen als laatste redmiddel.

### Batch primaire sleutel

Wanneer een tabel `Primary Key Batch` (PK-batch), worden nieuwe gegevens gedetecteerd door rijen binnen bereiken, of batches, van primaire-sleutelwaarden te tellen. Terwijl u typisch denkt dat dit met gehelen wordt gebruikt, zelfs kunnen de tekstwaarden op een manier worden bevolen die het systeem toestaat om constante waaiers te bepalen.

Bijvoorbeeld, zeg dat een update looppas en een rijtelling voor de waaier van sleutels van 1 tot 100 uitvoert. In deze update zoekt en registreert het systeem 37 rijen. In de volgende update wordt opnieuw een rijtelling uitgevoerd voor het bereik 1-100 en worden 41 rijen gevonden. Omdat er een verschil is in het aantal rijen in vergelijking met de laatste update, inspecteert het systeem die waaier (of partij) meer in detail.

Deze methode is bedoeld voor het repliceren van gegevens uit tabellen die aan de volgende criteria voldoen:

* één kolom, niet geheel getal; of
* samengestelde sleutels (meerdere kolommen die de primaire sleutel vormen) - houd er rekening mee dat kolommen die in een samengestelde primaire sleutel worden gebruikt nooit null-waarden kunnen hebben; of
* waarden voor één kolom, gehele getallen, niet automatisch incrementele primaire sleutels.

Deze methode is niet ideaal, omdat het ongelooflijk langzaam is door de hoeveelheid verwerking die moet plaatsvinden om partijen te onderzoeken en veranderingen te vinden. Adobe raadt u aan deze methode alleen te gebruiken als het niet mogelijk is de benodigde wijzigingen aan te brengen ter ondersteuning van de andere replicatiemethoden. Verwacht dat de updatetijden zullen stijgen als deze methode moet worden gebruikt.

## Replicatiemethoden instellen

De methodes van de replicatie worden geplaatst op een lijst-door-lijst basis. Om een replicatiemethode voor een lijst te plaatsen, hebt u nodig [`Admin`](../../administrator/user-management/user-management.md) machtigingen zodat u toegang hebt tot Data Warehouse Manager.

1. Eenmaal in Beheer Data Warehouse selecteert u de tabel in het menu `Synced Tables` om het schema van de tabel weer te geven.
1. De huidige replicatiemethode wordt vermeld onder de lijstnaam. Klik op de koppeling om deze te wijzigen.
1. Klik in het pop-upvenster dat wordt weergegeven op het keuzerondje naast een van de twee `Incremental` of `Full Table` replicatie om een replicatietype te selecteren.
1. Klik op de knop **[!UICONTROL Replication Method]** vervolgkeuzelijst om een methode te selecteren. Bijvoorbeeld: `Paused` of `Modified At`.

   >[!NOTE]
   >
   >**Voor sommige incrementele methoden moet u een`Replication Key`**. [!DNL Commerce Intelligence] zal deze sleutel gebruiken om te bepalen waar de volgende updatecyclus zou moeten beginnen.
   >
   >Als u bijvoorbeeld de opdracht `modified at` methode voor uw `orders` tabel, moet u een `date column` als replicatietoets. Er kunnen verschillende opties voor replicatietoetsen bestaan, maar u selecteert `created at`of de tijd waarop de bestelling is gemaakt. Als de laatste updatecyclus op 12-1-2015 00 is gestopt:10:00, de volgende cyclus zou beginnen gegevens te repliceren met een `created at` datum groter dan deze.

1. Als u klaar bent, klikt u op **[!UICONTROL Save]**.

Kijk naar het hele proces:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Omloop

Om omhoog te beëindigen, hebt u deze lijst samengebracht die de diverse replicatiemethodes vergelijkt. Het is ongelooflijk handig als u een methode voor de tabellen in uw Data Warehouse selecteert.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Sneller | Langzaam | Nee | Nee | Nee | Ja |
| `Primary Key Batch Monitoring` | Langzaam | Langzaam | Ja | Ja | Ja | Ja |
| `Modified At` | Sneller | Sneller | Ja | Ja | Ja | Nee |

{style="table-layout:auto"}

## Gerelateerde documentatie

* [Gegevens opnieuw controleren](../data-warehouse-mgr/cfg-data-rechecks.md)
* [De database aanpassen voor ondersteuning ](../../best-practices/mod-db-inc-replication.md)
* [De database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md)
* [Bijwerktijden reduceren](../../best-practices/reduce-update-cycle-time.md)
