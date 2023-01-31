---
title: Opbouwen[!DNL Google ECommerce]afmetingen
description: Leer dimensies te bouwen die uw gegevens van de eCommerce met uw orden en klantengegevens zullen verbinden.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Opbouwen [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

Nu bent u klaar [verbinden uw[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), wat kunt u doen met die gegevens in [!DNL MBI]? In dit artikel, lopen wij u door bouwdimensies die uw gegevens van de eCommerce met uw orden en klantengegevens zullen verbinden.

Met de afmetingen die we behandelen, kunt u analyses maken die [belangrijke vragen beantwoorden over uw marketingkanalen en -campagnes](../../data-analyst/analysis/most-value-source-channel.md). Welk percentage van opbrengst komt uit elke bron? Hoe vergelijk de levensduurwaarde van Facebook-klanten met die van? [!DNL Google]?

## Voorwaarden en overzicht

Als u de afmetingen in dit artikel wilt maken, hebt u een [!DNL Google ECommerce] tabel `orders` en een `customers` tabel. Deze tabellen moeten [gesynchroniseerd met uw gegevenspakhuis](../../data-analyst/data-warehouse-mgr/tour-dwm.md) voordat de afmetingen kunnen worden opgebouwd. Tabellen die worden gesynchroniseerd, worden weergegeven in het dialoogvenster `Synced Tables` van de `Data Warehouse Manager`.

Hier volgt een snelle blik bij het synchroniseren van lijsten en kolommen als u een verfrisser nodig hebt:

![](../../assets/Syncing_New_Columns.gif)

Nadat u een samenvoeging hebt gemaakt met de `orders` aan de [!DNL Google eCommerce] in de tabel hieronder worden de eerste drie dimensies gemaakt. Vervolgens gebruiken we die dimensies om drie gebruikers-/klantdimensies te maken in de `customers` tabel. Als u klaar bent, voegen we deze kolommen bij de `orders` tabel.

Hier zijn de dimensies die we behandelen:

* **Orderentabel**

* Bestelling [!DNL Google Analytics] bron
* Bestelling [!DNL Google Analytics] medium
* Bestelling [!DNL Google Analytics]Een campagne
* Eerste bestelling van de klant [!DNL Google Analytics] bron
* Eerste bestelling van de klant [!DNL Google Analytics] medium
* Eerste bestelling van de klant [!DNL Google Analytics] campagne

* **Klantentabel**

* Eerste bestelling van de klant [!DNL Google Analytics] bron
* Eerste bestelling van de klant [!DNL Google Analytics] medium
* Eerste bestelling van de klant [!DNL Google Analytics] campagne

## De afmetingen opbouwen

Als u dimensies wilt maken, opent u het dialoogvenster [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) door te klikken **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabel met bestellingen, rond 1

In dit voorbeeld bouwen wij **Bestelling [!DNL Google Analytics] Bron** dimensie.

1. Van de lijst van lijsten in de Data Warehouse, klik de lijst (in ons geval, `orders`) die uw bestelgegevens bevat.
1. Klikken **[!UICONTROL Create a Column]**.
1. Geef de kolom een naam.
1. Selecteren `Joined Column` van de [vervolgkeuzelijst voor definities](../data-warehouse-mgr/calc-column-types.md). In dit voorbeeld werken we met een [één-op-één relatie](../data-warehouse-mgr/table-relationships.md), overeenkomstig de `eCommerce.transactionID` kolom naar exact één rij van de `orders` tabel.
1. Daarna, moeten wij de weg bepalen, of hoe de lijst en de kolom die worden gebruikt worden verbonden. Klik op de knop `Select a table and column` vervolgkeuzelijst.
1. De weg die we nodig hebben is niet beschikbaar, dus moeten we een nieuwe uitstippelen. Klikken **[!UICONTROL Create new Path]**.
1. In het venster dat wordt weergegeven, stelt u de `Many` zijde naar `orders.order\_id`of de kolom in de `orders` tabel die de volgorde-id bevat.
1. Op de `One` zijde, zoek de `Google ECommerce` tabel, en stel vervolgens de kolom in op `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Klikken **[!UICONTROL Save]** om het pad te maken.
1. Nadat het pad is toegevoegd, klikt u op de knop **[!UICONTROL Select table and column]** weer neerzetten.
1. Zoek de `ECommerce` en klik vervolgens op de knop `Source` kolom. Hierdoor worden de orders aan de broninformatie gekoppeld.
1. Als u weer in het tabelschema bent, klikt u op **[!UICONTROL Save]** opnieuw om de dimensie te creëren.

Hier is een blik op het hele proces:

![](../../assets/help_center.gif)

Probeer het daarna opnieuw **Bestelling [!DNL Google Analytics] medium** en `campaign`. Niet veel zal veranderen voor deze dimensies, dus geef het een poging. Maar als je vastzit, kun je uitchecken [het einde van dit artikel](#stuck) om te zien wat anders is.

### Klantentabel {#customers}

In dit voorbeeld bouwen wij **Eerste bestelling van de klant [!DNL Google Analytics] bron** dimensie.

1. Van de lijst van lijsten in de Data Warehouse, klik de lijst (in ons geval, `customers`) die uw klantgegevens bevat.
1. Klikken **[!UICONTROL Create a Column]**.
1. Geef de kolom een naam.
1. In dit voorbeeld selecteren we de `is MAX` van de [vervolgkeuzelijst voor definities](../../data-analyst/data-warehouse-mgr/calc-column-types.md). De `is MIN` definitie kan ook werken als deze wordt toegepast op een tekstkolom met slechts één mogelijke waarde. Het belangrijkste onderdeel is dat er goede filters worden ingesteld, wat we later doen.
1. Klik op de knop **[!UICONTROL Select a table and column]** vervolgkeuzelijst en selecteert u de `orders` tabel, dan de `Order's [!DNL Google Analytics] source` kolom.
1. Klikken **[!UICONTROL Save]**.
1. Als u weer in het tabelschema bent, klikt u op de knop `Options` vervolgkeuzelijst, vervolgens `Filters`.
1. Klikken **[!UICONTROL Add Filter Set]** en selecteer vervolgens de `Orders we count` set. We willen alleen orders opnemen in de bestellingen waarvan we het filter tellen. Daarom is het belangrijk dat deze filterset wordt geselecteerd.
1. Klikken **[!UICONTROL Add Filter]**. We willen de eerste bestelling van de klant vinden [!DNL Google Analytics] bron, dus moeten wij een filter toevoegen:

   _orders.bestelnummer van de klant = 1

   _
1. Klikken **[!UICONTROL Save]** om de dimensie te maken.

Probeer het daarna opnieuw **Eerste bestelling van de klant [!DNL Google Analytics] medium** en `campaign`. Niet veel zal veranderen voor deze dimensies, dus geef het een poging. Maar als je vastzit, kun je uitchecken [het einde van dit artikel](#stuck) om te zien wat anders is.

### Bonus: Orders table, round 2

U kunt hier stoppen als u wilt, maar deze sectie maakt verdere analyse mogelijk door de **Eerste bestelling van de klant [!DNL Google Analytics] afmetingen** in het [laatste sectie](#customers) in de `orders` tabel. Door de afmetingen in deze sectie te maken, kunt u alle op uw `orders` tabel - `Revenue`, `Number of orders`, `Distinct buyers`, enzovoort, het gebruik van de [!DNL Google Analytics] kenmerken van de eerste bestelling van een klant.

In dit voorbeeld sluiten we ons aan bij de `Customer's first order's [!DNL Google Analytics] source` de `orders` tabel.

1. Van de lijst van lijsten in de Data Warehouse, klik de lijst (in ons geval, `orders`) die uw bestelgegevens bevat.
1. Klikken **[!UICONTROL Create a Column]**.
1. Geef de kolom een naam.
1. Selecteren `Joined Column` in het keuzemenu met definities. Hierdoor worden de klantdimensies die u in de vorige sectie hebt gemaakt, samengevoegd met de `orders` tabel.
1. Klik op de knop **[!UICONTROL Select a table and column]** vervolgkeuzelijst, selecteert u vervolgens de `customers` en de `Customer's first order's [!DNL Google Analytics] source` kolom.
1. Als een pad niet automatisch wordt ingevuld, selecteert u het pad dat de klanten het beste verbindt en de tabellen bestelt.
1. Klikken **[!UICONTROL Save]** om de dimensie te maken.

Hier is een blik op het hele proces:

![](../../assets/help_center2.gif)

Voltooien door deel te nemen aan de `Customer's first order's` medium en `campaign` de `orders` tabel. Geef het een poging, en zoals we al eerder hebben gezegd, controleer het [het einde van het artikel](#stuck) als u hulp nodig hebt.

### Omloop omhoog

We zijn klaar met het maken van de dimensies, wat betekent dat we nu krachtige analyses kunnen maken die de prestaties van onze verschillende kanalen en campagnes volgen. We weten dat u graag aan de slag wilt, maar vergeet niet **nieuwe kolommen zijn pas beschikbaar nadat de volgende update is voltooid**.

We hebben enkele van de populairste dimensies in dit artikel behandeld, maar de lucht is de grens - probeer zelf te creëren of voel ons vrij om ons te pingelen als u hulp wilt zoeken bij het verkennen van andere opties. 

### Ik zit vast! wat is anders ? {#stuck}

**`Orders`tabel 1:** Wanneer u het `Order's [!DNL Google Analytics]` medium en `campaign` de afmetingen, is het verschil de kolommen die in stap 12 worden geselecteerd. In ons voorbeeld was de kolom `Source`.

**`Customers`tabel:** Wanneer u het `Customer's first order's [!DNL Google Analytics]` medium en `campaign` de afmetingen, is het verschil de kolommen die in stap 5 worden geselecteerd. In ons voorbeeld was de kolom `Order's [!DNL Google Analytics]` bron.

**`Orders`tabel 2:** Wanneer u de `Customer's first order's [!DNL Google Analytics]` medium en `campaign` kolommen naar de `orders` het verschil is tussen de kolommen die in stap 5 zijn geselecteerd. In ons voorbeeld was de kolom `Customer's first order's [!DNL Google Analytics]` bron.
