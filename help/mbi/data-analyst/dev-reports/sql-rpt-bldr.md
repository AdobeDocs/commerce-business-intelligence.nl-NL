---
title: De SQL Report Builder gebruiken
description: Leer de in- en uitgangen van de SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---

# [!DNL SQL Report Builder] gebruiken

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../administrator/user-management/user-management.md) om SQL grafieken tot stand te brengen en uit te geven. `Standard` -gebruikers kunnen deze grafieken opnieuw rangschikken op dashboards en `Read-only` -gebruikers hebben dezelfde ervaring als met traditionele grafieken. Bovendien hebben `Read-only` -gebruikers geen toegang tot de tekst van de query.

Zie de [ opleidingsvideo ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) om meer te leren.

[!DNL SQL] (Structured Query Language) is een programmeertaal die wordt gebruikt om te communiceren met databases. In [!DNL Commerce Intelligence] wordt [!DNL SQL] gebruikt om gegevens van uw Data Warehouse te zoeken of op te halen. Bekijk de rapporten op uw dashboard - achter de schermen, wordt elk aangedreven door een [!DNL SQL] vraag.

Met de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) kunt u rechtstreeks query&#39;s uitvoeren op uw Data Warehouse, de resultaten bekijken en deze transformeren in een grafiek. U kunt een rapport maken met de [!DNL SQL Report Builder] door op **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]** te klikken.

Zie de [ opleidingsvideo ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) om meer te leren.

Met [!DNL SQL Report Builder] kunt u rechtstreeks query&#39;s uitvoeren op uw Data Warehouse, de resultaten bekijken en deze snel omzetten in een grafiek. Het beste deel over het gebruiken van [!DNL SQL] om rapporten te bouwen is dat u niet op updatecycli hoeft te wachten om op kolommen te herhalen u creeert. Als de resultaten niet goed lijken, kunt u de vraag snel uitgeven en opnieuw uitvoeren tot de dingen uw verwachtingen aanpassen.

Dit onderwerp doorloopt u gebruikend [!DNL SQL Report Builder]. Nadat u de weg hebt gekend, controleer [!DNL SQL] voor visualisatiezelfstudie of probeer optimaliserend sommige vragen u hebt geschreven.

Omvat in dit artikel:

