---
title: Ontdek uw [!DNL Commerce Intelligence] Account
description: Leer hoe u uw [!DNL Commerce Intelligence] account.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Maak uw [!DNL Adobe Commerce Intelligence] Account

Of u met bent geweest [!DNL Commerce Intelligence] gedurende zes maanden of zes jaar is het bijhouden van een proefaccount van het grootste belang voor uw organisatie die het beste uit het platform haalt . In tijd, is het natuurlijk voor er gebruikers, dashboards, rapporten, metriek, en kolommen zijn die niet meer nodig zijn. Mogelijk hebt u een rapport gemaakt voor eenmalig gebruik en bent u vergeten of heeft een gebruiker die uw bedrijf heeft verlaten, zijn account nooit gedeactiveerd.

Met [gestandaardiseerde, duidelijke naamgeving voor alle elementen](../best-practices/naming-elements.md)) van uw [!DNL Commerce Intelligence] met de onderstaande stappen voor accountcontrole kunt u de rommelige en onnodige analyses voor uw gebruikers verminderen. Eén extra voordeel omvat [potentieel snellere updatecycli](../best-practices/reduce-update-cycle-time.md).

## Stap 1: Identificeer uw niet-actieve gebruikers

De eerste stap bij het opschonen van uw account is het deactiveren van de accounts van niet-actieve gebruikers, zoals mensen die het bedrijf hebben verlaten of die niet meer gebruiken [!DNL Commerce Intelligence] in hun huidige rollen.

Om dit te doen - klik de naam van uw bedrijf in de hoger-juiste navigatiebar, dan selecteren **[!UICONTROL Manage Users]**. Selecteer vervolgens de gebruiker die u wilt deactiveren en klik op **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>U hebt [Beheerdersmachtigingen](../administrator/user-management/user-management.md) om dit te doen.

