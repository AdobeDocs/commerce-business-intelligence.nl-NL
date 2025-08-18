---
title: Het ontcijferen van uw  [!DNL Commerce Intelligence]  rekening
description: Leer hoe te om uw  [!DNL Commerce Intelligence]  rekening op te schonen.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Uw [!DNL Adobe Commerce Intelligence] -account opruimen

Of u nu al zes maanden of zes jaar bij [!DNL Commerce Intelligence] bent, het bijhouden van een proefaccount is van het grootste belang voor uw organisatie om het beste uit het platform te halen. In tijd, is het natuurlijk voor er gebruikers, dashboards, rapporten, metriek, en kolommen zijn die niet meer nodig zijn. Mogelijk hebt u een rapport gemaakt voor eenmalig gebruik en bent u vergeten of heeft een gebruiker die uw bedrijf heeft verlaten, zijn account nooit gedeactiveerd.

Met [ gestandaardiseerde, duidelijke noemende voor alle elementen ](../best-practices/naming-elements.md)) van uw [!DNL Commerce Intelligence] rekening, helpen de stappen van de rekeningscontrole hieronder u de rommelige en onnodige analyses voor uw gebruikers verminderen. Één extra voordeel omvat [ potentieel snellere updatecycli ](../best-practices/reduce-update-cycle-time.md).

## Stap 1: Identificeer uw niet-actieve gebruikers

De eerste stap bij het opschonen van uw account is het deactiveren van de accounts van niet-actieve gebruikers, zoals personen die het bedrijf hebben verlaten of [!DNL Commerce Intelligence] niet meer gebruiken in hun huidige rollen.

U doet dit door op de naam van uw bedrijf in de navigatiebalk rechtsboven te klikken en vervolgens **[!UICONTROL Manage Users]** te selecteren. Selecteer vervolgens de gebruiker die u wilt deactiveren en klik op **[!UICONTROL Deactivate User]** .

>[!NOTE]
>
>U hebt [ toestemmingen Admin ](../administrator/user-management/user-management.md) nodig om dit te doen.

