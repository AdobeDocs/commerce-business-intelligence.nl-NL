---
title: De visuele Report Builder gebruiken
description: Leer de gegevens in uw rapport gedurende een bepaalde periode te analyseren.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Gebruik de `Visual Report Builder`

De [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) kunt u uw gegevens visueel verkennen om inzichten te tekenen en zakelijke beslissingen te stimuleren. Dit leerprogramma begeleidt u door het proces om een basisrapport tot stand te brengen.

>[!NOTE]
>
>Als u een rapport aan een dashboard wilt toevoegen, moet u `Standard` [gebruikersmachtigingen](../administrator/user-management/user-management.md) en `Edit` toegang tot het dashboard.

## Stap 1: Een rapport maken

Als u een nieuw rapport wilt gaan maken, klikt u op **[!UICONTROL Report Builder]** op de zijbalk of **[!UICONTROL Add Report]** boven aan een dashboard. Wanneer de `Report Builder` op de selectiepagina worden weergegeven, klikt u op de **[!UICONTROL Visual Report Builder]** optie.

Als u een rapport wilt bewerken dat is gemaakt in het dialoogvenster `Visual Report Builder`, klikt u op het tandwielpictogram (Opties) in de rechterbovenhoek van een diagram en klikt u vervolgens op **[!UICONTROL Edit]**.

## Stap 2: Metrisch toevoegen

De eerste stap bij het maken van een analyse is het selecteren van [de](../data-user/reports/ess-manage-data-metrics.md) om te analyseren. Terwijl de metriek door gebrek alfabetisch vermeld zijn, kunt u hen door de lijst ook groeperen die metrisch bevoegdheden.

U kunt extra metriek toevoegen nadat aanvankelijke metrisch wordt geselecteerd en alle metriek op één enkel rapport bedekken of multi-metrische berekeningen uitvoeren door formules toe te voegen.

## Stap 3: Toevoegen `Formulas`

`Formulas` worden toegevoegd aan rapporten door op **[!UICONTROL Add Formula]**, die net boven de lijst van metriek in het rapport wordt gevestigd. In de [formule-editor](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), kan om het even welke metriek inbegrepen in het rapport als input worden gebruikt. De basis wiskundige exploitanten worden gebruikt om de verschillende metriek te manipuleren.

Stel dat we een verslag wilden opstellen waarin de gemiddelde inkomsten per bestelling worden weergegeven. In dit geval zouden we de `Revenue` metrisch met de `Number of orders` metrisch.

![](../assets/ave-rev-per-order.png)

## Stap 4: De instelling `Time Period` en `Interval of Analysis` {#time}

Aan nul binnen op een bepaalde rektijd, kunt u de tijdspanne voor de analyse plaatsen. U kunt ook tijdintervallen kiezen om de gegevens te segmenteren (bijvoorbeeld op jaar, op kwartaal of op maand). Gebruik de menu&#39;s in de rechterbovenhoek van het diagram om de tijdsperiode en het interval in te stellen.

![](../assets/Time_Options_Report_Builder.png)

Wanneer het plaatsen van een specifieke datumwaaier voor de tijdspanne, zorg ervoor de begindatum aan het begin van het interval is en de einddatum aan het eind van uw interval is.

Stel bijvoorbeeld een tijdsperiode in van `January 1st to March 1st` en kiest u een `monthly` interval wordt weergegeven `March` als datapoint, maar elke dag negeren `March` behalve `March 1`. In dat geval moet u uw `Time Period` van `January 1 to March 31`.

## Stap 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Uw metriek segmenteren door een gegevensdimensie](../best-practices/segment-filter.md)klikt u op de knop **[!UICONTROL Group by]** aan de linkerbovenhoek van het diagram. Dit zal een dropdown met alle beschikbare afmetingen van eerste metrisch inbegrepen in de lijst openbaren.

U kunt `None` om te voorkomen dat een metrisch wordt gesegmenteerd. Bijvoorbeeld, zou u metrisch kunnen willen die totale opbrengst zonder wordt gesegmenteerd terugkeert, terwijl het hebben van een andere opbrengst metrisch die door gebied wordt gesegmenteerd.

Ga terug naar onze gemiddelde opbrengst per ordevoorbeeld en plaats de Groep door om code te bevorderen. Dit zal ons de gemiddelde opbrengst per orde voor orden zowel met als zonder een Promo code tonen.

![](../assets/Group_By_Report_Builder.png)

Als de metriek inbegrepen in de analyse op verschillende gegevenslijsten wordt voortgebouwd, zal een pop-up u toestaan om de passende gegevensdimensie in elke lijst te selecteren. Het doel is hier dimensies te vinden die het zelfde type van waarden voor segmentatie delen:

![](../assets/Dimension_Editor.png)

## Stap 6: Instelling `Metric Filters`, `Perspective`, en `Time Interval` {#metric-specific}

Voor elke metrische waarde die aan de analyse wordt toegevoegd, kunt u filters toevoegen, het relevante gegevensperspectief selecteren en instellen `time interval` opties. Klik op de trechter (`Filter`), ogen (`Perspective`), en de klok (`Time`) pictogrammen naast de metriek in het rapport.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` de gegevensset in de analyse te beperken. Filters zijn bijvoorbeeld bijzonder handig bij het evalueren van afzonderlijke verwervingskanalen en het verwijderen van uitschieters.

Naast de vervolgkeuzemenu&#39;s en het tekstvak kunt u ook speciale filteroperatoren gebruiken, zoals `LIKE` of `IN` om filters te maken.

Het gebruik van jokertekens (`%` of `_`) in samenhang met `LIKE` instructies wordt ondersteund. De `%` jokerteken komt overeen met meerdere tekens, terwijl `_` komt slechts overeen met één willekeurig teken. Bijvoorbeeld:

- `affiliate's name Like B%` gegevens van klanten waarvan de naam begint met `B`.

