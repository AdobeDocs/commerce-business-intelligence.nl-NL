---
title: Berekende kolommen maken
description: Leer hoe u gegevens uit verschillende bronnen kunt consolideren.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Berekende kolommen maken

Bij het analyseren van uw gegevens is het nuttig om gegevens uit verschillende bronnen te consolideren. Wilt u de omzet groeperen door de bron van de overname, de gegevens van uw `orders` tabel en [!DNL Google Analytics] gegevens te koppelen? Misschien wilt u opbrengst groeperen door klantengeslacht of zich bij een klantenattribuut aan transactiegegevens voor segmentatie aansluiten. In dit onderwerp wordt besproken hoe dat moet gebeuren.

Alvorens begonnen te worden, adviseert de Adobe dat u de [ Berekende Gids van de Types van Kolom ](../../data-analyst/data-warehouse-mgr/calc-column-types.md) voor informatie over de types van kolommen herziet die u in de Manager van de Data Warehouse, samen met hun definities en voorbeelden kunt tot stand brengen.

1. Klik op **[!DNL Manage Data > Data Warehouse]** om te beginnen.

1. Klik op de tabel waarin u een kolom wilt maken. Als u bijvoorbeeld een kolom `Customer Gender` wilt maken voor inkomstensegmentatie, selecteert u de tabel `sales_flat_order` .

1. Het tabelschema wordt weergegeven. Klik op **[!UICONTROL Create New Column]**.

1. Geef uw kolom een naam. Bijvoorbeeld `Customer Gender` .

1. Selecteer de definitie voor de kolom. Dit is waar de [ Berekende gids van de Types van Kolom ](../data-warehouse-mgr/calc-column-types.md) in handvat komt!

1. Voor bepaalde typen kolommen is iets meer informatie nodig om de kolom correct te maken:

   * Voor `One to Many` (aangesloten bij) en `Many to One` (samengevoegde) kolommen, moet u de lijsten en de kolommen selecteren.

   * Voor een `Same Table calculation` moet u het gewenste datumveld in de vervolgkeuzelijst selecteren.

Als u een kolom `One to Many` (lid van) of `Many to One` (geaggregeerd) maakt, moet u een pad selecteren om de twee tabellen met elkaar te verbinden. In deze stap kunt u een bestaand pad gebruiken of een pad maken.

>[!NOTE]
>
>Vergeet niet de tabel op de juiste manier als een of meerdere tabellen te definiëren.

* Indien gewenst, kunt u [ filters ](../../data-user/reports/ess-manage-data-filters.md) op de nieuwe kolom toepassen.

* Klik op **[!UICONTROL Save]** als u klaar bent.

Uw nieuwe kolom verschijnt in de huidige lijst met een `Pending` status. Nadat de volgende update is voltooid, is uw kolom beschikbaar voor gebruik in metriek en rapporten.

## Handmatige verwijzingskaart {#map}

Als u moeite hebt zich te herinneren wat alle input wanneer het creëren van een berekende kolom zijn, probeer handig deze verwijzingskaart te houden wanneer u bouwt:

![](../../assets/Calculated_Columns_Example.png)

## Gerelateerde documentatie

* [Berekende kolomtypen](../data-warehouse-mgr/calc-column-types.md)
* [Geavanceerde berekende kolomtypen](../data-warehouse-mgr/adv-calc-columns.md)
* [De bouw  [!DNL Google ECommerce]  dimensies met orde en klantengegevens](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
