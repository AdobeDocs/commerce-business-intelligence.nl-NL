---
title: Visualisaties maken van SQL-query's
description: Leer om u met de terminologie vertrouwd te maken die in SQL Report Builder wordt gebruikt en u een stevige stichting te geven voor het creëren van SQL visualisaties.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Visualisaties maken van SQL-query&#39;s

Het doel van deze zelfstudie is om u vertrouwd te maken met de terminologie die wordt gebruikt in het dialoogvenster [!DNL SQL Report Builder] en u een solide basis geven voor het maken van `SQL visualizations`.

De [[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) is een rapportbouwer met opties: u kunt een vraag voor het enige doel in werking stellen om een lijst van gegevens terug te winnen, of u kunt die resultaten in een rapport veranderen. In deze zelfstudie wordt uitgelegd hoe u een visualisatie maakt op basis van een SQL-query.

## Terminologie

Voordat u met deze zelfstudie begint, raadpleegt u de volgende terminologie die in het dialoogvenster `SQL Report Builder`.

- `Series`: De kolom die u wilt meten wordt bedoeld als Reeks in SQL Report Builder. Algemene voorbeelden `revenue`, `items sold`, en `marketing spend`. Ten minste één kolom moet als een `Series` om een visualisatie te maken.

- `Category`: De kolom u wilt gebruiken om uw gegevens te segmenteren wordt genoemd a `Category` Dit is net als `Group By` in de [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Bijvoorbeeld, als u de levenopbrengst van uw klanten door hun verwervingsbron wilt segmenteren, zou de kolom die verwervingsbron bevat als worden gespecificeerd `Category`. Er kunnen meerdere kolommen als een kolom worden ingesteld `Category`.

>[!NOTE]
>
>Datums en tijdstempels kunnen ook worden gebruikt als `Categories`. Zij zijn enkel een kolom van gegevens in uw vraag en moeten worden geformatteerd en worden bevolen zoals gewenst in de vraag zelf.

- `Labels`: Deze worden toegepast als labels op de x-as. Wanneer het analyseren van gegevenstrending in tijd, worden de jaar en maandkolommen gespecificeerd als etiketten. Er kunnen meerdere kolommen worden ingesteld op Label.

## Stap 1: De query schrijven

Houd rekening met het volgende:

- De [!DNL SQL Report Builder] gebruik [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Als u een rapport met een tijdreeks maakt, moet u `ORDER BY` de tijdstempelkolom(men). Dit zorgt ervoor dat de tijdstempels in de juiste volgorde in het rapport worden uitgezet.

- De `EXTRACT` Deze functie is handig voor het parseren van de dag, week, maand of het jaar van de tijdstempel. Dit is handig wanneer de `time interval` u wilt gebruiken voor het rapport: `daily`, `weekly`, `monthly`, of `yearly`.

Om te beginnen, open omhoog [!DNL SQL Report Builder] door te klikken **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Neem bijvoorbeeld deze query in overweging die het maandelijkse totale aantal verkochte items voor elk product retourneert:

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

Deze vraag keert deze lijst van resultaten terug:

![](../assets/SQL_results_table.png)

## Stap 2: De visualisatie maken

Met deze resultaten *hoe maak je de visualisatie ?* Klik op de knop **[!UICONTROL Chart]** in de `Results` venster. Hierdoor wordt het dialoogvenster `Chart settings` tab.

Wanneer een vraag eerst wordt uitgevoerd, kan het rapport onscrubable kijken omdat alle kolommen in de vraag als reeks worden uitgezet:

![](../assets/SQL_initial_report_results.png)

In dit voorbeeld wilt u dat dit een lijngrafiek wordt die zich in de loop van de tijd ontwikkelt. Gebruik de volgende instellingen om het bestand te maken:

- `Series`: Selecteer `Items sold` kolom als de `Series` omdat je het wilt meten. Nadat u een `Series` kolom, zult u één enkele lijn zien die in het rapport wordt geplot.

- `Category`: Voor dit voorbeeld, wilt u elk product als verschillende lijn in het rapport bekijken. Hiervoor stelt u `Product name` als de `Category`.

- `Labels`: De kolommen gebruiken `year` en `month` als labels op de x-as om te kunnen bekijken `Items Sold` in de loop van de tijd.

>[!NOTE]
>
>De query moet een `ORDER BY` clausule op de etiketten indien deze `date`/`time` kolommen.

Hieronder volgt een snel overzicht van hoe u deze visualisatie creeerde, van het runnen van de vraag aan vestiging het rapport:

![](../assets/SQL_report_settings.gif)

## Stap 3: Selecteer een `Chart Type`

In dit voorbeeld wordt het `Line` diagramtype. Een andere `chart type`Klik op de pictogrammen boven de sectie met grafiekopties om deze te wijzigen:

![](../assets/Chart_types.png)

## Stap 4: De visualisatie opslaan

Als u dit rapport opnieuw wilt gebruiken, geeft u het rapport een naam en klikt u op **[!UICONTROL Save]** in de rechterbovenhoek.

Selecteer in het vervolgkeuzemenu de optie `Chart` als de `Type` en dan een dashboard om het rapport aan te slaan.

## Omloop omhoog

Wilt u een stap verder gaan? Kijk uit de [best practices voor queryoptimalisatie](../best-practices/optimizing-your-sql-queries.md).