>[!WARNING]
>
>Als u een gebruiker deactiveert, verwijdert u de diagrammen, dashboards en andere elementen die door die gebruiker zijn gemaakt. Als u deze elementen wilt behouden, neemt u contact op met [!DNL Commerce Intelligence] [ondersteuning](../guide-overview.md#Submitting-a-Support-Ticket) team voordat u de gebruiker deactiveert. Ondersteuning kan u helpen deze middelen over te brengen naar een andere gebruiker.

### Gebruiker opnieuw activeren

Als u een gebruiker opnieuw wilt activeren, nodigt u de gebruiker opnieuw uit door zijn account opnieuw te maken met hetzelfde e-mailadres dat is gedeactiveerd, en de toegang tot de gebruiker en de gegevens die hij of zij bezat, worden bij de aanmelding hersteld.

## Stap 2: Ongebruikte dashboards en rapporten verwijderen

De volgende stap bij het controleren van uw account is het verwijderen van ongebruikte dashboards en rapporten.

>[!NOTE]
>
>U hebt `Admin` of `Standard` [gebruikersmachtigingen](../administrator/user-management/user-management.md) om dit te doen.

Elke gebruiker met `Admin` of `Standard` de toegang kan rapporten en dashboards tot stand brengen. Daarom moet iedereen met deze machtigingen de onderstaande stappen volgen om ongebruikte rapporten te identificeren en te verwijderen.

### Controleer uw dashboards en rapporten

Voordat u iets verwijdert, moet u eerst uw rapporten en dashboards bekijken om te beoordelen wat er in gebruik is. Terwijl u **[!UICONTROL find unused reports]** met de hieronder beschreven functie maakt een eerste revisie uw opschoningsinspanningen veel productiever.

### Dashboards en rapporten verwijderen

Nadat u toegang hebt tot uw dashboards en rapporten, kunt u beginnen uw rekening op te schonen.

**Een rapport verwijderen van een dashboard**

1. Zoek het rapport dat u op het dashboard wilt verwijderen.
1. Selecteren **[!UICONTROL Options]** in de rechterbovenhoek van het rapport.
1. Klik op **[!UICONTROL Remove From Dashboard]**.

**Een volledig dashboard verwijderen**

1. Selecteren **[!UICONTROL Manage Data]**, dan **[!UICONTROL Dashboards**].
1. Klik op het dashboard dat u wilt verwijderen.
1. Klik op **[!UICONTROL Delete Dashboard]**.

U kunt ook **[!UICONTROL Dashboard Options]** vervolgens **[!UICONTROL Delete]** van het dashboard zelf.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>Als u een dashboard verwijdert, worden de rapporten in het dashboard niet verwijderd. U moet dus nog een stap ondernemen om de rapporten te verwijderen.

**Ongebruikte rapporten verwijderen**

1. Selecteren **[!UICONTROL Manage Data]** vervolgens **[!UICONTROL Reports]**.
1. Controleer de **Alleen ongebruikte rapporten weergeven** onder de lijst Metriek. Hiermee maakt u een lijst met rapporten die niet worden gebruikt in een dashboard- of e-mailoverzicht.
1. Selecteer de rapporten die u wilt schrappen. U kunt alle selecteren door checkbox boven de rapportlijst te klikken.
1. Klik op **[!UICONTROL Delete Selected]**.

Hier is een blik op het ongebruikte proces van de rapportschrapping:

![](../../mbi/assets/unused_reports.png)

## Stap 3: Ongebruikte metriek verwijderen

Nadat u uw gebruikerslijst, dashboards, en rapporten hebt schoongemaakt, kunt u zich op controle van uw lijst van metriek bewegen. Dit helpt u om het even wat identificeren die verouderd zou kunnen zijn - bijvoorbeeld, werd nieuw metrisch gecreeerd met een verschillende definitie - of niet in gebruik.

1. Om een lijst van afhankelijke rapporten voor metrisch te produceren, ga **[!DNL Manage Data]** Selecteer vervolgens Klikken **[!UICONTROL Metrics]**.
1. Klikken **[!UICONTROL Edit]** naast een metrische waarde.
1. Onder aan de pagina ziet u een sectie met de naam **[!UICONTROL Dependent Charts]**. Klik de verbinding om een afhankelijke rapportlijst voor dit metrisch te produceren.
1. Nadat het systeem de controle heeft voltooid, [!DNL Commerce Intelligence] toont een lijst van dashboards, rapporten, en gebruikers die dit metrisch gebruiken.

![](../../mbi/assets/report_dependecies.png)

Als u besluit dat metrisch niet meer nodig is, ga terug naar **[!UICONTROL Metrics]** pagina door te klikken **[!UICONTROL Back to Metric List]** om metrisch te vinden u wilt schrappen. Klik op **[!UICONTROL Delete]**.

## Stap 4: De gesynchroniseerde kolommen beoordelen

De laatste stap is het beoordelen van de kolommen die momenteel in uw Data Warehouse worden gesynchroniseerd. U kunt niet alleen de synchronisatie van kolommen in uw account ongedaan maken, maar ook de updatetijd verminderen.

Als u dit wilt nastreven, richt u zich tot [!DNL Commerce Intelligence] [Ondersteuning](../guide-overview.md#Submitting-a-Support-Ticket). Het ondersteuningsteam kan een rapport maken dat alle kolommen bevat die in geen enkel dashboard voor een gebruiker worden gebruikt en die niet in e-mailoverzichten worden gebruikt, met uitzondering van SQL-rapporten. U kunt dit rapport dan gebruiken als richtlijn voor het selecteren van kolommen aan unsync via de Manager van de Data Warehouse.

>[!NOTE]
>
>U kunt deze kolommen in de toekomst altijd weer synchroniseren. Als u de synchronisatie van een kolom opheft, worden alle gegevens uit de Data Warehouse verwijderd. Dit betekent alleen dat deze kolom tijdens de updatecyclus niet wordt gecontroleerd op nieuwe of bijgewerkte waarden.

**De synchronisatie van een kolom (of kolommen) opheffen**

1. Ga naar **[!DNL Manage Data]** vervolgens **[!UICONTROL Data Warehouse]**.
1. In de **[!UICONTROL Synced Tables]** Blader naar de tabel die de kolom bevat.
1. Schakel een of meer vakken in naast een of meer kolommen die u niet wilt synchroniseren.
   >[!NOTE]
   >
   >U kunt de synchronisatie van een kolom Primaire sleutel niet ongedaan maken zonder de volledige tabel neer te zetten.

1. Klikken **[!UICONTROL Remove]** om de synchronisatie van een of meer kolommen ongedaan te maken.

Hier is een blik op het hele proces:

![](../../mbi/assets/drop_column.png)

## Omloop

Uw [!DNL Commerce Intelligence] De account moet nu overzichtelijker en eenvoudiger door u en uw team kunnen navigeren.