1. [Een query schrijven](#writing)

1. [De query uitvoeren en de resultaten weergeven](#runquery)

1. [Een visualisatie maken](#createviz)

1. [Het rapport opslaan](#save)

## [!DNL SQL Report Builder] Integraties

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) is de enige integratie die niet beschikbaar is voor gebruik met de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) . Deze functionaliteit is in ontwikkeling.

Als u een [!DNL SQL] -rapport wilt gaan maken, klikt u op **[!UICONTROL Report Builder]** of **[!UICONTROL Add Report]** boven aan een dashboard. Klik in het [!DNL Report Picker] -scherm op **[!UICONTROL SQL Report Builder]** om de [!DNL SQL] -editor te openen.

## Aan de slag

Als u een rapport wilt bewerken, klikt u op het tandwielpictogram (![](../../assets/gear-icon.png)) in de rechterbovenhoek van een [!DNL SQL] -diagram en klikt u op **[!UICONTROL Edit]** .

## Een query schrijven {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] -query&#39;s zijn hoofdlettergevoelig. Zorg ervoor u het correcte geval gebruikt wanneer het schrijven van vragen of u kon met onverwachte resultaten of fouten opwinden.

Na de [ richtlijnen voor vraagoptimalisering ](../../best-practices/optimizing-your-sql-queries.md), schrijf een vraag in de [!DNL SQL] redacteur.

>[!IMPORTANT]
>
>**Metriek in [!DNL SQL] rapporten** - wanneer u metrisch in een SQL rapport opneemt, wordt `current definition` van metrisch gebruikt.

Als metrisch in de toekomst wordt bijgewerkt, wijst het SQL rapport *niet* op de veranderingen. De wijzigingen worden pas van kracht nadat u het rapport handmatig hebt bewerkt.

Met de knoppen boven aan het zijpaneel kunt u schakelen tussen lijsten met tabellen en metriek die beschikbaar zijn voor gebruik in de [!DNL SQL Report Builder] . Als u niet ziet waarnaar u zoekt in de lijst, zoekt u ernaar op de zoekbalk boven in de zijbalk.

U kunt de zijbalk in de [!DNL SQL] -editor ook gebruiken om metriek, tabellen en kolommen rechtstreeks in uw query&#39;s in te voegen door de cursor boven de tekst te plaatsen en op **[!UICONTROL Insert]** te klikken:

![ Invoegend een lijst in de [!DNL SQL] redacteur.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Om het even welke [ UITGEZOCHTE functie ](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), of om het even welke functie die geen gegevens muteert, die door PostSQL wordt gesteund wordt gesteund in SQL Report Builder. Dit omvat, maar is niet beperkt tot, AVG, COUNT, COUNT DISTINCT, MIN/MAX en SUM.

Elk `JOIN` -type wordt ook ondersteund, maar Adobe raadt u alleen aan INNER JOIN te gebruiken omdat dit het goedkoopst is voor de `JOIN` -typen.

## De query uitvoeren en de resultaten weergeven {#runquery}

Klik op **[!UICONTROL Run Query]** als u klaar bent met het schrijven van de query. De resultaten worden weergegeven in een tabel onder de SQL-editor:

![ in werking stellend de vraag en het bekijken resultaten.](../../assets/SQL_Run_Query.gif)

Als er iets mis lijkt in de resultaten, kunt u de query bewerken en opnieuw uitvoeren totdat u tevreden bent.

U zou soms [ berichten onder de redacteur met EXPLAIN in hen ](../../best-practices/optimizing-your-sql-queries.md) kunnen zien. Als u één van deze ziet, betekent dat dat uw vraag niet heeft gelopen en een beetje van fijnafstemmen nodig heeft.

Nadat u klaar bent met het bewerken van uw query, kunt u overschakelen op het maken van een visualisatie of het opslaan van uw werk op een dashboard.

## Een visualisatie maken {#createviz}

Als u een visualisatie wilt maken met de resultaten van de query, klikt u op de tab **[!UICONTROL Chart]** in het deelvenster `Results` . Op dit tabblad selecteert u:

* `Series`, of de kolom u, zoals **verkochte Punten** wilt meten.
* `Category`, of de kolom u wilt gebruiken om uw gegevens, zoals **verwervingsbron** te segmenteren.
* De waarden voor de `Labels` -as of de X-as.

Hieronder volgt een kort overzicht van hoe het visualisatieproces eruitziet:

![](../../assets/SQL_RB_viz_overview.gif)

Voor een gedetailleerde looppas-door van hoe te om een visualisatie tot stand te brengen, verwijs naar [ Creërend visualisaties van SQL vragen leerprogramma ](../../tutorials/create-visuals-from-sql.md){: target="_blank"}.

## Het rapport opslaan {#save}

Voordat u uw werk kunt opslaan, moet u het rapport een naam geven. Herinner me om de [ beste praktijkrichtlijnen voor het noemen ](../../best-practices/naming-elements.md){: target="_blank"} te volgen en iets te kiezen dat duidelijk overbrengt wat het rapport is!

Klik op **[!UICONTROL Save]** in de rechterbovenhoek van de [!DNL SQL] -editor en selecteer het rapport `Type` ( `Chart` of `Table`). Als u de tekst wilt laten omlopen, selecteert u het dashboard waarin u het rapport wilt opslaan en klikt u op **[!UICONTROL Save to Dashboard]** .

![](../../assets/SQL_Save_Report.gif)

### Uw gegevens analyseren

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) geeft u de macht om uw Data Warehouse direct te vragen, de resultaten te bekijken, en hen snel om te zetten in een rapport. Het gebruiken van [!DNL SQL] staat u [ ook toe om  [!DNL SQL]  functies te gebruiken die niet beschikbaar ](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) in `Visual` of `Cohort` de Bouwers van het Rapport zijn, waarbij u grotere controle over uw gegevens geeft.

Berekende kolommen die zijn gemaakt met [!DNL SQL] zijn niet afhankelijk van updatecycli. Dit betekent dat u deze kolommen kunt doorlopen zoals u wilt en de resultaten direct kunt zien.

>[!NOTE]
>
>Dit geldt alleen voor de structuur van de kolom, niet voor de versheid van de gegevens. Nieuwe gegevens zijn nog steeds afhankelijk van voltooide updatecycli.

| **dit is perfect voor...** | **dit is niet zo groot voor...** |
|---|---|
| Tussentijdse/gevorderde analisten | Beginners - u moet het weten [!DNL SQL]. |
| De [!DNL SQL] savvy | Eenvoudige analyses - het schrijven van een query kan meer werken dan het eenvoudig gebruiken van [!UICONTROL Visual Report Builder]. |
| Berekende kolommen voor eenmalig gebruik samenstellen | Delen met anderen - Overweeg uw publiek: begrijpen ze [!DNL SQL] ? Zo niet, dan kunnen ze verward worden door de manier waarop het rapport is opgebouwd. |
| Gegevens met `one-to-many` relaties |  |
| Een nieuwe kolom of analyse testen |  |

#### Resultaten van database versus SQL Editor

Meestal kunnen verschillen in resultaten worden toegeschreven aan updatecycli. Als [!DNL Commerce Intelligence] bezig is met het repliceren van gegevens van uw database naar uw Data Warehouse, ziet u mogelijk verschillende resultaten, zelfs als u dezelfde query gebruikt.

Verbindingsproblemen kunnen ook tot discrepanties leiden. Navigeer naar de pagina `Connections` door op **[!DNL Manage Data** > **Connections]** te klikken om de pagina uit te checken. Is er een fout opgetreden voor de databaseintegratie in kwestie? Als zo, kunt u de integratie [ moeten opnieuw voor authentiek verklaren om dingen te krijgen die opnieuw lopen.](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

Als al uw integraties met succes worden verbonden en u niet in het midden van een updatecyclus bent, kan iets anders misleidend zijn.

#### Verwijdert het schrappen van een [!DNL SQL] rapport ook de onderliggende kolommen uit mijn Data Warehouse?

Nee, u verliest geen kolommen van uw Data Warehouse, ongeacht hoe u ze hebt gemaakt.

Kolommen die zijn gemaakt met de methode `Data Warehouse Manager` worden niet beïnvloed als u een rapport of query verwijdert waarin ze worden gebruikt.

Kolommen die zijn gemaakt met [!DNL SQL Report Builder] , worden niet opgeslagen op uw Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

[!DNL SQL Report Builder] geeft u meer flexibiliteit bij het maken en structureren van uw grafieken. U kunt bijvoorbeeld selecteren welke waarden op de `X` - en `Y` -as moeten worden weergegeven. Voor meer informatie bij het creëren van grafieken in [!DNL SQL Report Builder], controleer [ Creërend visualisaties van  [!DNL SQL]  vragen ](../../tutorials/create-visuals-from-sql.md) leerprogramma.

#### `Cohort Report Builder` {#cohortrb}

In tegenstelling tot de [!DNL Visual Report Builder] is de [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) bedoeld voor één doel: het analyseren en identificeren van gedragstrends van vergelijkbare gebruikersgroepen in de loop van de tijd. Als u [!DNL Cohort Report Builder] gebruikt, hebt u geen [!DNL SQL] savvy nodig. U kunt dus zonder aarzeling naar binnen duiken als u net bent begonnen.

| **dit is perfect voor...** | **dit is niet zo groot voor...** |
|---|---|
| Tussentijdse/gevorderde analisten | Beginners - u hebt praktische cohorten nodig. |
| Gedragstrends in de loop der tijd identificeren | Kwalitatieve analyse - het kan [ worden gedaan ](../dev-reports/create-qual-cohort-analysis.md), maar vereist de hulp van Adobe. |

## Vragen opnieuw samenstellen na de updatecyclus

U hoeft uw query&#39;s niet opnieuw samen te stellen. Rapporten die zijn gemaakt met de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) , worden opgeslagen als de rapporten die zijn gemaakt met de traditionele `Report Builder` . Het updateproces voor [!DNL SQL] grafieken is hetzelfde. Nadat uw gegevens zijn bijgewerkt, worden de waarden in uw grafieken opnieuw berekend en weergegeven.

>[!NOTE]
>
>Wanneer u een [!DNL SQL] -rapport/query verwijdert, worden de onderliggende kolommen niet uit uw Data Warehouse verwijderd. U verliest geen kolommen, ongeacht hoe u ze hebt gemaakt.

* Kolommen die zijn gemaakt met Data Warehouse Manager worden niet beïnvloed als u een rapport of query verwijdert waarin ze worden gebruikt.

* Kolommen die zijn gemaakt met de SQL Report Builder worden niet opgeslagen op uw Data Warehouse.

## Omloop {#wrapup}

Als u iets een beetje uitdagender wilt proberen, waarom probeert niet het schrijven van een vraag die voor visualisatie wordt geoptimaliseerd? Controle uit [ Creërend visualisaties van  [!DNL SQL]  vragen leerprogramma ](../../tutorials/create-visuals-from-sql.md){: target="_blank"} om begonnen te worden.
