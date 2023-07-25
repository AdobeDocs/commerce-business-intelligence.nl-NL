---
title: De SQL-Report Builder gebruiken
description: Leer de in- en uiteinden van het gebruik van de SQL-Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Gebruiken [!DNL SQL Report Builder]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md) om SQL-grafieken te maken en te bewerken. `Standard` gebruikers kunnen deze grafieken op dashboards opnieuw rangschikken, en `Read-only` gebruikers hebben dezelfde ervaring als met traditionele grafieken . Daarnaast `Read-only` gebruikers hebben geen toegang tot de tekst van de query.

Zie de [trainingsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) voor meer informatie.

[!DNL SQL], of Gestructureerde Taal van de Vraag, is een programmeertaal die wordt gebruikt om met gegevensbestanden te communiceren. In [!DNL Commerce Intelligence], [!DNL SQL] wordt gebruikt om, gegevens van uw Data Warehouse te vragen of terug te winnen. Kijk naar de rapporten op je dashboard - achter de schermen wordt elk van hen aangedreven door een [!DNL SQL] query.

U kunt de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) om uw Data Warehouse direct te vragen, bekijk de resultaten, en zet hen in een grafiek om. U kunt een rapport maken met de [!DNL SQL Report Builder] door te klikken **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Zie de [trainingsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) voor meer informatie.

De [!DNL SQL Report Builder] staat u toe om uw Data Warehouse direct te vragen, de resultaten te bekijken, en hen snel om te zetten in een grafiek. Het beste onderdeel over het gebruik [!DNL SQL] om rapporten te bouwen is dat u niet op updatecycli hoeft te wachten om op kolommen te herhalen u creeert. Als de resultaten niet goed lijken, kunt u de vraag snel uitgeven en opnieuw uitvoeren tot de dingen uw verwachtingen aanpassen.

Dit onderwerp loopt u door het gebruiken van [!DNL SQL Report Builder]. Nadat je je weg hebt weten, kun je de [!DNL SQL] voor een zelfstudie over visualisaties of optimaliseer enkele query&#39;s die u hebt geschreven.

Omvat in dit artikel:

1. [Een query schrijven](#writing)

1. [De query uitvoeren en de resultaten weergeven](#runquery)

1. [Een visualisatie maken](#createviz)

1. [Het rapport opslaan](#save)

## [!DNL SQL Report Builder] Integraties

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) is de enige integratie die niet beschikbaar is voor gebruik met de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Deze functionaliteit is in ontwikkeling.

Ga als volgt te werk om een [!DNL SQL] rapport, klik **[!UICONTROL Report Builder]** of **[!UICONTROL Add Report]** boven aan een dashboard. In de [!DNL Report Picker] scherm, klikken **[!UICONTROL SQL Report Builder]** om de [!DNL SQL] editor.

## Aan de slag

Als u een rapport wilt bewerken, klikt u op het gereedschap (![](../../assets/gear-icon.png)) in de rechterbovenhoek van een [!DNL SQL]-gebaseerde grafiek en klik **[!UICONTROL Edit]**.

## Een query schrijven {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] query&#39;s zijn hoofdlettergevoelig. Zorg ervoor u het correcte geval gebruikt wanneer het schrijven van vragen of u kon met onverwachte resultaten of fouten opwinden.

Na de [richtlijnen voor queryoptimalisatie](../../best-practices/optimizing-your-sql-queries.md), schrijven een vraag in [!DNL SQL] editor.

>[!IMPORTANT]
>
>**Metrisch in [!DNL SQL] rapporten** - Wanneer u metrisch in een SQL- rapport opneemt, `current definition` van de metrische waarde wordt gebruikt.

Als metrisch in de toekomst wordt bijgewerkt, het SQL- rapport *niet* de wijzigingen weerspiegelen. De wijzigingen worden pas van kracht nadat u het rapport handmatig hebt bewerkt.

Met de knoppen boven aan het zijpaneel kunt u schakelen tussen tabellen en metriek die beschikbaar zijn voor gebruik in het dialoogvenster [!DNL SQL Report Builder]. Als u niet ziet waarnaar u zoekt in de lijst, zoekt u ernaar op de zoekbalk boven in de zijbalk.

U kunt de zijbalk ook gebruiken in het dialoogvenster [!DNL SQL] editor om metriek, tabellen en kolommen rechtstreeks in te voegen in uw query&#39;s door de muis erboven te plaatsen en op **[!UICONTROL Insert]**:

![Een tabel invoegen in de [!DNL SQL] editor.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Alle [SELECT, functie](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), of elke functie die geen gegevens muteert, die wordt ondersteund door PostgreSQL, wordt ondersteund in de SQL-Report Builder. Dit omvat, maar is niet beperkt tot, AVG, COUNT, COUNT DISTINCT, MIN/MAX en SUM.

Ook alle `JOIN` type wordt ondersteund, maar Adobe raadt u aan alleen BINNER JOIN te gebruiken omdat dit de goedkoopste `JOIN` typen.

## De query uitvoeren en de resultaten weergeven {#runquery}

Wanneer u klaar bent met het schrijven van uw query, klikt u op **[!UICONTROL Run Query]**. De resultaten worden weergegeven in een tabel onder de SQL-editor:

![De query uitvoeren en de resultaten weergeven.](../../assets/SQL_Run_Query.gif)

Als er iets mis lijkt in de resultaten, kunt u de query bewerken en opnieuw uitvoeren totdat u tevreden bent.

Soms ziet u [berichten onder de redacteur met EXPLAIN in hen](../../best-practices/optimizing-your-sql-queries.md). Als u één van deze ziet, betekent dat dat uw vraag niet heeft gelopen en een beetje van fijnafstemmen nodig heeft.

Nadat u klaar bent met het bewerken van uw query, kunt u overschakelen op het maken van een visualisatie of het opslaan van uw werk op een dashboard.

## Een visualisatie maken {#createviz}

Als u een visualisatie wilt maken met uw queryresultaten, klikt u op de knop **[!UICONTROL Chart]** in de `Results` venster. Op dit tabblad selecteert u:

* De `Series`of de kolom die u wilt meten, zoals **Objecten verkocht**.
* De `Category`of de kolom die u wilt gebruiken om uw gegevens te segmenteren, zoals **aankoopbron**.
* De `Labels`, of waarden voor de X-as.

Hieronder volgt een kort overzicht van hoe het visualisatieproces eruitziet:

![](../../assets/SQL_RB_viz_overview.gif)

Voor een gedetailleerde doorloop van hoe te om een visualisatie tot stand te brengen, verwijs naar [Visualisaties maken op basis van de zelfstudie SQL-query&#39;s](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Het rapport opslaan {#save}

Voordat u uw werk kunt opslaan, moet u het rapport een naam geven. Vergeet niet de [richtlijnen voor aanbevolen procedures voor naamgeving](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} en kies iets dat duidelijk laat zien wat het rapport is!

Klikken **[!UICONTROL Save]** in de rechterbovenhoek van het [!DNL SQL] editor en selecteer het rapport `Type` (`Chart` of `Table`). Als u de tekst wilt laten omlopen, selecteert u het dashboard waarin u het rapport wilt opslaan en klikt u op **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Uw gegevens analyseren

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) geeft u de macht om uw Data Warehouse direct te vragen, de resultaten te bekijken, en hen snel om te zetten in een rapport. Gebruiken [!DNL SQL] staat u ook toe [te gebruiken [!DNL SQL] functies die niet beschikbaar zijn](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) in de `Visual` of `Cohort` Report Builder, zodat u meer controle hebt over uw gegevens.

Berekende kolommen gemaakt met [!DNL SQL] zijn niet afhankelijk van updatecycli, wat betekent dat u deze kunt doorlopen zoals u wilt en de resultaten direct kunt zien.

>[!NOTE]
>
>Dit geldt alleen voor de structuur van de kolom, niet voor de versheid van de gegevens. Nieuwe gegevens zijn nog steeds afhankelijk van voltooide updatecycli.

| **Dit is perfect voor...** | **Dat is niet zo geweldig voor...** |
|---|---|
| Tussentijdse/gevorderde analisten | Beginners - u moet het weten [!DNL SQL]. |
| De [!DNL SQL] wreed | Eenvoudige analyses - het schrijven van een vraag kan meer werk dan het eenvoudig gebruiken van [!UICONTROL Visual Report Builder]. |
| Berekende kolommen voor eenmalig gebruik samenstellen | Delen met anderen - overweeg uw publiek: begrijpen ze [!DNL SQL]? Zo niet, dan kunnen ze verward worden door de manier waarop het rapport is opgebouwd. |
| Gegevens met `one-to-many` relaties |  |
| Een nieuwe kolom of analyse testen |  |

#### Resultaten van database versus SQL Editor

Meestal kunnen verschillen in resultaten worden toegeschreven aan updatecycli. Indien [!DNL Commerce Intelligence] is bezig gegevens van uw gegevensbestand aan uw Data Warehouse te herhalen, zou u verschillende resultaten kunnen zien zelfs wanneer het gebruiken van de zelfde vraag.

Verbindingsproblemen kunnen ook tot discrepanties leiden. Ga naar de `Connections` pagina door te klikken **[!DNL Manage Data** > **Connections]** om het uit te zoeken - is er een fout voor de betreffende integratie van de database ? Indien dit het geval is, kan het nodig zijn [de integratie opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) om de zaken weer aan de gang te krijgen.

Als al uw integraties met succes worden verbonden en u niet in het midden van een updatecyclus bent, kan iets anders misleidend zijn.

#### Verwijdert een [!DNL SQL] het rapport ook de onderliggende kolommen van mijn Data Warehouse schrapt?

Nee, u verliest geen kolommen van uw Data Warehouse, ongeacht hoe u ze hebt gemaakt.

Kolommen die zijn gemaakt met de `Data Warehouse Manager` worden niet beïnvloed als u een rapport of een vraag schrapt die hen gebruikt.

Kolommen die zijn gemaakt met de [!DNL SQL Report Builder] niet worden opgeslagen in uw Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

De [!DNL SQL Report Builder] geeft u meer flexibiliteit bij het maken en structureren van uw grafieken. U kunt bijvoorbeeld selecteren welke waarden op de `X` en `Y` assen. Voor meer informatie over het maken van grafieken in het dialoogvenster [!DNL SQL Report Builder], bekijk de [Visualisaties maken van [!DNL SQL] query](../../tutorials/create-visuals-from-sql.md) zelfstudie.

#### `Cohort Report Builder` {#cohortrb}

In tegenstelling tot [!DNL Visual Report Builder]de [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) is bedoeld voor het analyseren en identificeren van gedragstrends van soortgelijke gebruikersgroepen in de loop van de tijd . Met de [!DNL Cohort Report Builder] geen [!DNL SQL] suf, dus je kunt zonder aarzeling naar binnen duiken als je net begint.

| **Dit is perfect voor...** | **Dat is niet zo geweldig voor...** |
|---|---|
| Tussentijdse/gevorderde analisten | Beginners - u hebt praktische cohorten nodig. |
| Gedragstrends in de loop der tijd identificeren | Kwalitatieve analyse - het kan [gedaan](../dev-reports/create-qual-cohort-analysis.md), maar vereist hulp van Adobe. |

## Vragen opnieuw samenstellen na de updatecyclus

U hoeft uw query&#39;s niet opnieuw samen te stellen. Rapporten gemaakt met de [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) worden opgeslagen als in de traditionele `Report Builder`. Het updateproces voor [!DNL SQL] grafieken zijn hetzelfde: nadat uw gegevens zijn bijgewerkt, worden de waarden in uw grafieken opnieuw berekend en weergegeven.

>[!NOTE]
>
>Wanneer u een [!DNL SQL] rapport/vraag, schrapt het niet de onderliggende kolommen van uw Data Warehouse. U verliest geen kolommen, ongeacht hoe u ze hebt gemaakt.

* Kolommen die zijn gemaakt met de Data Warehouse Manager worden niet beïnvloed als u een rapport of query verwijdert waarin ze worden gebruikt.

* Kolommen die zijn gemaakt met de SQL-Report Builder, worden niet opgeslagen in uw Data Warehouse.

## Omloop {#wrapup}

Als u iets een beetje uitdagender wilt proberen, waarom probeert niet het schrijven van een vraag die voor visualisatie wordt geoptimaliseerd? Kijk uit de [Visualisaties maken van [!DNL SQL] naslaggids](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} om aan de slag te gaan.
