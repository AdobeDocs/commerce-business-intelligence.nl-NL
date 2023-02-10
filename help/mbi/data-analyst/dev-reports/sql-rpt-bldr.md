---
title: De SQL-Report Builder gebruiken
description: Leer de in- en uiteinden van het gebruik van de SQL-Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 0%

---

# Gebruiken `SQL Report Builder`

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md) om SQL-grafieken te maken en te bewerken. `Standard` gebruikers kunnen deze grafieken op dashboards opnieuw rangschikken, en `Read-only` de gebruikers zullen de zelfde ervaring hebben zij met traditionele grafieken doen. Daarnaast `Read-only` gebruikers hebben geen toegang tot de tekst van de query.

Zie onze [trainingsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) voor meer informatie.

`SQL`, of Gestructureerde Taal van de Vraag, is een programmeertaal die wordt gebruikt om met gegevensbestanden te communiceren. In [!DNL MBI], SQL wordt gebruikt om, gegevens van uw gegevenspakhuis te vragen of terug te winnen. Bekijk de rapporten op uw dashboard - achter de scènes, elk wordt aangedreven door een SQL vraag.

U kunt de [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) om uw gegevenspakhuis direct te vragen, bekijk de resultaten, en zet hen in een grafiek om. U kunt een rapport maken met de `SQL Report Builder` door te navigeren naar **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Zie onze [trainingsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) voor meer informatie.

De `SQL Report Builder` staat u toe om uw gegevenspakhuis direct te vragen, de resultaten te bekijken, en hen snel om te zetten in een grafiek. Het beste deel over het gebruiken van SQL om rapporten te bouwen is dat u niet op updatecycli hoeft te wachten om op kolommen te herhalen u creeert. Als de resultaten niet behoorlijk juist kijken, kunt u de vraag snel uitgeven en opnieuw in werking stellen tot de dingen uw verwachtingen aanpassen.

In dit artikel doorlopen we u met de `SQL Report Builder`. Nadat u uw weg rond hebt gekend, controleer onze SQL voor visualisatiezelfstudie of probeer optimaliserend sommige vragen u hebt geschreven.

Hier volgt een overzicht van wat we in dit artikel behandelen:

