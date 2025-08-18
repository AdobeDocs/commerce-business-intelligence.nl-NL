---
title: Visualisaties maken van SQL-query's
description: Leer u vertrouwd te maken met de terminologie die in SQL Report Builder wordt gebruikt en geef u een stevige basis voor het maken van SQL-visualisaties.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Visualisaties maken van SQL-query&#39;s

Het doel van deze zelfstudie is om u vertrouwd te maken met de terminologie die in de [!DNL SQL Report Builder] wordt gebruikt en u een solide basis te geven voor het maken van `SQL visualizations` .

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) is een rapportbouwer met opties: u kunt een vraag voor het enige doel in werking stellen om een lijst van gegevens terug te winnen, of u kunt die resultaten in een rapport veranderen. In deze zelfstudie wordt uitgelegd hoe u een visualisatie maakt op basis van een SQL-query.

## Terminologie

Voordat u met deze zelfstudie begint, raadpleegt u de volgende terminologie die in de `SQL Report Builder` wordt gebruikt.

- `Series`: De kolom die u wilt meten, wordt bedoeld als Serie in SQL Report Builder. Algemene voorbeelden zijn `revenue` , `items sold` en `marketing spend` . Ten minste één kolom moet als een `Series` worden ingesteld om een visualisatie te maken.

- `Category`: De kolom die u wilt gebruiken om uw gegevens te segmenteren, wordt een `Category` Dit is net als de functie `Group By` in de [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) . Bijvoorbeeld, als u de levenopbrengst van uw klanten door hun aanschafbron wilt segmenteren, zou de kolom die aanschafbron bevat als `Category` worden gespecificeerd. U kunt meerdere kolommen instellen als een `Category` .

>[!NOTE]
>
>Datums en tijdstempels kunnen ook worden gebruikt als `Categories` . Zij zijn enkel een kolom van gegevens in uw vraag en moeten worden geformatteerd en worden bevolen zoals gewenst in de vraag zelf.

- `Labels`: deze worden toegepast als labels op de x-as. Wanneer het analyseren van gegevenstrending in tijd, worden de jaar en maandkolommen gespecificeerd als etiketten. Er kunnen meerdere kolommen worden ingesteld op Label.

## Stap 1: Schrijf de Vraag

Houd rekening met het volgende:

- [!DNL SQL Report Builder] gebruikt [`Redshift SQL` ](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Als u een rapport met een tijdreeks maakt, moet u de tijdstempelkolom(men) `ORDER BY` gebruiken. Dit zorgt ervoor dat de tijdstempels in de juiste volgorde in het rapport worden uitgezet.

- De functie `EXTRACT` is ideaal om te gebruiken voor het ontleden van de dag, de week, de maand, of het jaar van timestamp. Dit is handig wanneer de `time interval` die u voor het rapport wilt gebruiken `daily` , `weekly` , `monthly` of `yearly` is.

Open om te beginnen de [!DNL SQL Report Builder] door op **[!UICONTROL Report Builder** > **SQL Report Builder]** te klikken.

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

Met deze resultaten, *hoe creeert u de visualisatie?* Klik om aan de slag te gaan op de tab **[!UICONTROL Chart]** in het deelvenster `Results` . Hierdoor wordt de tab `Chart settings` weergegeven.

Wanneer een vraag eerst wordt uitgevoerd, kan het rapport onscrubable kijken omdat alle kolommen in de vraag als reeks worden uitgezet:

![](../assets/SQL_initial_report_results.png)

In dit voorbeeld wilt u dat dit een lijngrafiek wordt die zich in de loop van de tijd ontwikkelt. Gebruik de volgende instellingen om het bestand te maken:

- `Series`: selecteer de kolom `Items sold` als de `Series` omdat u deze wilt meten. Nadat u een `Series` kolom bepaalt, zult u één enkele lijn zien die in het rapport wordt geplot.

- `Category`: In dit voorbeeld wilt u elk product als een andere regel in het rapport bekijken. Hiervoor stelt u `Product name` in als de `Category` .

- `Labels`: gebruik de kolommen `year` en `month` als labels op de x-as om `Items Sold` in de loop van de tijd als een trending te kunnen weergeven.

>[!NOTE]
>
>De vraag moet een `ORDER BY` clausule op de etiketten bevatten als zij `date` zijn/ `time` kolommen.

Hieronder volgt een snel overzicht van hoe u deze visualisatie creeerde, van het runnen van de vraag aan vestiging het rapport:

![](../assets/SQL_report_settings.gif)

## Stap 3: Selecteer een `Chart Type`

In dit voorbeeld wordt het diagramtype `Line` gebruikt. Als u een andere `chart type` wilt gebruiken, klikt u op de pictogrammen boven de sectie met grafiekopties om deze te wijzigen:

![](../assets/Chart_types.png)

## Stap 4: De visualisatie opslaan

Als u dit rapport opnieuw wilt gebruiken, geeft u het rapport een naam en klikt u op **[!UICONTROL Save]** in de rechterbovenhoek.

Selecteer in het vervolgkeuzemenu `Chart` als `Type` en vervolgens als dashboard om het rapport in op te slaan.

## Omloop omhoog

Wilt u een stap verder gaan? Controle uit de [ beste praktijken van de vraagoptimalisering ](../best-practices/optimizing-your-sql-queries.md).
