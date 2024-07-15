---
title: De visuele Report Builder gebruiken
description: Leer de gegevens in uw rapport gedurende een bepaalde periode te analyseren.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# De [!DNL Visual Report Builder] gebruiken

Met [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) kunt u visueel uw gegevens verkennen om inzichten te tekenen en zakelijke beslissingen te helpen maken. Dit leerprogramma begeleidt u door het proces om een basisrapport tot stand te brengen.

>[!NOTE]
>
>Om een rapport aan een dashboard toe te voegen, hebt u `Standard` [ gebruikerstoestemmingen ](../administrator/user-management/user-management.md) en `Edit` toegang tot het dashboard nodig.

## Stap 1: Een rapport maken

Als u een rapport wilt gaan maken, klikt u op **[!UICONTROL Report Builder]** op de zijbalk of **[!UICONTROL Add Report]** boven aan een dashboard. Klik op de optie **[!UICONTROL Visual Report Builder]** wanneer de pagina `Report Builder` wordt weergegeven.

Als u een rapport wilt bewerken dat in [!DNL Visual Report Builder] is gemaakt, klikt u op het tandwielpictogram (Opties) rechtsboven in een willekeurige grafiek en klikt u op **[!UICONTROL Edit]** .

## Stap 2: Metrisch toevoegen

De eerste stap in het creëren van een analyse selecteert [ metrisch ](../data-user/reports/ess-manage-data-metrics.md) om te analyseren. Terwijl de metriek door gebrek alfabetisch vermeld zijn, kunt u hen door de lijst ook groeperen die metrisch bevoegdheden.

U kunt extra metriek toevoegen nadat aanvankelijke metrisch wordt geselecteerd en alle metriek op één enkel rapport bedekken of multi-metrische berekeningen uitvoeren door formules toe te voegen.

## Stap 3: toevoegen `Formulas`

`Formulas` wordt toegevoegd aan rapporten door **[!UICONTROL Add Formula]** te klikken, die enkel boven de lijst van metriek in het rapport wordt gevestigd. In de [ formuleredacteur ](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), kan om het even welke metriek inbegrepen in het rapport als input worden gebruikt. De basis wiskundige exploitanten worden gebruikt om de verschillende metriek te manipuleren.

Stel dat u een rapport wilt maken waarin de gemiddelde inkomsten per bestelling worden weergegeven. In dit geval deelt u de `Revenue` -metrische waarde door de `Number of orders` -waarde.

![](../assets/ave-rev-per-order.png)

## Stap 4: De instellingen `Time Period` en `Interval of Analysis` {#time}

Aan nul binnen op een bepaalde rektijd, kunt u de tijdspanne voor de analyse plaatsen. U kunt ook tijdintervallen kiezen om de gegevens te segmenteren (bijvoorbeeld op jaar, op kwartaal of op maand). Gebruik de menu&#39;s in de rechterbovenhoek van het diagram om de tijdsperiode en het interval in te stellen.

![](../assets/Time_Options_Report_Builder.png)

Wanneer het plaatsen van een specifieke datumwaaier voor de tijdspanne, zorg ervoor dat de begindatum bij het begin van het interval is en de einddatum aan het eind van uw interval is.

Als u bijvoorbeeld een tijdsperiode instelt van `January 1st` naar `March 1st` en een interval van `monthly` kiest, wordt `March` weergegeven als een datapoint, maar wordt elke dag genegeerd in `March` behalve `March 1` . In dat geval moet u de `Time Period` from `January 1 to March 31` maken.

## Stap 5: `Group by` / `Segmenting the Analysis` {#groupby}

[ om uw metriek door een gegevensdimensie ](../best-practices/segment-filter.md) te segmenteren, klik het **[!UICONTROL Group by]** menu bij de bovenkant verlaten van de grafiek. Dit onthult een dropdown met inbegrip van alle beschikbare afmetingen van eerste metrisch inbegrepen in de lijst.

U kunt `None` kiezen om te voorkomen dat een metrische code wordt gesegmenteerd. Bijvoorbeeld, zou u metrisch kunnen willen die totale opbrengst zonder wordt gesegmenteerd terugkeert, terwijl het hebben van een andere opbrengst metrisch die door gebied wordt gesegmenteerd.

Ga terug naar uw gemiddelde opbrengst per ordevoorbeeld en plaats de Groep door aan bevorderingscode. Dit toont u de gemiddelde opbrengst per orde voor orden zowel met als zonder een bevorderingscode.

![](../assets/Group_By_Report_Builder.png)

Als de metriek inbegrepen in de analyse op verschillende gegevenslijsten wordt voortgebouwd, staat een pop-up u toe om de passende gegevensdimensie in elke lijst te selecteren. Het doel is hier dimensies te vinden die type van waarden voor segmentatie delen:

![](../assets/Dimension_Editor.png)

## Stap 6: Instellen `Metric Filters` , `Perspective` en `Time Interval` {#metric-specific}