>[!WARNING]
>
>Als u een gebruiker deactiveert, verwijdert u de diagrammen, dashboards en andere elementen die door die gebruiker zijn gemaakt. Als u deze activa wilt bewaren, contacteer het [!DNL Commerce Intelligence] [ steun ](../guide-overview.md#Submitting-a-Support-Ticket) team alvorens de gebruiker te deactiveren. Ondersteuning kan u helpen deze middelen over te brengen naar een andere gebruiker.

### Gebruiker opnieuw activeren

Als u een gebruiker opnieuw wilt activeren, nodigt u de gebruiker opnieuw uit door zijn account opnieuw te maken met hetzelfde e-mailadres dat is gedeactiveerd, en de toegang tot de gebruiker en de gegevens die hij of zij bezat, worden bij de aanmelding hersteld.

## Stap 2: Ongebruikte dashboards en rapporten verwijderen

De volgende stap bij het controleren van uw account is het verwijderen van ongebruikte dashboards en rapporten.

>[!NOTE]
>
>U hebt `Admin` of `Standard` [ gebruikerstoestemmingen ](../administrator/user-management/user-management.md) nodig om dit te doen.

Elke gebruiker met `Admin` of `Standard` toegang kan rapporten en dashboards tot stand brengen. Daarom moet iedereen met deze machtigingen de onderstaande stappen volgen om ongebruikte rapporten te identificeren en te verwijderen.

### Controleer uw dashboards en rapporten

Voordat u iets verwijdert, moet u eerst uw rapporten en dashboards bekijken om te beoordelen wat er in gebruik is. Hoewel u de hieronder beschreven functie **[!UICONTROL find unused reports]** kunt gebruiken, zorgt een eerste revisie ervoor dat uw opschoonbewerkingen veel productiever worden.

### Dashboards en rapporten verwijderen

Nadat u toegang hebt tot uw dashboards en rapporten, kunt u beginnen uw rekening op te schonen.

**om een Rapport uit een Dashboard** te verwijderen

1. Zoek het rapport dat u op het dashboard wilt verwijderen.
1. Selecteer **[!UICONTROL Options]** rechtsboven in het rapport.
1. Klik op **[!UICONTROL Remove From Dashboard]**.

**om een volledig dashboard** te schrappen

1. Selecteer **[!UICONTROL Manage Data]**, dan **&#x200B; [!UICONTROL Dashboards**].
1. Klik op het dashboard dat u wilt verwijderen.
1. Klik op **[!UICONTROL Delete Dashboard]**.

U kunt ook **[!UICONTROL Dashboard Options]** selecteren en vervolgens **[!UICONTROL Delete]** in het dashboard zelf.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>Als u een dashboard verwijdert, worden de rapporten in het dashboard niet verwijderd. U moet dus nog een stap ondernemen om de rapporten te verwijderen.

**om Ongebruikte Rapporten te schrappen**

1. Selecteer **[!UICONTROL Manage Data]** en vervolgens **[!UICONTROL Reports]** .
1. Controle **toont slechts ongebruikte rapporten** doos onder de metrieklijst wordt gevestigd. Hiermee maakt u een lijst met rapporten die niet worden gebruikt in een dashboard- of e-mailoverzicht.
1. Selecteer de rapporten die u wilt schrappen. U kunt alle selecteren door checkbox boven de rapportlijst te klikken.
1. Klik op **[!UICONTROL Delete Selected]**.

Hier is een blik op het ongebruikte proces van de rapportschrapping:

![](../../mbi/assets/unused_reports.png)

## Stap 3: Ongebruikte metriek verwijderen

Nadat u uw gebruikerslijst, dashboards, en rapporten hebt schoongemaakt, kunt u zich op controle van uw lijst van metriek bewegen. Dit helpt u om het even wat identificeren die verouderd zou kunnen zijn - bijvoorbeeld, werd nieuw metrisch gecreeerd met een verschillende definitie - of niet in gebruik.

1. Als u een lijst met afhankelijke rapporten voor een metrische waarde wilt genereren, gaat u naar **[!DNL Manage Data]** en selecteert u Klikken **[!UICONTROL Metrics]** .
1. Klik op **[!UICONTROL Edit]** naast een metrische waarde.
1. Onder aan de pagina ziet u een sectie met de naam **[!UICONTROL Dependent Charts]** . Klik de verbinding om een afhankelijke rapportlijst voor dit metrisch te produceren.
1. Nadat het systeem de controle voltooit, [!DNL Commerce Intelligence] toont een lijst van dashboards, rapporten, en gebruikers die dit metrisch gebruiken.

![](../../mbi/assets/report_dependecies.png)

Als u besluit dat de metrische waarde niet meer nodig is, navigeert u weer naar de pagina **[!UICONTROL Metrics]** door op **[!UICONTROL Back to Metric List]** te klikken om de metrische waarde te zoeken die u wilt verwijderen. Klik op **[!UICONTROL Delete]**.

## Stap 4: De gesynchroniseerde kolommen beoordelen

De laatste stap bestaat uit het beoordelen van de kolommen die momenteel worden gesynchroniseerd in uw Data Warehouse. U kunt niet alleen de synchronisatie van kolommen in uw account ongedaan maken, maar ook de updatetijd verminderen.

Als u dit zou willen nastreven, bereik uit aan [!DNL Commerce Intelligence] [ Steun ](../guide-overview.md#Submitting-a-Support-Ticket). Het ondersteuningsteam kan een rapport maken dat alle kolommen bevat die in geen enkel dashboard voor een gebruiker worden gebruikt en die niet in e-mailoverzichten worden gebruikt, met uitzondering van SQL-rapporten. U kunt dit rapport vervolgens gebruiken als richtlijn voor het selecteren van kolommen die u niet wilt synchroniseren via Data Warehouse Manager.

>[!NOTE]
>
>U kunt deze kolommen in de toekomst altijd weer synchroniseren. Als u de synchronisatie van een kolom opheft, worden alle gegevens uit uw Data Warehouse verwijderd. Dit betekent alleen dat deze kolom tijdens de updatecyclus niet wordt gecontroleerd op nieuwe of bijgewerkte waarden.

**om een Kolom (of Kolommen) uit te synchroniseren**

1. Ga naar **[!DNL Manage Data]** en vervolgens naar **[!UICONTROL Data Warehouse]** .
1. Navigeer in de lijst **[!UICONTROL Synced Tables]** naar de tabel die de kolom bevat.
1. Schakel een of meer vakken in naast een of meer kolommen die u niet wilt synchroniseren.
   >[!NOTE]
   >
   >U kunt de synchronisatie van een kolom Primaire sleutel niet ongedaan maken zonder de volledige tabel neer te zetten.

1. Klik op **[!UICONTROL Remove]** om de synchronisatie van een of meer kolommen ongedaan te maken.

Hier is een blik op het hele proces:

![](../../mbi/assets/drop_column.png)

## Omloop

Uw [!DNL Commerce Intelligence] -account moet nu overzichtelijker en gemakkelijker door u en uw team te navigeren zijn.
