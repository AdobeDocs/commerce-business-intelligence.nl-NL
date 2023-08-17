---
title: Een SQL Berekende kolom maken en gebruiken
description: Leer hoe u geavanceerde kolommen kunt maken in de vorm van SQL-berekeningskolommen op de nieuwe Adobe Commerce Intelligence-architectuur.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Een SQL Berekende kolom maken

Dit onderwerp schetst het doel en het gebruik van `Calculation` kolomtype, dat met de opdracht [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). Hieronder wordt uitgelegd wat SQL-berekeningen doen, waarom ze worden gebruikt, het proces voor het maken van een SQL-berekening en bevat twee voorbeelden.

**Toelichting**

In het verleden werden kolommen die `advanced` kan alleen worden uitgevoerd door een analist van het Customer Success-team hier op [!DNL Adobe Commerce Intelligence]. Nu is al macht in de handen van het eind - gebruiker, en de geavanceerde kolommen kunnen in de vorm van worden gecreeerd `SQL Calculation` kolommen over de nieuwe [!DNL Commerce Intelligence] architectuur.

De `Calculation` kolomtype, nu beschikbaar als optie in de Manager van de Data Warehouse, is een zelfde lijstverrichting die u toestaat om de kolommen op een lijst om te zetten gebruikend logica PostgreSQL. Documentatie over de functies en operatoren die in de `Calculation` het kolomtype is te vinden op de website PostgreSQL [hier](https://www.postgresql.org/docs/9.6/functions.html).

De verschillende kolommen die kunnen worden gemaakt met de `Calculation` de kolom is bijna onbeperkt, maar de meeste kolommen kunnen worden tot stand gebracht gebruikend IF-THEN verklaringen en basisrekenkunde, die in de voorbeelden hieronder wordt gebruikt.

**Voorbeeld 1: Is de laatste bestelling van de klant?**

De meeste accounts hebben een kolom met de naam `Is customer's last order?` op hun `orders` tabel voor het uitvoeren van analyses op herhaalde aankooppercentages en gekochte klanten. Als uw account zich op de nieuwe architectuur bevindt, wordt deze kolom gemaakt met een `Calculation` kolom en kunt u zien in de onderstaande schermafbeelding:

![](../../assets/Is_customer_s_last_order.png)

De `Is customer's last order?` de kolom gebruikt de input `Customer's lifetime number of orders` en `Customer's order number` alias `A` en `B` respectievelijk.

De betekenis van PostgreSQL is regel voor regel:

* case: Dit begint een reeks instructies &#39;If&#39;
* wanneer `A` is null of `B` is null dan null: Als een van de invoerwaarden leeg is, moet de uitvoer ook leeg zijn. Zo voorkomt u SQL-fouten
* wanneer `A=B` dan `Yes`: if `Customer's lifetime number of orders` equals `Customer's order number` voor deze rij, dan terugkeer `Yes`. Dus als een klant vier orders heeft geplaatst, zou de rij voor hun vierde orde terugkeren `Yes` for `Is customer's last order?`
* else `No`: Als geen van de andere instructies wordt uitgevoerd wanneer aan instructies wordt voldaan, retourneert u `No`
* end: This end the If - then statements

De mogelijke waarden die door deze kolom kunnen worden geretourneerd (`NULL`, `Yes`, `No`) bevat niet-numerieke tekens, dus het gegevenstype hier is String.

**Voorbeeld 2: Volgitem totale waarde (hoeveelheid * prijs)**

Veel clients analyseren de inkomsten op itemniveau en segmenteren deze op velden zoals `product name` of `category`. De meeste databases geven u niet de inkomsten uit een product in een bestelling, maar leveren de hoeveelheid die in de bestelling wordt verkocht en de prijs van het item.

Om de analyses van de productopbrengst toe te laten, hebben de meeste rekeningen een kolom genoemd `Order item total value (quantity * price)` op hun `Orders Items` tabel. Als uw account zich op de nieuwe architectuur bevindt, wordt deze kolom ook gebouwd met een `Calculation` kolom en kunt u zien in de onderstaande schermafbeelding:

![](../../assets/Order_item_total_value.png)

In het schema Handel `Order item total value (quantity * price)` de kolom gebruikt de input `qty ordered` en `base price` alias `A` en `B` respectievelijk.

De waarden die door deze nieuwe kolom worden geretourneerd, zijn in dollars en cent, zodat het juiste gegevenstype is `Decimal(10,2)`.

**Mechanica**

Een nieuwe `Calculation` kolom kan aan een lijst worden toegevoegd door te navigeren aan **[!DNL Manage Data > Data Warehouse]** zoals hieronder weergegeven:

![](../../assets/blobid2.png)

Van hieruit kunt u een `Calculation` kolom door de onderstaande stappen te volgen:

1. Selecteer de tabel waaraan u de `Calculation` kolom.
1. Klik in de juiste tabel op **[!UICONTROL Create New Column]** rechtsboven in het scherm.
1. Van de `Select a definition` vervolgkeuzelijst, selecteren `Same Table`.
1. Selecteren `Calculation` als de `column definition equation`.
1. Voer de kolomnaam in.
1. Kies de optie `input` kolommen uit de lijst die in de logica voor uw nieuwe kolom worden gebruikt. Elke kolom die u toevoegt, krijgt een letter alias, dus de eerste kolom is `A`de tweede is `B` enzovoort.
1. Typ in het venster de PostgreSQL-logica voor de nieuwe kolom met behulp van de letteraliassen van uw invoer. De SQL-berekening moet worden beperkt tot één kolomdefinitie, inclusief alle logica tussen de instructies SELECT en FROM van een SQL-query. SQL de sleutelwoorden die om het even welke inputbrieven gebruiken zouden in kleine letters moeten zijn. Als u bijvoorbeeld de opdracht `CASE` verklaring, moet het in kleine letters worden geschreven - `case`. Het systeem gaat ervan uit dat een hoofdletter `A` verwijst naar een van de inputs.
1. Kies het juiste gegevenstype.
   * `Integer` - Het gehele getal
   * `Decimal(10,2)` - een decimaal getal met 10 totale cijfers, waarvan 2 rechts van het decimaalteken
   * `String` - Elk type tekst of reeks tekens die niet-getallen gebruiken
   * `Datetime` - yyyy-MM-dd hh:mm:ss-indeling

1. Klik op **[!UICONTROL test column]**. Hierdoor wordt een lijst met vijf testwaarden gegenereerd voor elk van uw inputs en wordt het resultaat van de logica uit stap 6 voor elke set testwaarden weergegeven. Als een gedeelte van de SQL een fout genereert, wordt het juiste foutbericht geretourneerd. Voorbeeldresultaten kunnen alleen worden gegenereerd als alle invoerkolommen native velden zijn. Als om het even welke inputkolommen worden berekend kolommen, moet u de resultaten bevestigen door de kolom aan metrisch toe te voegen en in de Visuele Report Builder te bekijken

1. Als u tevreden bent met het resultaat, klikt u op **[!UICONTROL Save]**. De kolom schakelt voor gebruik in.