1. [Een query schrijven](#writing)

1. [De query uitvoeren en de resultaten weergeven](#runquery)

1. [Een visualisatie maken](#createviz)

1. [Het rapport opslaan](#save)

## SQL Report Builder-integratie

In de huidige staat van de wereld, [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) is de enige integratie die niet beschikbaar is voor gebruik met de [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). We werken eraan deze functionaliteit in een latere release op te nemen.

Als u een nieuw SQL-rapport wilt gaan maken, klikt u op **[!UICONTROL Report Builder]** of **[!UICONTROL Add Report]** boven aan een dashboard. In de `Report Picker` scherm, klikken **[!UICONTROL SQL Report Builder]** om de SQL-editor te openen.

## Aan de slag

Als u een rapport wilt bewerken, klikt u op het gereedschap (![](../../assets/gear-icon.png)) in de rechterbovenhoek van een op SQL gebaseerd diagram en klik op **[!UICONTROL Edit]**.

## Een query schrijven {#writing}

>[!NOTE]
>
>`SQL Report Builder` query&#39;s zijn hoofdlettergevoelig. Zorg ervoor u het correcte geval gebruikt wanneer het schrijven van vragen of u kon met onverwachte resultaten of fouten opwinden.

Na de [richtlijnen voor queryoptimalisatie](../../best-practices/optimizing-your-sql-queries.md), schrijft u een query in de SQL-editor.

>[!IMPORTANT]
>
>**Metriek in SQL-rapporten** - Wanneer u metrisch in een SQL- rapport opneemt, `current definition` van de metrische waarde wordt gebruikt.

Als metrisch in de toekomst wordt bijgewerkt, het SQL- rapport *niet* de wijzigingen weerspiegelen. U zult het rapport manueel moeten uitgeven om de veranderingen van kracht te hebben.

Met de knoppen boven aan het zijpaneel kunt u schakelen tussen tabellen en metriek die beschikbaar zijn voor gebruik in het dialoogvenster `SQL Report Builder`. Als u niet ziet waarnaar u zoekt in de lijst, zoekt u ernaar op de zoekbalk boven in de zijbalk.

U kunt sidebar in de SQL redacteur ook gebruiken om metriek, lijsten, en kolommen direct in uw vragen op te nemen door over hen te hangen en te klikken **[!UICONTROL Insert]**:

![Een tabel invoegen in de SQL-editor.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Alle [SELECT, functie](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), of elke functie die geen gegevens muteert, die wordt ondersteund door PostgreSQL, wordt ondersteund in de SQL-Report Builder. Dit omvat, maar is niet beperkt tot, AVG, COUNT, COUNT DISTINCT, MIN/MAX en SUM.

Bovendien wordt elk JOIN-type ondersteund, maar we raden u aan alleen BINNER JOIN te gebruiken, omdat dit het goedkoopst is voor de JOIN-typen.

## De query uitvoeren en de resultaten weergeven {#runquery}

Wanneer u klaar bent met het schrijven van uw query, klikt u op **[!UICONTROL Run Query]**. De resultaten worden weergegeven in een tabel onder de SQL-editor:

![De query uitvoeren en de resultaten weergeven.](../../assets/SQL_Run_Query.gif)

Als er iets in de resultaten lijkt, kunt u de query bewerken en opnieuw uitvoeren totdat u tevreden bent.

Soms ziet u [berichten onder de redacteur met EXPLAIN in hen](../../best-practices/optimizing-your-sql-queries.md). Als u één van deze ziet, betekent dat dat uw vraag niet heeft gelopen en een beetje van fijnafstemmen nodig heeft.

Nadat u klaar bent met het bewerken van uw query, kunt u overschakelen op het maken van een visualisatie of het opslaan van uw werk op een dashboard.

## Een visualisatie maken {#createviz}

Als u een visualisatie wilt maken met uw queryresultaten, klikt u op de knop **[!UICONTROL Chart]** in de `Results` venster. Op dit tabblad selecteert u:

* De `Series`of de kolom die u wilt meten, zoals **Objecten verkocht**.
* De `Category`of de kolom die u wilt gebruiken om uw gegevens te segmenteren, zoals **aankoopbron**.
* De `Labels`, of waarden voor de X-as.

Hieronder volgt een kort overzicht van hoe het visualisatieproces eruitziet:

![](../../assets/SQL_RB_viz_overview.gif)

Voor een gedetailleerd overzicht van hoe u een visualisatie kunt maken, raadpleegt u onze [Visualisaties maken op basis van de zelfstudie SQL-query&#39;s](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Het rapport opslaan {#save}

Voordat u uw werk kunt opslaan, moet u het rapport een naam geven. Vergeet niet de [richtlijnen voor aanbevolen procedures voor naamgeving](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} en kies iets dat duidelijk laat zien wat het rapport is!

Klikken **[!UICONTROL Save]** in de rechterbovenhoek van de SQL-editor en selecteer het rapport `Type` (`Chart` of `Table`). Als u de tekst wilt laten omlopen, selecteert u het dashboard waarin u het rapport wilt opslaan en klikt u op **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Uw gegevens analyseren

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) geeft u de macht om uw gegevenspakhuis direct te vragen, de resultaten te bekijken, en hen snel om te zetten in een rapport. Met SQL kunt u ook [om SQL functies te gebruiken die niet beschikbaar zijn](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) in de `Visual` of `Cohort` Report Builder, zodat u meer controle hebt over uw gegevens.

We willen graag vermelden dat berekende kolommen die met SQL zijn gemaakt, niet afhankelijk zijn van updatecycli. Dit betekent dat u deze kolommen op dezelfde manier kunt doorlopen als u wilt en de resultaten direct kunt zien.

>[!NOTE]
>
>Dit geldt alleen voor de structuur van de kolom, niet voor de versheid van de gegevens. Nieuwe gegevens zijn nog steeds afhankelijk van voltooide updatecycli.

| **Dit is perfect voor...** | **Dat is niet zo geweldig voor...** |
|---|---|
| Tussentijdse/gevorderde analisten | Beginners - u moet SQL kennen. |
| De SQL savvy | Eenvoudige analyses - het schrijven van een vraag kan meer werk zijn dan eenvoudig het gebruiken van Visual Report Builder. |
| Berekende kolommen voor eenmalig gebruik samenstellen | Delen met anderen - overweeg uw publiek: begrijpen ze SQL? Zo niet, dan kunnen ze verward worden door de manier waarop het rapport is opgebouwd. |
| Gegevens met `one-to-many` relaties |  |
| Een nieuwe kolom of analyse testen |  |

#### Resultaten van database versus SQL Editor

Het grootste deel van de tijd, kunnen de verschillen in resultaten aan updatecycli worden toegeschreven. Indien [!DNL MBI] is bezig gegevens van uw gegevensbestand aan uw Data Warehouse te herhalen, zou u verschillende resultaten kunnen zien zelfs wanneer het gebruiken van de zelfde vraag.

Verbindingsproblemen kunnen ook tot discrepanties leiden. Ga naar de `Connections` pagina door te klikken **[!DNL Manage Data** > **Connections]**) om het uit te checken - is er een fout voor de betreffende integratie van de database? Indien dit het geval is, kan het nodig zijn [de integratie opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en) om de zaken weer aan de gang te krijgen.

Als al uw integraties met succes worden verbonden en u niet in het midden van een updatecyclus bent, kan iets anders misleidend zijn.

#### Verwijdert het schrappen van een SQL rapport ook de onderliggende kolommen uit mijn Data Warehouse?

Nee, u verliest geen kolommen van uw Data Warehouse, ongeacht hoe u ze hebt gemaakt.

Kolommen die zijn gemaakt met de `Data Warehouse Manager` zal niet worden beïnvloed als u een rapport of een vraag schrapt die hen gebruikt.

Kolommen die zijn gemaakt met de `SQL Report Builder` niet worden opgeslagen in uw Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

De `SQL Report Builder` geeft u meer flexibiliteit bij het maken en structureren van uw grafieken. U kunt bijvoorbeeld selecteren welke waarden op de `X` en `Y` assen. Voor meer informatie over het maken van grafieken in het dialoogvenster `SQL Report Builder`, controleer onze [Visualisaties maken van SQL-query&#39;s](../../tutorials/create-visuals-from-sql.md) zelfstudie.

#### `Cohort Report Builder` {#cohortrb}

In tegenstelling tot `Visual Report Builder`de [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) is bedoeld voor het analyseren en identificeren van gedragstrends van soortgelijke gebruikersgroepen in de loop van de tijd . Voor het gebruik van de Cohort-Report Builder is geen SQL-savvy vereist, dus u kunt zonder aarzeling naar binnen duiken als u net bent begonnen.

| **Dit is perfect voor...** | **Dat is niet zo geweldig voor...** |
|---|---|
| Tussentijdse/gevorderde analisten | Beginners - u hebt oefening nodig die cohorten definieert. |
| Gedragstrends in de loop der tijd identificeren | Kwalitatieve analyse - het kan [gedaan](../dev-reports/create-qual-cohort-analysis.md), maar wij hebben onze hulp nodig. |

## Vragen opnieuw samenstellen na de updatecyclus

U hoeft uw query&#39;s niet opnieuw samen te stellen. Rapporten gemaakt met de [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) worden opgeslagen als in de traditionele `Report Builder`. Het updateproces voor SQL-grafieken is precies hetzelfde. Nadat uw gegevens zijn bijgewerkt, worden de waarden in uw grafieken opnieuw berekend en weergegeven.

>[!NOTE]
>
>Wanneer het schrappen van een SQL rapport/vraag het schrapt niet de onderliggende kolommen van uw Data Warehouse. U verliest geen kolommen, ongeacht hoe u ze hebt gemaakt.

* De kolommen die worden gecreeerd gebruikend de Manager van de Data Warehouse zullen niet worden beïnvloed als u een rapport of een vraag schrapt die hen gebruikt.

* Kolommen die zijn gemaakt met de SQL-Report Builder, worden niet opgeslagen in uw Data Warehouse.

## Omloop {#wrapup}

Als u iets een beetje uitdagender wilt proberen, waarom probeert niet het schrijven van een vraag die voor visualisatie wordt geoptimaliseerd? Bekijk onze [Visualisaties maken op basis van de zelfstudie SQL-query&#39;s](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} om aan de slag te gaan.