- `affiliate's name Like _ake` alleen gegevens toestaan van klanten waarvan de naam zoiets is `Jake`, `Rake`, of `Bake` maar niet `Drake` of `Blake`.

Door meerdere filters toe te voegen, kunt u de gegevens in de grafiek strak beheren. Standaard moeten alle filtervoorwaarden true zijn voor een deel van de gegevens dat wordt opgenomen, maar u kunt OR-relaties maken door het tekstvak Filterregels te bewerken.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` kunt u gemakkelijk schakelen tussen verschillende weergaven van uw gegevens. Laten we eens kijken naar wat er beschikbaar is:

- `Standard perspective`: Het standaardperspectief toont u het resultaat voor de passende datum op x-as (bijvoorbeeld opbrengst in Januari). Dit is het perspectief dat we gebruiken in ons voorbeeld van gemiddelde inkomsten per bestelling.

![](../assets/Standard.png)

- `Amount` OF `Percent Change` versus `Previous Period` perspectief: Dit perspectief toont de hoeveelheid of de percentageverandering van één interval aan volgende en is nuttig om de snelheid van verandering in snel veranderende metriek te meten.Er is ook een perspectief om het interval met de zelfde tijdsperiode vorig jaar te vergelijken om jaar over jaargroei te tonen.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: De `cumulative perspective` toont het lopende of cumulatieve bedrag van de maatstaf over de tijdsperiode. Dit wordt vaak gebruikt om totale klanten te analyseren en voor toekomstige capaciteit te plannen.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Dit perspectief toont de gegevens als percentage van het eerste tijdinterval inbegrepen in de analyse. Dit is nuttig bij het meten van de doeltreffendheid van specifieke acties in verhouding tot de prestaties van de eerste periode.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: Het het rollen perspectief van het middelvenster van gemiddelden toont de het rollen gemiddelde waarde van metrisch over de gespecificeerde tijdwaaier. Het interval moet het zelfde zijn als het interval dat op het rapportniveau wordt geplaatst. Bijvoorbeeld, als het rapport het laatste volledige kwart van Ontvangsten door week toont, kunt u het voortschrijdende gemiddelde tijdwaaier van het venster aan vier weken plaatsen, en de eerste drie waarden zullen ongeldig zijn en de vierde waarde vertegenwoordigt het gemiddelde van de eerste vier weken van Ontvangsten. Voor de duidelijkheid moet u de optie `Multiple Y-Axes` Schakel het selectievakje in als u dezelfde metrische waarde met een voortschrijdend gemiddelde weergeeft, zoals in het onderstaande voorbeeld.

![](../assets/rolling_avg_window.png)

### Opties voor metrische specifieke tijd

Er zijn twee opties voor metriek die in rapporten worden gebruikt: zij kunnen zich in de loop van de tijd , al dan niet volgens de globale tijdopties ontwikkelen , die hen als scalair aantal zullen tonen .

Een metrisch tijdinterval wijzigen in `None` retourneert een `scalar` getal, dat nuttig is bij het maken van formules waarbij een tijdtrending-metrische waarde wordt gedeeld door een `scalar` getal. Bovendien kunt u ook het tijdbereik van het dialoogvenster `scalar` metrisch aan een tijdwaaier onafhankelijk van dat voor het rapport.

We wilden bijvoorbeeld dat de maandelijkse inkomsten voor 2019 uitgedrukt werden als een percentage van de totale inkomsten voor 2019. We kunnen er twee toevoegen `Revenue` cijfers voor een rapport met een algemeen tijdbereik van 1 januari 2019 tot en met 31 december 2019, gesegmenteerd per maandinterval.

>[!NOTE]
>
>Als u `group by` afmetingen, kies een nieuwe visualisatie, of pas het tijdinterval aan en sparen enkel het Aantal (`scalar`), blijven deze aanpassingen niet behouden wanneer u dat rapport weer opent vanaf een dashboard - alleen het tijdsbereik blijft behouden.

Meer informatie over het gebruiken van tijdopties in uw rapporten, zie dit [zelfstudie](../tutorials/time-options-visual-rpt-bldr.md).

## Stap 7: Het rapport opslaan

Wanneer u een nieuw diagram maakt, kunt u het opslaan door op **[!UICONTROL Save]** in de rechterbovenhoek van het dialoogvenster `Visual Report Builder`.

U kunt een grafiek, tabel of nummer opslaan (`scalar`) met de `Type` dropdown en het dashboard waaraan het rapport zou moeten worden bewaard gebruikend `Location` vervolgkeuzelijst.

U kunt het rapport vervolgens opslaan door op **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Resultaten rapporteren

Om u te helpen beslissen welke rapportoutput om te kiezen, zie het volgende:

### Diagram

![](../assets/RB_Chart.png)

### Tabel

![](../assets/RB_Table.png)

### Getal (`scalar`)

![](../assets/RB_Scalar.png)

Gefeliciteerd! U bent klaar.
