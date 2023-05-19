---
title: Cohort Report Builder
description: Leer over de analyse van gebruikersgroepen die gelijkaardige kenmerken over hun levenscycli delen.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Cohort Report Builder

Hebt u ooit willen onderzoeken hoe verschillende subsets van uw gebruikers zich in de loop der tijd gedragen? Bijvoorbeeld, vroeg ooit zich af of de gebruikers die tijdens een bevorderingsperiode registreren een hogere gemiddelde levensinkomsten hebben dan zij die niet? Als het antwoord `Yes`en de `Cohort Report Builder` is het perfecte gereedschap voor je. [!DNL Adobe Commerce Intelligence] is geoptimaliseerd om deze analyse uit te voeren en deze relevant te maken voor uw bedrijf.

## Wat is cohortanalyse? {#what}

`Cohort` de analyse kan globaal worden gedefinieerd als de analyse van gebruikersgroepen die gedurende hun levenscyclus vergelijkbare kenmerken delen . Hiermee kunt u gedragstrends in verschillende gebruikersgroepen identificeren.

Voor een diepgaande primer ingeschakeld `cohort` analyse, herziening [deze pagina](https://www.cohortanalysis.com/).

In uw [!DNL Commerce Intelligence] dashboard, is het gemakkelijk om gebruiker tot stand te brengen `cohorts` op basis van een `cohort` datum en een metrische waarde in uw account.

## Waarom is cohortanalyse belangrijk? {#important}

Zoals hierboven vermeld, `cohort` Met een analyse kunt u gedragstrends onder verschillende gebruikersgroepen vaststellen. Met een goed begrip van hoe bepaalde groepen zich gedragen, kunt u uw besluiten en uitgaven aanpassen om uw verkoop te maximaliseren. Neem bijvoorbeeld levenslange inkomsten `cohort` analyse - hoewel dit soort analyse om vele redenen nuttig is , is de belangrijkste een betere beslissing over de verwerving van klanten .

## Hoe maak ik mijn eigen `cohort` analyse?

### Nieuwe architectuur

Dit zijn de instructies voor het gebruik van de `Cohort Report Builder` op de [Nieuwe architectuur](../../administrator/account-management/new-architecture.md).

1. Klikken **[!UICONTROL Report Builder]** op de linkertab of **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. In de `Report Builder` selectiescherm, klikken **[!UICONTROL Create Report]** naast de `Visual Report Builder` optie.

**Een metrisch object toevoegen**

Nu ben je in de `Report Builder`Voeg de metrische waarde toe waarop u de analyse wilt uitvoeren (voorbeeld: `Revenue` of `Orders`).

>[!NOTE]
>
>Oorspronkelijk [!DNL Google Analytics] metriek is niet compatibel met de `Cohort Report Builder`.

**De metrische weergave in-/uitschakelen`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Dit opent omhoog een nieuw venster om de details van te vormen `Cohort` Rapport.

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

Kies de periode die u wilt groeperen `cohorts` uiterlijk. Met andere woorden, welk deel van de tijdstempel die u hierboven hebt geselecteerd, is het belangrijkst; de `week`, `month`, `quarter`, of `year`? Uw rapport toont gegevens in om het even welk interval dat u hier selecteert

#### 3. en 4. Aantal instellen `cohorts` om te bekijken en hoeveel gegevens elk `cohort` moeten

Met deze parameters kunt u alleen de `cohorts` dat je geïnteresseerd bent, en de handigheid `Preview` onder aan het venster ziet u precies welke cohorten in uw rapport worden weergegeven.

Standaard wordt de huidige `cohort` is niet inbegrepen tenzij u de minimumhoeveelheid gegevens wijzigt die voor elk wordt vereist `cohort` tot `0`. In dit geval worden de `cohort` voor de huidige periode omvatten slechts gedeeltelijke gegevens.

#### 5. Tijdbereik na `Cohort` Voorval

Met deze functie kunt u het tijdbereik instellen van de gegevens die u voor de geselecteerde `cohorts`. Als u bijvoorbeeld 24 maanden wilt weergeven `cohorts` gebaseerd op `customer's first order date`, maar u bent alleen geïnteresseerd in de eerste drie maanden van gegevens voor elke `cohort`kunt u de `number of cohorts to view` tot `24` en de `time range after cohort occurrence` tot `3`.

Het interval voor deze waarde verandert met wat u in het dialoogvenster `cohort time period` en de waarde is ingesteld op `12` door wanbetaling; de waarde verandert alleen als u op het kalenderpictogram klikt om deze te bewerken.

![](../../assets/cohort-time-range.png)

#### Overige opmerkingen

* [!UICONTROL Filters]: toegepast op uw metriek blijven intact wanneer u schakelt tussen `Standard` en `Cohort` weergaven.

* Zie [`Perspectives`](#perspectives).

#### Voorbeeld

Hier is een voorbeeld om het allemaal samen te trekken. In dit voorbeeld wil ik het gedrag van de bestelling uitchecken na een `cohort`We kopen voor het eerst om te zien of die cohort terugkomt om in de komende zes maanden herhaalde aankopen te doen.

![Orders, cohort](../../assets/crb_example.gif)

### Verouderde architectuur

#### Verouderde architectuur {#personalinfo}

Hieronder vindt u instructies die specifiek zijn voor de oudere versie van het `Cohort Report Builder`. Als u geïnteresseerd bent in het gebruik van de nieuwe versie, raadpleegt u [Nieuwe architectuur](../../administrator/account-management/new-architecture.md) voor meer informatie over migreren naar een [!DNL Commerce Intelligence] Nieuw architectuuraccount.

#### Hoe maak ik mijn eigen `cohort` analyse? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` analyse in actie! Hier zie je dat de omzet in de loop der tijd toeneemt, op cumulatieve basis en per gebruiker.

Deze sectie begeleidt u door het creëren van uw eigen `cohort` analyse. Bekijk voor voorbeelden (en geanimeerde GIFFEN die het proces demonstreren) de [Voorbeelden, sectie](#examples) van dit onderwerp.

1. Klikken **[!UICONTROL Report Builder]** op de linkertab of **[!UICONTROL Add Report** > **Create Report]** in een dashboard.

1. In de `Report Builder Selection` scherm, klikken **[!UICONTROL Create Report]** naast de `Cohort Analysis` optie.

#### Metrisch toevoegen

Nu ben je in de `Cohort Report Builder`voegt u de metrische waarde toe (voorbeeld: `Revenue` of `Number of orders`) waarop u de analyse wilt uitvoeren.

>[!NOTE]
>
>Oorspronkelijk [!DNL Google Analytics] metriek is niet compatibel met de `Cohort Report Builder`.

#### De cohortdatum selecteren {#date}

De volgende stap bestaat uit het opgeven van de `cohort date`. Dit is de datum waarop de gebruikers zijn gegroepeerd. Dit kan bijvoorbeeld `User's first order date` of `User's registration date`.

>[!NOTE]
>
>U kunt niet de zelfde datum gebruiken metrisch wordt gebouwd (voorbeeld: `created at`) als de `cohort date`.

#### Het instellen van het interval en de tijdsperiode

Stel vervolgens de `Interval` en `Time Period`.

`Interval`
De `Interval` kunt u de `length` van uw `cohorts`. Als deze bijvoorbeeld is ingesteld op `Month`, uw rapport wordt gemeten in maanden.

U kunt de weergave van deze intervallen op de x-as wijzigen met de **Duur** -menu.

`Time Period`
Gebruik de `Time Period` menu om de specifieke gebruiker te kiezen `cohorts` om te analyseren. U kunt elke `cohort`, kiest u uit een lijst, geeft u een tijdbereik op of definieert u een schuiftijdbereik van `cohorts` op te nemen. Als u bijvoorbeeld de opdracht `Specific Cohorts` kunt u specifieke maanden selecteren om in de analyse op te nemen:

![Met de `Time Period` menu om specifiek toe te voegen `Cohorts`](../../assets/Cohort_Time_Period.gif)

Als u groepeert `cohorts` op registratiedatum en vervolgens in april, mei en juni in het `Specific Cohorts` lijst worden alle gebruikers die zich in die maanden hebben ingeschreven, opgenomen.

#### De X-as definiëren

Onder `duration`kunt u de instellingen voor de X-as van het diagram definiëren. Dat wil zeggen, hoeveel tijdsperiodes elk gegevenspunt vertegenwoordigt en hoeveel gegevenspunten in de analyse moeten worden opgenomen.

#### Het selecteren van `counting members` table

Als u ervoor hebt gekozen om gebruikers te groeperen met een `cohort date` die van een andere lijst is aangesloten, kunt u zien `counting members in the … table` optie.

![](../../assets/Cohort_Counting_Members_option.png)

Bekijk een voorbeeld om deze instelling te begrijpen. Stel dat u een rapport hebt gemaakt waarin een `Revenue` metrisch volgens `Customer's registration date`. U wilde ook het perspectief gebruiken `Average value per cohort member` om de inkomsten per koper in de loop van de tijd te zien. Als je de gemiddelde waarde per koper wilt vinden, moet je bepalen door hoeveel kopers je wilt delen. Is het het aantal geregistreerde klanten in uw `customers` of is het het aantal afzonderlijke kopers in je `orders table` voor dezelfde periode?

Deze instelling beantwoordt die vraag. Leden tellen in de `customers` de tabel bevat het gemiddelde voor alle klanten ( ongeacht of zij een aankoop hebben gedaan , ooit ) . Leden tellen in de `orders` de tabel omvat alleen klanten die een aankoop hebben gedaan .

#### Perspectief selecteren {#perspective}

Nadat u metrisch hebt bepaald en hoe u het wilt analyseren, kunt u selecteren `perspective` wilt gebruiken.

Net boven het rapport is visualisatie een uitval van `perspective` instellingen.

Zie [Perspectieven](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Voorbeelden van cohortanalyse {#examples}

Nu hebt u al geleerd hoe u een `cohort` analyse, bekijk sommige voorbeelden.

### Ik wil weten hoe mijn gebruiker `cohorts` groeien in de loop der tijd.

![Gebruiker `cohorts` groeien in de tijd](../../assets/cohort1.gif)

In dit voorbeeld hebt u de opdracht `Revenue` metrisch, groepeerde uw cohorts door `customer's first order date`en selecteert u de 8 meest recente `cohorts` (gedefinieerd in de `Time Period` ) die in de analyse moet worden opgenomen. Om te zien hoe de cohorten in de loop der tijd groeiden, gebruikte je de `Cumulative Average Value per Cohort Member` `perspective`.

### Ik wil gemiddeld weten hoeveel bestellingen een gebruiker maakt op verschillende punten in zijn leven.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif

In dit voorbeeld hebt u de `Number of orders` metrisch, groepeerde uw cohorts door `customer's first order date`en bevat de acht meest recente cohorten (gedefinieerd in de `Time Period` ) in de analyse. Als u het gemiddelde aantal bestellingen voor elke cohort wilt zien, hebt u de opdracht `perspective` tot `Average Value per Cohort Member`.

### Ik wil begrijpen hoe de toekomstige aankoopactiviteit van een gebruiker met zijn eerste maandactiviteit met de zaken vergelijkt.

![De toekomstige aankoopactiviteiten van een gebruiker vergelijken met de eerste maand van de activiteit](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Dit toont de incrementele bijdrage van een bepaalde cohortgroep op een bepaald punt in hun levenscyclus. (voorbeeld: Met het punt &quot;Week 6&quot; worden alle gegevenspunten weergegeven die gebruikers in hun zesde week hebben aangegeven.)

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

De `Cohort Report Builder` is geoptimaliseerd voor het groeperen van gebruikers op basis van een algemene `cohort date`. U bent wellicht geïnteresseerd in het groeperen van de gebruikers op basis van een vergelijkbare activiteit of een vergelijkbaar kenmerk. Adobe raadt aan om uit te checken [deze zelfstudie over kwalitatieve cohorten](../dev-reports/create-qual-cohort-analysis.md) om aan de slag te gaan.
