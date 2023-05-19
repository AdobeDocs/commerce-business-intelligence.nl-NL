---
title: Data Warehouse Manager
description: Leer hoe te om lijst en kolomsync montages te beheren, boor neer in het schema van een lijst, en creeer berekende kolommen in rapporten te gebruiken.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: c4094e780f83255846520d18f4d0806b1dd9a9ef
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Data Warehouse Manager

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md)

De Manager van de Data Warehouse, die door te klikken wordt betreden **[!UICONTROL Manage Data > Data Warehouse]**, is het portaal voor uw [!DNL Adobe Commerce Intelligence] Data Warehouse. Gebruikend de Manager van de Data Warehouse, kunt u lijst en kolomsync montages beheren, neer in het schema van een lijst boren, en berekende kolommen tot stand brengen in rapporten te gebruiken.

Dit onderwerp omvat:

* [Leer je weg](#learning)
* [Tabellen en kolommen synchroniseren](#syncing)
* [Berekende kolommen maken](#calculated)
* [Tabellen neerzetten en kolommen verwijderen](#delete)
* [Nieuwe tabellen op de achtergrond synchroniseren](#syncnew)
* [Wanneer kan ik mijn nieuwe kolommen gebruiken?](#when)

## Leer je weg {#learning}

De linkerkant van `Data Warehouse Manager` Deze pagina bevat de lijst met tabellen, zodat u eenvoudig kunt schakelen tussen tabellen. Wanneer u een tabel in de lijst selecteert, wordt het tabelbeheergebied gevuld met het schema van de tabel waarin u de geselecteerde tabel kunt wijzigen.

Binnen de lijst van de lijst, worden de lijsten gegroepeerd door hun verbindingsbron. Deze bronnen worden toegevoegd onder [!UICONTROL Manage Data > Integrations] en kan een database zijn, en [API](https://developer.adobe.com/commerce/services/reporting/)of een aansluiting van derden. Boven aan de lijst met tabellen bevindt zich een zoekvak waarmee u gemakkelijk de gewenste tabellen kunt vinden.

Onder het zoekvak ziet u twee opties: `All Tables` en `Synced Tables`. De `All Tables` Hiermee worden alle tabellen weergegeven die u ter beschikking van de Data Warehouse hebt gesteld. Deze tabellen bevatten zowel gesynchroniseerde als niet-gesynchroniseerde tabellen.

De `Synced Tables` toont alle lijsten die reeds aan uw Data Warehouse zijn toegevoegd en gegevens hebben die van de geselecteerde kolommen worden herhaald.

Zie de tabel die u zoekt niet in het dialoogvenster `All Tables` lijst? Hiervoor zijn enkele redenen te vinden:

* De gegevensbron is nog niet toegevoegd
* De gegevensbron is een database en de [!DNL Commerce Intelligence] de gebruiker die u hebt gemaakt, heeft geen toegang. In dit geval moet u of uw databasebeheerder toegang verlenen.
* De gegevensbron of tabel is onlangs toegevoegd en nog niet gesynchroniseerd

## Tabellen en kolommen synchroniseren {#syncing}

### Nieuwe tabellen en native kolommen synchroniseren

De Manager van de Data Warehouse geeft u niet alleen de capaciteit om uw gegevensbronnen gemakkelijk te bekijken en te beheren, u hebt ook de vrijheid om de individuele lijsten en de kolommen te selecteren u wilt synchroniseren.

1. Klik op de knop `All Tables` en zoek de tabel die u wilt synchroniseren.
1. Klik op de naam van de tabel om een voorvertoning van het schema weer te geven. Als de tabel nieuw is, worden alle kolommen weergegeven als `Unsynced`.
1. Controleer de kolommen die u wilt synchroniseren.

   >[!NOTE]
   >
   >Kolommen die native zijn voor een tabel, zijn afkomstig uit uw database in de `Location` kolom.

1. Controleer of de `Primary Key` kolommen - deze kolommen hebben een sleutelsymbool naast de kolomnaam. A `Primary Key` is vereist om gegevens correct te synchroniseren in de Data Warehouse.

   Als u een tabel synchroniseert die rechtstreeks afkomstig is uit uw database, is het mogelijk dat `Primary Keys` mag niet worden aangegeven. In dit geval neemt u contact op met de databasebeheerder om te vragen of een primaire sleutel of sleutels aan de tabel moet worden toegevoegd.
1. Als u klaar bent, klikt u op de knop ![knop](../../assets/button.png) knop.

A *Succes!* berichtweergaven en de status verandert in `Pending` voor de geselecteerde kolommen. Nadat de volgende volledige update is voltooid, zijn de nieuw gesynchroniseerde tabellen en kolommen beschikbaar voor gebruik in rapporten. U kunt ook nieuwe [replicatiemethoden](./cfg-replication-methods.md) na de eerste synchronisatie.

Hieronder volgt een kort overzicht van het hele proces:

![Kolommen toevoegen aan uw gegevenspakhuis](../../assets/DW_sync.gif)

### Nieuwe tabellen synchroniseren op de achtergrond {#syncnew}

Wanneer u een grote lijst voor het eerst synchroniseert, moet uw Data Warehouse alle gegevenspunten in de lijst terugwerkende kracht vangen alvorens nieuwe gegevens op een lopende basis te vangen. Als de tabel groot is, is het mogelijk dat de eerste synchronisatie niet op volgorde met de **updatecyclus**. In deze situatie wilt u dat de eerste synchronisatie op de achtergrond plaatsvindt, in *parallel* met een actieve update.

Om ervoor te zorgen dat dit gebeurt, selecteert u de optie `Save and Sync Data Immediately` die tabel voor het eerst synchroniseert.

### Controleren op nieuwe tabellen en kolommen {#forceupdate}

Uw Data Warehouse ontdekt automatisch geen nieuwe bronnen, lijsten, of kolommen het ogenblik zij worden toegevoegd. Een synchronisatieproces loopt door de week om nieuwe toevoegingen te vinden en hen ter beschikking te stellen, maar u kunt een structuursynchronisatie dwingen als u tot onlangs toegevoegde lijsten en kolommen wilt toegang hebben alvorens het proces loopt.

Onder de zoekbalk in de tabellijst bevindt zich een `Check for new tables and columns` koppeling. Als u op deze koppeling klikt, wordt het proces voor het synchroniseren van de structuur geforceerd gestart. nieuwe toevoegingen zijn doorgaans na 10 minuten beschikbaar. Vernieuw de pagina om de nieuwe bron, tabel of kolom te zien.

## Berekende kolommen maken {#calculated}

Eenvoudig het kunnen gegevens van al uw bronnen zien en beheren maakt het verkrijgen van inzicht in uw zaken veel gemakkelijker. Maar binnen de Manager van de Data Warehouse, kunt u een stap verder gaan door berekende kolommen binnen uw lijsten te creëren. `Calculated` de kolommen leiden nieuwe informatie uit uw bestaande gegevens af.

Zeg u wilt toevoegen `user's lifetime revenue` aan uw `users` tabel om gebruikers met een hoge waarde te zoeken. Of, als u opbrengst door geslacht wilt segmenteren, kunt u toevoegen `customer's gender` aan uw `orders` tabel.

Raadpleeg deze voor meer informatie [zelfstudie](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Tabellen neerzetten en kolommen verwijderen {#delete}

Net zoals u tabellen en kolommen kunt selecteren die u met de Data Warehouse wilt synchroniseren, kunt u ze ook neerzetten of verwijderen.

>[!NOTE]
>
>Als u een tabel neerzet of kolommen verwijdert, worden afhankelijke rapporten, metriek, filtersets en kolommen verwijderd zodra u de verwijdering hebt bevestigd. Wees zeker dat je dit wilt doen - **deze handeling kan niet ongedaan worden gemaakt.**

U hoeft zich geen zorgen te maken als u op **[!UICONTROL Delete]** per ongeluk. Een gebiedsdeelcontrole loopt alvorens om het even wat wordt geschrapt, zodat hebt u de kans om alles te herzien alvorens te bevestigen.

Als u kolommen wilt verwijderen, klikt u op de tabel waartoe de kolom behoort. Controleer de kolommen die u wilt verwijderen en klik op de knop ![knop\_1.png](../../assets/button_1.png) knop.

Als u een gesynchroniseerde tabel wilt verwijderen, selecteert u alle kolommen in de tabel en klikt u nogmaals op de knop ![knop](../../assets/button_1.png) knop. Hierdoor worden alle native en berekende kolommen die deze tabel gebruiken, uit de Data Warehouse verwijderd.

### Wijzigingen bevestigen

Of u een lijst laat vallen of kolommen verwijdert, een looppas van de gebiedsdeelcontrole alvorens het schrappingsproces voltooit. Afhankelijkheden zijn berekende kolommen, metriek, filterreeksen en rapporten die de tabel of kolom(men) gebruiken die worden verwijderd. Om het even welke ontdekte gebiedsdelen tonen - op dit punt kunt u of het proces annuleren of klikken **[!UICONTROL Confirm Changes]** om de tabel neer te zetten/de kolom(men) te verwijderen.

Terwijl de geschrapte gebiedsdelen niet kunnen worden hersteld, zullen de lijsten en de kolommen nog beschikbaar zijn als u om het even welke inheemse kolommen in de toekomst opnieuw moet synchroniseren.

Hier volgt een snelle blik bij het verwijderen van een kolom:

![Het verwijderen van een kolom uit uw gegevenspakhuis](../../assets/DW_delete.gif)

## Wanneer kan ik mijn nieuwe kolommen gebruiken? {#when}

Nieuwe gesynchroniseerde kolommen en nieuwe/bijgewerkte berekende kolommen zijn klaar voor gebruik nadat de volgende volledige update is voltooid. Als er nog geen update wordt uitgevoerd, kunt u een update afdwingen door op **[!UICONTROL Force update]** boven aan het dialoogvenster `Data Warehouse` of `Integrations` pagina. U kunt ook een e-mailmelding plannen wanneer de update is voltooid door op **[!UICONTROL Email me when complete]**.

Wanneer u klaar bent om uw nieuwe kolommen in rapporten te gebruiken, [u moet ze eerst aan metriek toevoegen](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Hoewel gegevens pas beschikbaar zijn nadat een update is voltooid, kunt u nog steeds nieuwe kolommen in rapporten gebruiken. De gegevens binnen het rapport worden weergegeven wanneer de update is voltooid.

## Omloop

Dit artikel bedekte veel materiaal. Ondertussen, zou u een stevig inzicht in wat een gegevensbestand is, hoe de gegevens worden georganiseerd, hoe de lijsten met elkaar betrekking hebben, en wat u met de Manager van de Data Warehouse kunt doen.

Test uw kennis door [een berekende kolom maken](../data-warehouse-mgr/creating-calculated-columns.md) of [interessante verslagen](../../tutorials/using-visual-report-builder.md).
