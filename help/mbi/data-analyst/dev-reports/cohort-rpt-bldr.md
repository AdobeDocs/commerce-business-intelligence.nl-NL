---
title: Cohort Report Builder
description: Leer over de analyse van gebruikersgroepen die gelijkaardige kenmerken over hun levenscycli delen.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Cohort Report Builder

Hebt u ooit willen onderzoeken hoe verschillende subsets van uw gebruikers zich in de loop der tijd gedragen? Bijvoorbeeld, vroeg ooit zich af of de gebruikers die tijdens een bevorderingsperiode registreren een hogere gemiddelde levensinkomsten hebben dan zij die niet? Als het antwoord `Yes`en de `Cohort Report Builder` is het perfecte gereedschap voor je. [!DNL MBI] is specifiek geoptimaliseerd om deze analyse uit te voeren en het relevant voor uw zaken te maken.

## Wat is cohortanalyse? {#what}

`Cohort` de analyse kan globaal worden gedefinieerd als de analyse van gebruikersgroepen die gedurende hun levenscyclus vergelijkbare kenmerken delen . Hiermee kunt u gedragstrends in verschillende gebruikersgroepen identificeren.

Voor een diepgaandere primer ingeschakeld `cohort` analyse, [kijk hier](https://www.cohortanalysis.com/) - we hebben de site erop geschreven!

In uw [!DNL MBI] dashboard, is het gemakkelijk om gebruiker tot stand te brengen `cohorts` op basis van een `cohort` datum en een metrische waarde in uw account.

## Waarom is cohortanalyse belangrijk? {#important}

Zoals hierboven vermeld, `cohort` Met een analyse kunt u gedragstrends onder verschillende gebruikersgroepen vaststellen. Met een goed begrip van hoe bepaalde groepen zich gedragen, kunt u uw besluiten en uitgaven aanpassen om uw verkoop te maximaliseren. Neem bijvoorbeeld levenslange inkomsten `cohort` analyse - hoewel dit soort analyse om vele redenen nuttig is , is de belangrijkste een betere beslissing over de verwerving van klanten .

## Hoe maak ik mijn eigen `cohort` analyse?

### Nieuwe architectuur

Dit zijn de instructies voor het gebruik van de `Cohort Report Builder` op de [Nieuwe architectuur](../../administrator/account-management/new-architecture.md).

1. Klikken **[!UICONTROL Report Builder]** op de linkertab of **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. In de `Report Builder` selectiescherm, klikken **[!UICONTROL Create Report]** naast de `Visual Report Builder` optie.

**Een metrisch object toevoegen**

Nu bevinden we ons in de `Report Builder`, voegen wij metrisch toe dat wij de analyse op (voorbeeld willen uitvoeren: `Revenue` of `Orders`).

>[!NOTE]
>
>Oorspronkelijk [!DNL Google Analytics] metriek is niet compatibel met de `Cohort Report Builder`.

**De metrische weergave in-/uitschakelen`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Dit opent een nieuw venster waar wij de details van kunnen vormen `Cohort` Rapport.

### Er zijn vijf specificaties nodig om een `Cohort` rapport:

1. Hoe groepeert u de `cohorts`
1. De `cohort` tijdsperiode
1. Het aantal `cohorts` om weer te geven
1. De minimale hoeveelheid gegevens elk `cohort` moet bevatten
1. Tijdbereik na `cohort` voorkomen

#### 1. Groepering `cohorts`

`Cohorts` worden gegroepeerd met een tijdstempel, zoals **registratiedatum** of **eerste besteldatum**.

>[!NOTE]
>
>U kunt niet het zelfde timestamp gebruiken dat metrisch voor metrisch wordt voortgebouwd `cohort` datum. Voor een analyse die dit vereist, kunt u gebruiken `Standard report builder` in plaats daarvan.

#### 2. `Cohort` tijdsperiode

Kies de periode die u wilt groeperen `cohorts` uiterlijk. Met andere woorden, welk deel van de tijdstempel die u hierboven hebt geselecteerd, is het belangrijkst; de `week`, `month`, `quarter`, of `year`?  Uw rapport zal gegevens in om het even welk interval tonen u hier selecteert

#### 3. en 4. Aantal instellen `cohorts` om te bekijken en hoeveel gegevens elk `cohort` moeten

Met deze parameters kunt u alleen de `cohorts` dat je geïnteresseerd bent, en de handigheid `Preview` onder aan het venster ziet u precies welke cohorten in uw rapport worden weergegeven.

Standaard wordt de huidige `cohort` wordt alleen opgenomen als u de minimale hoeveelheid gegevens wijzigt die voor elke `cohort` tot `0`. In dit geval worden de `cohort` voor de huidige periode zullen slechts gedeeltelijke gegevens worden opgenomen .

#### 5. Tijdbereik na `Cohort` Voorval

Met deze functie kunt u het tijdbereik instellen van de gegevens die u voor de geselecteerde `cohorts`. Als u bijvoorbeeld 24 maanden wilt weergeven `cohorts` gebaseerd op `customer's first order date`, maar u bent alleen geïnteresseerd in de eerste drie maanden van gegevens voor elke `cohort`kunt u de `number of cohorts to view` tot `24` en de `time range after cohort occurrence` tot `3`.

Het interval voor deze waarde verandert met wat u in het dialoogvenster `cohort time period` en de waarde is ingesteld op `12` door wanbetaling; De waarde wordt alleen gewijzigd als u op het kalenderpictogram klikt om de waarde te bewerken.

![](../../assets/cohort-time-range.png)

#### Overige opmerkingen

* [!UICONTROL Filters]: toegepast op uw metriek blijft intact wanneer u schakelt tussen `Standard` en `Cohort` weergaven.

* Zie [`Perspectives`](#perspectives).

#### Voorbeeld

Hier is een voorbeeld om het allemaal samen te trekken. In dit voorbeeld wil ik het gedrag van de bestelling uitchecken na een `cohort`We kopen voor het eerst om te zien of die cohort terugkomt om in de komende zes maanden herhaalde aankopen te doen.

![Orders, cohort](../../assets/crb_example.gif)

### Verouderde architectuur

#### Verouderde architectuur {#personalinfo}

Hieronder vindt u instructies die specifiek zijn voor de oudere versie van het `Cohort Report Builder`. Als u geïnteresseerd bent in het gebruik van de nieuwe versie, raadpleegt u [Nieuwe architectuur](../../administrator/account-management/new-architecture.md) voor meer informatie over migreren naar een [!DNL MBI] Nieuw architectuuraccount.

#### Hoe maak ik mijn eigen `cohort` analyse? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` analyse in actie! Hier kunnen we zien dat de inkomsten in de loop der tijd toenemen op cumulatieve basis en per gebruiker.

In deze sectie doorlopen we uw eigen creatie `cohort` analyse. Kijk bijvoorbeeld naar de [Voorbeelden, sectie](#examples) van dit artikel.

1. Klikken **[!UICONTROL Report Builder]** op de linkertab of **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. In de `Report Builder Selection` scherm, klikken **[!UICONTROL Create Report]** naast de `Cohort Analysis` optie.

#### Metrisch toevoegen

Nu bevinden we ons in de `Cohort Report Builder`, Laten we de metrische waarde toevoegen (voorbeeld: `Revenue` of `Number of orders`) dat wij de analyse willen uitvoeren.

>[!NOTE]
>
>Oorspronkelijk [!DNL Google Analytics] metriek is niet compatibel met de `Cohort Report Builder`.

#### De cohortdatum selecteren {#date}

De volgende stap bestaat uit het opgeven van de `cohort date`. Dit is de datum waarop de gebruikers worden gegroepeerd. Dit kan bijvoorbeeld `User's first order date` of `User's registration date`.

>[!NOTE]
>
>U kunt niet de zelfde datum gebruiken metrisch wordt gebouwd (voorbeeld: `created at`) als de `cohort date`.

#### Het instellen van het interval en de tijdsperiode

Vervolgens stellen we de `Interval` en `Time Period`.

`Interval`
De `Interval` kunt u de `length` van uw `cohorts`. Als deze bijvoorbeeld is ingesteld op `Month`, wordt uw rapport in maanden gemeten.

U kunt de weergave van deze intervallen op de x-as wijzigen met de **Duur** -menu.

`Time Period`
Gebruik de `Time Period` menu om de specifieke gebruiker te kiezen `cohorts` om te analyseren. U kunt elke `cohort`, kiest u uit een lijst, geeft u een tijdbereik op of definieert u een schuiftijdbereik van `cohorts` op te nemen. Als we bijvoorbeeld de `Specific Cohorts` wij kunnen specifieke maanden selecteren om in de analyse op te nemen :

![Met de `Time Period` menu om specifiek toe te voegen `Cohorts`](../../assets/Cohort_Time_Period.gif)

Als we onze `cohorts` op registratiedatum en vervolgens in april, mei en juni in het `Specific Cohorts` lijst worden alle gebruikers die zich in die maanden hebben ingeschreven, opgenomen.

#### De X-as definiëren

Onder `duration`kunt u de instellingen voor de X-as van het diagram definiëren. Dat wil zeggen, hoeveel tijdsperiodes elk gegevenspunt vertegenwoordigt en hoeveel gegevenspunten in de analyse moeten worden opgenomen.

#### Het selecteren van `counting members` table

Als u ervoor hebt gekozen om gebruikers te groeperen met een `cohort date` die van een andere lijst is aangesloten, kunt u zien `counting members in the … table` optie.

![](../../assets/Cohort_Counting_Members_option.png)

Laten we naar een voorbeeld kijken om deze instelling te begrijpen. Stel dat u een rapport hebt gemaakt waarin een `Revenue` metrisch volgens `Customer's registration date`. U wilde ook het perspectief gebruiken `Average value per cohort member` om de inkomsten per koper in de loop van de tijd te zien. Om de gemiddelde waarde per koper te vinden, moeten we bepalen door hoeveel kopers we het delen. Is het het aantal geregistreerde klanten in uw `customers` of is het het aantal afzonderlijke kopers in je `orders table` voor dezelfde periode?

Deze instelling beantwoordt die vraag. Leden tellen in de `customers` de tabel omvat het gemiddelde van alle klanten ( ongeacht of zij een aankoop hebben gedaan of niet ) . Leden tellen in de `orders` de tabel omvat alleen klanten die een aankoop hebben gedaan .

#### Perspectief selecteren {#perspective}

Nadat u metrisch hebt bepaald en hoe u het wilt analyseren, kunt u selecteren `perspective` wilt gebruiken.

Net boven het rapport is visualisatie een uitval van `perspective` instellingen.

Zie [Perspectieven](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Voorbeelden van cohortanalyse {#examples}

Nu hebben we doorlopen hoe we een `cohort` analyse , laten we enkele voorbeelden bekijken .

### Ik wil weten hoe mijn gebruiker `cohorts` groeien in de loop der tijd.

![Gebruiker `cohorts` groeien in de tijd](../../assets/cohort1.gif)

In dit voorbeeld analyseerden we de `Revenue` metrisch, gegroepeerd onze cohorten door `customer's first order date`en selecteert u de 8 meest recente `cohorts` (gedefinieerd in de `Time Period` ) die in de analyse moet worden opgenomen. Om te zien hoe de cohorten in de loop der tijd groeiden, gebruikten we de `Cumulative Average Value per Cohort Member` `perspective`.

### Ik wil gemiddeld weten hoeveel bestellingen een gebruiker maakt op verschillende punten in zijn leven.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif

In dit voorbeeld hebben we de `Number of orders` metrisch, gegroepeerd onze cohorten door `customer's first order date`en bevat de 8 meest recente cohorten (gedefinieerd in de `Time Period` ) in de analyse. Om het gemiddelde aantal orders voor elke cohort te zien, veranderden wij `perspective` tot `Average Value per Cohort Member`.

### Ik wil begrijpen hoe de toekomstige aankoopactiviteit van een gebruiker met zijn eerste maandactiviteit met de zaken vergelijkt.

![De toekomstige aankoopactiviteiten van een gebruiker vergelijken met de eerste maand van de activiteit](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Hieruit blijkt de incrementele bijdrage van een bepaalde cohortgroep op een bepaald punt in hun levenscyclus. (voorbeeld: Met het punt &quot;Week 6&quot; worden alle gegevenspunten weergegeven die gebruikers in hun zesde week hebben aangegeven.)

`Average Value per Cohort Member`
Hiermee verdeelt u de `Standard cohort` analyse in (1) door het aantal gebruikers in elke `cohort` groep. Dit kan handig zijn voor het vergelijken van cohortprestaties op appelbasis, aangezien niet alle cohortgroepen hetzelfde aantal gebruikers kunnen bevatten. Bijvoorbeeld de gemiddelde opbrengst van week 6 per gebruiker van een bepaalde `cohort`.

`Cumulative`
Dit `perspective` toont de traditionele `cohort` analyse van een `cumulative` basis. Met andere woorden, het toont de totale bijdrage van een bepaalde cohort tot op heden op een bepaald punt in hun levenscyclus. Bijvoorbeeld, de cumulatieve opbrengst na zes weken van gebruikers van een bepaalde cohort.

`Cumulative Average Value per Cohort Member`
Hiermee verdeelt u de `Cumulative` analyse in (3) door het aantal gebruikers in elke `cohort` groep. Het toont de gemiddelde levensduurbijdrage (vaak gemiddelde levensinkomsten) per `cohort` lid op elke periode in de `cohort's` leven. Bijvoorbeeld, de gemiddelde levensinkomsten na zes maanden van gebruikers die in Juni toetraden.

`Percent of First Value (show first value)`
Hiermee wordt het aggregaat geanalyseerd `cohort` bijdrage op een specifiek tijdstip in een `cohort's` levenscyclus als percentage van hun bijdrage in de eerste periode. Bijvoorbeeld, maand 6 opbrengst gedeeld door maand 1 inkomsten van gebruikers die zich in juni aansloten.

`Percent of First Value (hide first value)`
Dit is hetzelfde als `perspective` hierboven, behalve dat de waarde voor de eerste tijdsperiode van 100% verborgen is.

## Omloop {#finish}

De `Cohort Report Builder` is momenteel geoptimaliseerd voor het groeperen van gebruikers door een algemene `cohort date`. Misschien wilt u de gebruikers groeperen op basis van een vergelijkbare activiteit of kenmerk. Als dat het geval is, willen we u graag helpen! We raden aan om uit te checken [deze zelfstudie over kwalitatieve cohorten](../dev-reports/create-qual-cohort-analysis.md) om aan de slag te gaan.
