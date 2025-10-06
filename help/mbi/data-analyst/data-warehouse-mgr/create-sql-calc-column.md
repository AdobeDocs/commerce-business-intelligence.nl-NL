---
title: Een SQL Berekende kolom maken en gebruiken
description: Leer hoe de geavanceerde kolommen in de vorm van SQL de kolommen van de Berekening op de nieuwe architectuur van Adobe Commerce Intelligence kunnen worden gecreeerd.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Een SQL Berekende kolom maken

Dit onderwerp schetst het doel en het gebruik van het `Calculation` kolomtype, dat aan lijsten kan worden toegevoegd gebruikend de [&#x200B; Manager van Data Warehouse &#x200B;](../data-warehouse-mgr/tour-dwm.md). Hieronder wordt uitgelegd wat SQL-berekeningen doen, waarom ze worden gebruikt, het proces voor het maken van een SQL-berekening en bevat twee voorbeelden.

**Verklaring**

In het verleden konden kolommen die `advanced` werden geacht, alleen worden uitgevoerd door een analist bij het team Klantsucces hier op [!DNL Adobe Commerce Intelligence] . Nu is alle macht in handen van de eindgebruiker, en de geavanceerde kolommen kunnen in de vorm van `SQL Calculation` kolommen op de nieuwe [!DNL Commerce Intelligence] architectuur worden gecreeerd.

Het kolomtype `Calculation` dat nu beschikbaar is als een optie in Data Warehouse Manager, is dezelfde tabelbewerking waarmee u de kolommen in een tabel kunt transformeren met behulp van de PostSQL-logica. De documentatie over de functies en de exploitanten die in het `Calculation` kolomtype kunnen worden gebruikt kan op de website PostgreSQL [&#x200B; hier &#x200B;](https://www.postgresql.org/docs/9.6/functions.html) worden gevonden.

De verschillende kolommen die met de kolom `Calculation` kunnen worden gecreeerd zijn bijna onbeperkt, maar de meeste kolommen kunnen worden gecreeerd gebruikend IF-DEN verklaringen en basisrekenkunde, die in de voorbeelden hieronder wordt gebruikt.

**Voorbeeld 1: Is de laatste orde van de klant?**

De meeste accounts hebben een kolom met de naam `Is customer's last order?` in hun `orders` -tabel om analyses uit te voeren op herhaalde aankoopsnelheden en gekochte klanten. Als uw account zich op de nieuwe architectuur bevindt, wordt deze kolom gemaakt met een `Calculation` -kolom. Deze kolom kan worden weergegeven in de onderstaande schermafbeelding:

![&#x200B; SQL berekende kolomdefinitie voor het identificeren van de laatste orde van de klant &#x200B;](../../assets/Is_customer_s_last_order.png)

De kolom `Is customer's last order?` gebruikt de invoer `Customer's lifetime number of orders` en `Customer's order number` als `A` respectievelijk `B` alias.

De betekenis van PostgreSQL is regel voor regel:

* case: Dit begint een reeks instructies &#39;If&#39;
* als `A` null is of `B` null is, dan null. Als een van de invoerwaarden leeg is, moet de uitvoer ook leeg zijn. Zo voorkomt u SQL-fouten
* als `A=B` then `Yes`: if `Customer's lifetime number of orders` equals `Customer's order number` voor deze rij, dan return `Yes` . Dus als een klant vier bestellingen heeft geplaatst, retourneert de rij voor de vierde bestelling `Yes` for `Is customer's last order?`
* else `No`: als geen van de andere instructies wordt uitgevoerd wanneer aan instructies wordt voldaan, retourneert u `No`
* end: This end the If - then statements

De mogelijke waarden die door deze kolom (`NULL`, `Yes`, `No`) kunnen worden geretourneerd, bevatten niet-numerieke tekens. Het gegevenstype hier is String.

**Voorbeeld 2: Het punt van de orde totale waarde (hoeveelheid * prijs)**

Veel clients analyseren de omzet graag op itemniveau en segmenteren deze op velden zoals `product name` of `category` . De meeste databases geven u niet de inkomsten uit een product in een bestelling, maar leveren de hoeveelheid die in de bestelling wordt verkocht en de prijs van het item.

Voor het analyseren van productinkomsten staat in de meeste accounts een kolom met de naam `Order item total value (quantity * price)` in de tabel `Orders Items` . Als uw account zich op de nieuwe architectuur bevindt, wordt deze kolom ook gebouwd met een `Calculation` -kolom. Deze kolom is zichtbaar in de onderstaande schermafbeelding:

![&#x200B; SQL berekende kolomdefinitie voor de totale waarde van het orde punt &#x200B;](../../assets/Order_item_total_value.png)

In het Commerce-schema gebruikt de kolom `Order item total value (quantity * price)` de invoer `qty ordered` en `base price` alias als `A` respectievelijk `B` .

De waarden die door deze nieuwe kolom worden geretourneerd, zijn in dollars en cent, zodat het juiste gegevenstype `Decimal(10,2)` is.

**Mechanics**

Een nieuwe kolom `Calculation` kan aan een lijst worden toegevoegd door aan **[!DNL Manage Data > Data Warehouse]** te navigeren zoals hieronder getoond:

![&#x200B; mening die van de Lijst berekende kolomresultaten tonen &#x200B;](../../assets/blobid2.png)

Van hieruit kunt u een kolom `Calculation` maken door de onderstaande stappen te volgen:

1. Selecteer de tabel waaraan u de kolom `Calculation` wilt toevoegen.
1. Klik op de juiste tabel **[!UICONTROL Create New Column]** rechtsboven in het scherm.
1. Selecteer in het vervolgkeuzemenu `Select a definition` de optie `Same Table` .
1. Selecteer `Calculation` als de `column definition equation` .
1. Voer de kolomnaam in.
1. Kies de `input` kolommen van de lijst die in de logica voor uw nieuwe kolom worden gebruikt. Elke kolom die u toevoegt, krijgt een letter-alias. De eerste kolom is dus `A`, de tweede kolom is `B` enzovoort.
1. Typ in het venster de PostgreSQL-logica voor de nieuwe kolom met behulp van de letteraliassen van uw invoer. De SQL-berekening moet worden beperkt tot één kolomdefinitie, inclusief alle logica tussen de instructies SELECT en FROM van een SQL-query. SQL de sleutelwoorden die om het even welke inputbrieven gebruiken zouden in kleine letters moeten zijn. Wanneer u bijvoorbeeld de instructie `CASE` gebruikt, moet deze in kleine letters worden geschreven - `case` . Het systeem gaat ervan uit dat een hoofdletter `A` naar een van de invoeren verwijst.
1. Kies het juiste gegevenstype.
   * `Integer` - Het gehele getal
   * `Decimal(10,2)` - een decimaal getal met 10 totale cijfers, waarvan 2 rechts van het decimaalteken staan
   * `String` - Elk type tekst of reeks tekens die niet-getallen gebruiken
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` -indeling

1. Klik op **[!UICONTROL test column]**. Hierdoor wordt een lijst met vijf testwaarden gegenereerd voor elk van uw inputs en wordt het resultaat van de logica uit stap 6 voor elke set testwaarden weergegeven. Als een gedeelte van de SQL een fout genereert, wordt het juiste foutbericht geretourneerd. Voorbeeldresultaten kunnen alleen worden gegenereerd als alle invoerkolommen native velden zijn. Als om het even welke inputkolommen worden berekend kolommen, moet u de resultaten bevestigen door de kolom aan metrisch toe te voegen en in Visual Report Builder te bekijken

1. Klik op **[!UICONTROL Save]** als u tevreden bent met het resultaat. De kolom schakelt voor gebruik in.
