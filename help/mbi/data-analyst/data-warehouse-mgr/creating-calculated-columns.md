---
title: Berekende kolommen maken
description: Leer hoe u gegevens uit verschillende bronnen kunt consolideren.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# Berekende kolommen maken

Bij het analyseren van uw gegevens is het nuttig om gegevens uit verschillende bronnen te consolideren. Wilt u opbrengsten groeperen door bron van de verwerving, gegevens van uw orderlijst en Google Analytics te koppelen? Of hoe te over het groeperen van opbrengst door klantengeslacht, of het aansluiten van een klantenattribuut aan transactiegegevens voor segmentatie?

Deze gids leert je hoe je dat doet. Voordat u aan de slag gaat, raadt Adobe u aan de [Gids voor berekende kolomtypen](../../data-analyst/data-warehouse-mgr/calc-column-types.md). De _Gids voor berekende kolomtypen_ schetst de types van kolommen die u in de Manager van de Data Warehouse, samen met hun definities en voorbeelden kunt tot stand brengen.

1. Klik op **[!DNL Manage Data > Data Warehouse]** in de zijbalk.

1. Klik op de tabel waarin u een kolom wilt maken. Als u bijvoorbeeld een `Customer Gender` kolom voor inkomstensegmentatie, zou u selecteren `sales_flat_order` tabel.

1. Het tabelschema wordt weergegeven. Klikken **[!UICONTROL Create New Column]**.

1. Geef uw kolom een naam, bijvoorbeeld `Customer Gender`.

1. Selecteer de definitie voor de kolom. Dit is waar de [Hulplijn Berekende kolomtypen](../data-warehouse-mgr/calc-column-types.md) is handig!

1. Voor bepaalde typen kolommen is iets meer informatie nodig om de kolom correct te maken:
   * Voor `One to Many` (lid) en `Many to One` (geaggregeerde) kolommen, moet u de tabellen en kolommen selecteren.
   * Voor een `Same Table calculation`selecteert u het gewenste datumveld in het vervolgkeuzemenu.

Als u een `One to Many` (lid) of `Many to One` (bijeengevoegde) kolom, moet u een weg selecteren om de twee lijsten te verbinden. In deze stap kunt u een bestaand pad gebruiken of een pad maken.

>[!NOTE]
>
>Vergeet niet de tabel op de juiste manier als een of meerdere tabellen te definiëren.

* U kunt desgewenst toepassen [filters](../../data-user/reports/ess-manage-data-filters.md) naar de nieuwe kolom.
* Als u klaar bent, klikt u op **[!UICONTROL Save]**.

Dat is het! Uw nieuwe kolom verschijnt in de huidige lijst met a `Pending` status. Nadat de volgende update is voltooid, is uw kolom beschikbaar voor gebruik in metriek en rapporten.

## Handmatige verwijzingskaart {#map}

Als u een beetje moeite hebt zich te herinneren wat alle input wanneer het creëren van een berekende kolom zijn, probeer behoudend deze verwijzingskaart handig wanneer u bouwt:

![](../../assets/Calculated_Columns_Example.png)

## Gerelateerde documentatie

* [Berekende kolomtypen](../data-warehouse-mgr/calc-column-types.md)
* [Geavanceerde berekende kolomtypen](../data-warehouse-mgr/adv-calc-columns.md)
* [Gebouw [!DNL Google ECommerce] afmetingen met bestelling en klantgegevens](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
