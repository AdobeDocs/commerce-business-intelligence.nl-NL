---
title: Cohort Report Builder
description: Leer over de analyse van gebruikersgroepen die gelijkaardige kenmerken over hun levenscycli delen.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Cohort Report Builder

Hebt u ooit willen onderzoeken hoe verschillende subsets van uw gebruikers zich in de loop der tijd gedragen? Bijvoorbeeld, vroeg ooit zich af of de gebruikers die tijdens een bevorderingsperiode registreren een hogere gemiddelde levensinkomsten hebben dan zij die niet? Als het antwoord `Yes` is, dan is `Cohort Report Builder` het perfecte hulpmiddel voor u. [!DNL Adobe Commerce Intelligence] is geoptimaliseerd voor het uitvoeren van deze analyse en het relevant maken voor uw bedrijf.

## Wat is cohortanalyse? {#what}

`Cohort` -analyse kan globaal worden gedefinieerd als de analyse van gebruikersgroepen die vergelijkbare kenmerken gedurende hun levenscyclus delen. Hiermee kunt u gedragstrends in verschillende gebruikersgroepen identificeren.

Voor een diepgaande primer op `cohort` analyse, herzie [ deze pagina ](https://www.cohortanalysis.com/).

In uw [!DNL Commerce Intelligence] dashboard is het eenvoudig om gebruiker `cohorts` te maken op basis van een `cohort` -datum en een metrische waarde in uw account.

## Waarom is cohortanalyse belangrijk? {#important}

Zoals hierboven vermeld, kunt u met `cohort` -analyse gedragstrends onder verschillende gebruikersgroepen identificeren. Met een goed begrip van hoe bepaalde groepen zich gedragen, kunt u uw besluiten en uitgaven aanpassen om uw verkoop te maximaliseren. Neem bijvoorbeeld een levenslange inkomstenanalyse `cohort` - hoewel dit soort analyse om vele redenen nuttig is, is de directe die betere besluiten van de klantenverwerving zijn.

## Hoe maak ik mijn eigen `cohort` analyse?

### Nieuwe architectuur

Dit zijn de instructies om `Cohort Report Builder` op de [ Nieuwe Architectuur ](../../administrator/account-management/new-architecture.md) te gebruiken.

1. Klik op **[!UICONTROL Report Builder]** op het linkertabblad of op **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. Klik in het selectiescherm van `Report Builder` op **[!UICONTROL Create Report]** naast de optie `Visual Report Builder` .

**Toevoegend metrisch**

Nu u zich in `Report Builder` bevindt, voegt u de metrische waarde toe waarop u de analyse wilt uitvoeren (bijvoorbeeld: `Revenue` of `Orders`).

>[!NOTE]
>
>Eigen [!DNL Google Analytics] metriek zijn niet compatibel met `Cohort Report Builder` .

**Knevel de Metrische Mening aan`Cohort`**

![ Visuele Report Builder die de kneveloptie van de de kleurenanalyse tonen ](../../assets/visual-report-builder-cohort-toggle.png)

Hiermee wordt een nieuw venster geopend waarin de details van het `Cohort` -rapport worden geconfigureerd.

### Voor het samenstellen van een `Cohort` -rapport zijn vijf specificaties nodig:

1. Hoe te om `cohorts` te groeperen
1. De `cohort` tijdsperiode
1. Het aantal `cohorts` dat moet worden weergegeven
1. De minimale hoeveelheid gegevens die elke `cohort` moet bevatten
1. Tijdbereik na `cohort` voorkomen

#### &#x200B;1. Groeperen `cohorts`

`Cohorts` wordt gegroepeerd door een timestamp, als **registratiedatum** of **eerste ordedatum**.

>[!NOTE]
>
>U kunt niet dezelfde tijdstempel gebruiken als de metrische waarde voor de datum `cohort` is gebruikt. Voor een analyse die dit vereist, kunt u `Standard report builder` in plaats daarvan gebruiken.

#### &#x200B;2. `Cohort` tijdsperiode

Kies de periode waarop u `cohorts` wilt groeperen. Met andere woorden, welk deel van de tijdstempel dat u hierboven hebt geselecteerd, is het belangrijkst. De waarden `week`, `month`, `quarter` of `year` ? Uw rapport toont gegevens in om het even welk interval dat u hier selecteert

#### &#x200B;3. en 4. Stel het aantal `cohorts` in dat moet worden weergegeven en het aantal gegevens dat elke `cohort` moet hebben

Met deze parameters kunt u alleen de `cohorts` bekijken waarin u bent geïnteresseerd. Met het handige vak `Preview` onder aan het venster kunt u precies zien wat de cohorten in uw rapport weergeven.

Standaard wordt de huidige `cohort` niet opgenomen, tenzij u de minimale hoeveelheid gegevens wijzigt die voor elke `cohort` wordt vereist naar `0` . In dit geval bevat de `cohort` voor de huidige periode alleen gedeeltelijke gegevens.

#### &#x200B;5. Tijdbereik na `Cohort` voorkomen

Met deze functie kunt u het tijdbereik instellen van gegevens die u voor de geselecteerde `cohorts` bekijkt. Als u bijvoorbeeld 24 maanden `cohorts` wilt weergeven op basis van `customer's first order date` , maar u alleen geïnteresseerd bent in de eerste 3 maanden van gegevens voor elke `cohort` , kunt u de `number of cohorts to view` op `24` en de `time range after cohort occurrence` op `3` instellen.

Het interval voor deze waarde verandert met wat u in `cohort time period` hebt geselecteerd en de waarde wordt standaard ingesteld op `12` . De waarde verandert alleen als u op het kalenderpictogram klikt om deze te bewerken.

![ de selecteur van de tijdwaaier van de Cohort die datumopties toont ](../../assets/cohort-time-range.png)

#### Overige opmerkingen

* [!UICONTROL Filters] : toegepast op uw metriek blijft intact wanneer u schakelt tussen de weergaven `Standard` en `Cohort` .

* Zie [`Perspectives`](#perspectives) .

#### Voorbeeld

Hier is een voorbeeld om het allemaal samen te trekken. In dit voorbeeld wil ik het gedrag van bestellingen uitchecken na de eerste aankoop van een `cohort` om te zien of die cohort terugkomt om in de komende zes maanden herhaalde aankopen te doen.

![ de cohort van Orden ](../../assets/crb_example.gif)

### Verouderde architectuur

#### Verouderde architectuur {#personalinfo}

Hieronder vindt u instructies die specifiek zijn voor de oudere versie van de `Cohort Report Builder` . Als u in het gebruiken van de nieuwe versie geinteresseerd bent, zie [ Nieuwe Architectuur ](../../administrator/account-management/new-architecture.md) voor meer informatie over het migreren aan een [!DNL Commerce Intelligence] Nieuwe rekening van de Architectuur.

#### Hoe maak ik mijn eigen `cohort` analyse? {#create}

![ creeer de dialoog van de kleurenanalyse met configuratieopties ](../../assets/create-cohort-analysis.png)

`Cohort` analyse in actie! Hier zie je dat de omzet in de loop der tijd toeneemt, op cumulatieve basis en per gebruiker.

In deze sectie wordt u door het maken van uw eigen `cohort` -analyse geleid. Voor voorbeelden (en geanimeerde GIFs die het proces aantonen), bekijk de [ sectie van Voorbeelden ](#examples) van dit onderwerp.

1. Klik op **[!UICONTROL Report Builder]** op het linkertabblad of op **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. Klik in het `Report Builder Selection` -scherm op **[!UICONTROL Create Report]** naast de optie `Cohort Analysis` .

#### Metrisch toevoegen

Nu u zich in `Cohort Report Builder` bevindt, voegt u de metrische waarde (bijvoorbeeld: `Revenue` of `Number of orders` ) toe waarop u de analyse wilt uitvoeren.

>[!NOTE]
>
>Eigen [!DNL Google Analytics] metriek zijn niet compatibel met `Cohort Report Builder` .

#### De cohortdatum selecteren {#date}

De volgende stap bestaat uit het opgeven van de `cohort date` . Dit is de datum waarop de gebruikers zijn gegroepeerd. Dit kan bijvoorbeeld `User's first order date` of `User's registration date` zijn.

>[!NOTE]
>
>U kunt niet dezelfde datum gebruiken waarop de metrische waarde is gebaseerd (bijvoorbeeld: `created at`) als de `cohort date` .

#### Het bepalen van het interval en de tijdspanne

Stel vervolgens de opties `Interval` en `Time Period` in.

`Interval`
Met de optie `Interval` kunt u de `length` van de `cohorts` -component instellen. Als deze bijvoorbeeld is ingesteld op `Month` , wordt uw rapport gemeten in maanden.

U kunt veranderen hoe deze intervallen op de x-as gebruikend het **menu van de Duur** worden getoond.

`Time Period`
Kies in het menu `Time Period` de specifieke gebruiker die u wilt analyseren. `cohorts` U kunt elke `cohort` weergeven, een keuze maken in een lijst, een tijdbereik opgeven of een schuiftijdbereik van `cohorts` definiëren om op te nemen. Als u bijvoorbeeld de optie `Specific Cohorts` hebt gebruikt, kunt u specifieke maanden selecteren om in de analyse op te nemen:

![ Specifiek toevoegen via het menu `Time Period` `Cohorts`](../../assets/Cohort_Time_Period.gif)

Als u `cohorts` groepeert op registratiedatum en vervolgens april, mei en juni in de `Specific Cohorts` -lijst selecteert, worden alle gebruikers opgenomen die zich in die maanden hebben geregistreerd.

#### De X-as definiëren

Onder `duration` kunt u de instellingen voor de X-as van het diagram definiëren. Dat wil zeggen, hoeveel tijdsperiodes elk gegevenspunt vertegenwoordigt en hoeveel gegevenspunten in de analyse moeten worden opgenomen.

#### De tabel `counting members` selecteren

Als u ervoor hebt gekozen om gebruikers te groeperen met een `cohort date` die vanuit een andere tabel is gekoppeld, wordt mogelijk een `counting members in the … table` -optie weergegeven.

![ de tellende van de Cohort ledenoptie die onafhankelijke versus cumulatieve wijzen tonen ](../../assets/Cohort_Counting_Members_option.png)

Bekijk een voorbeeld om deze instelling te begrijpen. Stel dat u een rapport hebt gemaakt waarin een `Revenue` metrisch op `Customer's registration date` wordt geconverteerd. Je wilde ook het perspectief `Average value per cohort member` gebruiken om de opbrengst per koper in de loop van de tijd te zien. Als je de gemiddelde waarde per koper wilt vinden, moet je bepalen door hoeveel kopers je wilt delen. Is het het aantal geregistreerde klanten in uw `customers` lijst, of is het het aantal verschillende kopers in uw `orders table` voor de zelfde periode?

Deze instelling beantwoordt die vraag. Bij het tellen van leden in de tabel `customers` worden gemiddeld alle klanten (ongeacht of ze een aankoop hebben gedaan, ooit) vermeld. Telende leden in de tabel `orders` bevatten alleen klanten die een aankoop hebben gedaan.

#### Perspectief selecteren {#perspective}

Nadat u de metrische waarde hebt gedefinieerd en wilt analyseren, kunt u de `perspective` selecteren die u wilt gebruiken.

Net boven de rapportvisualisatie bevindt zich een vervolgkeuzelijst met `perspective` -instellingen.

Zie [ Perspectieven ](#perspectives).

![ het perspectiefmenu van de Cohort dat verschillende meningsopties toont ](../../assets/Cohort_Perspective_Menu.png)

## Voorbeelden van cohortanalyse {#examples}

Nu u door hebt gegaan hoe te om een `cohort` analyse tot stand te brengen, bekijk sommige voorbeelden.

### Ik wil weten hoe mijn gebruiker `cohorts` in de loop der tijd groeit.

![ Gebruiker `cohorts` groeiend in tijd ](../../assets/cohort1.gif)

In dit voorbeeld hebt u de `Revenue` -metrische waarde geanalyseerd, de cohorten gegroepeerd op `customer's first order date` en de 8 meest recente `cohorts` kleur geselecteerd (gedefinieerd in het menu `Time Period` ) die u in de analyse wilt opnemen. Om te zien hoe de cohorten in de loop der tijd groeiden, gebruikte u `Cumulative Average Value per Cohort Member` `perspective`.

### Ik wil gemiddeld weten hoeveel bestellingen een gebruiker maakt op verschillende punten in zijn leven.

(../../assets/cohort2.gif

In dit voorbeeld hebt u de `Number of orders` -meting geanalyseerd, de cohorten gegroepeerd op `customer's first order date` en de acht meest recente cohorts (gedefinieerd in het menu `Time Period` ) opgenomen in de analyse. Als u het gemiddelde aantal bestellingen voor elke cohort wilt zien, hebt u de opdracht `perspective` gewijzigd in `Average Value per Cohort Member` .

### Ik wil begrijpen hoe de toekomstige aankoopactiviteit van een gebruiker met zijn eerste maandactiviteit met de zaken vergelijkt.

![ Vergelijkend de toekomstige het kopen van een gebruiker activiteit aan hun eerste maand van activiteit ](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Dit toont de incrementele bijdrage van een bepaalde cohortgroep op een bepaald punt in hun levenscyclus. (Voorbeeld: het punt &quot;Week 6&quot; geeft alle gegevenspunten weer die gebruikers in hun zesde week hebben aangegeven.)

`Average Value per Cohort Member`
Hiermee wordt de `Standard cohort` analyse in (1) gedeeld door het aantal gebruikers in elke `cohort` -groep. Dit kan handig zijn voor het vergelijken van cohortprestaties op appelbasis, aangezien niet alle cohortgroepen hetzelfde aantal gebruikers kunnen bevatten. Bijvoorbeeld, de gemiddelde opbrengst van week 6 per gebruiker van bepaalde `cohort`.

`Cumulative`
Deze `perspective` toont de traditionele `cohort` analyse op `cumulative` basis. Met andere woorden, het toont de totale bijdrage van een bepaalde cohort tot op heden op een bepaald punt in hun levenscyclus. Bijvoorbeeld, de cumulatieve opbrengst na zes weken van gebruikers van een bepaalde cohort.

`Cumulative Average Value per Cohort Member`
Hiermee wordt de `Cumulative` analyse in (3) gedeeld door het aantal gebruikers in elke `cohort` -groep. Het toont de gemiddelde levenbijdrage (vaak gemiddelde levensinkomsten) per `cohort` lid bij elke periode in het `cohort's` leven. Bijvoorbeeld, de gemiddelde levensinkomsten na zes maanden van gebruikers die in Juni toetraden.

`Percent of First Value (show first value)`
Hiermee wordt de totale `cohort` bijdrage op een specifiek tijdstip in een `cohort's` levenscyclus geanalyseerd als percentage van hun bijdrage in de eerste periode. Bijvoorbeeld, maand 6 opbrengst gedeeld door maand 1 inkomsten van gebruikers die zich in juni aansloten.

`Percent of First Value (hide first value)`
Dit is hetzelfde als de bovenstaande `perspective` , behalve dat de waarde voor de eerste tijdsperiode van 100% verborgen is.

## Omloop {#finish}

`Cohort Report Builder` is geoptimaliseerd voor het groeperen van gebruikers door een gemeenschappelijke `cohort date`. U bent wellicht geïnteresseerd in het groeperen van de gebruikers op basis van een vergelijkbare activiteit of een vergelijkbaar kenmerk. Adobe adviseert het controleren van [ dit leerprogramma op kwalitatieve cohorts ](../dev-reports/create-qual-cohort-analysis.md) om begonnen te worden.