Voor elke metrische waarde die aan de analyse wordt toegevoegd, kunt u filters toevoegen, het relevante gegevensperspectief selecteren en `time interval` -opties instellen. Om tot deze eigenschappen toegang te hebben, klik de trechter (`Filter`), oog (`Perspective`), en klok (`Time`) pictogrammen die naast de metriek inbegrepen in het rapport worden gevestigd.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` beperkt de gegevensset die in de analyse is opgenomen. Filters zijn bijvoorbeeld handig bij het evalueren van afzonderlijke verwervingskanalen en het verwijderen van uitschieters.

Naast de vervolgkeuzemenu&#39;s en het tekstvak kunt u ook speciale filteroperatoren gebruiken, zoals `LIKE` of `IN` , om filters te maken.

Het gebruik van jokertekens (`%` of `_` ) met `LIKE` -instructies wordt ondersteund. Het jokerteken `%` komt overeen met meerdere tekens, terwijl `_` alleen overeenkomt met één willekeurig teken. Bijvoorbeeld:

- `affiliate's name Like B%` staat alleen gegevens toe van klanten wier naam begint met `B` .

- `affiliate's name Like _ake` staat alleen gegevens toe van klanten waarvan de namen `Jake`, `Rake` of `Bake` maar niet `Drake` of `Blake` zijn.

Door meerdere filters toe te voegen, kunt u de gegevens in de grafiek strak beheren. Standaard moeten alle filtervoorwaarden true zijn voor een deel van de gegevens dat wordt opgenomen, maar u kunt OR-relaties maken door het tekstvak Filterregels te bewerken.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Hiermee kunt u eenvoudig schakelen tussen de verschillende weergaven van uw gegevens. Kijk wat er beschikbaar is:

- `Standard perspective`: In het standaardperspectief ziet u het resultaat van de overeenkomende datum op de x-as (bijvoorbeeld omzet in januari). Dit is het perspectief dat u in uw Gemiddelde opbrengst per ordevoorbeeld gebruikt.

![](../assets/Standard.png)

- `Amount` OF `Percent Change` versus `Previous Period` perspectief: dit perspectief toont de hoeveelheid of het percentage verandering van het ene interval in het volgende en is nuttig om de snelheid van verandering in snel veranderende metriek te meten. Er is ook een perspectief om het interval te vergelijken met dezelfde periode vorig jaar om de groei van jaar tot jaar te laten zien.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: `cumulative perspective` toont het lopende of cumulatieve totale bedrag van metrisch over de tijdspanne. Dit wordt vaak gebruikt om totale klanten te analyseren en voor toekomstige capaciteit te plannen.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: In dit perspectief worden de gegevens weergegeven als een percentage van het eerste interval dat is opgenomen in de analyse. Dit is nuttig bij het meten van de doeltreffendheid van specifieke acties in verhouding tot de prestaties van de eerste periode.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: het het rollen gemiddelde perspectief van het venster van gemiddelden toont de het rollen gemiddelde waarde van metrisch over de gespecificeerde tijdwaaier. Het interval moet het zelfde zijn als het interval dat op het rapportniveau wordt geplaatst. Bijvoorbeeld, als het rapport het laatste volledige kwart van Ontvangsten door week toont, kunt u het het rollen gemiddelde tijdwaaier van het venster aan vier weken plaatsen. Dit betekent dat de eerste drie waarden null zijn en de vierde waarde het gemiddelde van de eerste vier weken van Ontvangsten vertegenwoordigt. Voor de duidelijkheid moet u het selectievakje `Multiple Y-Axes` uitschakelen als u dezelfde maateenheid met een voortschrijdend gemiddelde weergeeft, zoals in het onderstaande voorbeeld.

![](../assets/rolling_avg_window.png)

### Opties voor metrische specifieke tijd

Er zijn twee opties voor metriek die in rapporten worden gebruikt: zij kunnen zich in tijd volgens de globale tijdopties, of niet ontwikkelen, die hen als scalair aantal zullen tonen.

Als u een metrisch tijdinterval instelt op `None` , wordt een `scalar` -getal geretourneerd. Dit is handig wanneer u formules maakt die een metrische tijdwaarde delen door een `scalar` -getal. U kunt ook het tijdbereik van de metrische waarde van `scalar` wijzigen in een tijdbereik dat onafhankelijk is van dat voor het rapport.

Bijvoorbeeld, wilde u 2019 maandelijkse inkomsten die als percentage van totale inkomsten 2019 worden uitgedrukt. U kunt twee `Revenue` metriek aan een rapport met een globaal tijdwaaier van 1 Januari, 2019, aan December 31 toevoegen 2019, die door maandinterval wordt gesegmenteerd.

>[!NOTE]
>
>Als u `group by` afmetingen toevoegt, kies een nieuwe visualisatie, of pas het tijdinterval aan en bewaar dan enkel het Aantal (`scalar`). Deze aanpassingen blijven niet behouden wanneer u dat rapport weer opent vanaf een dashboard - alleen het tijdsbereik blijft behouden.

Meer over het gebruiken van tijdopties in uw rapporten leren, zie dit [ leerprogramma ](../tutorials/time-options-visual-rpt-bldr.md).

## Stap 7: Het rapport opslaan

Wanneer u een grafiek maakt, kunt u deze opslaan door op **[!UICONTROL Save]** in de rechterbovenhoek van `Visual Report Builder` te klikken.

U kunt verkiezen om een grafiek, een lijst, of een aantal (`scalar`) te bewaren gebruikend `Type` dropdown en het dashboard waaraan het rapport zou moeten worden bewaard gebruikend `Location` dropdown.

U kunt het rapport vervolgens opslaan door op **[!UICONTROL Save to Dashboard]** te klikken.

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
