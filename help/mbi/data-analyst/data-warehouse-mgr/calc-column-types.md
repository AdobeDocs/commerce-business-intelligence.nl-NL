---
title: Berekende kolomtypen
description: Leer hoe u kolommen maakt om uw gegevens te vergroten en te optimaliseren voor analyse.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# Berekende kolomtypen

* [Dezelfde tabelberekeningen](#sametable)
* [Eén tot veel berekeningen](#onetomany)
* [Veel berekeningen](#manytoone)
* [Handmatige verwijzingskaart](#map)
* [Geavanceerde berekende kolommen](#advanced)

Binnen de [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md)kunt u kolommen maken om uw gegevens te vergroten en te optimaliseren voor analyse. [Deze functionaliteit](../data-warehouse-mgr/creating-calculated-columns.md) kan worden betreden door om het even welke lijst in de Manager van de Data Warehouse te selecteren en te klikken **[!UICONTROL Create New Column]**.

Dit onderwerp beschrijft de types van kolommen die u met de Manager van de Data Warehouse kunt tot stand brengen. Het omvat ook de beschrijving, een visuele doorloop van die kolom, en een [referentiekaart](#map) van alle inputs die nodig zijn om een kolom te maken. U kunt op drie manieren berekende kolommen maken:

1. [Dezelfde tabel berekende kolommen](#sametable)
1. [Een-op-veel berekende kolommen](#onetomany)
1. [Vele-aan-één berekende kolommen](#manytoone)

## Dezelfde tabel berekende kolommen {#sametable}

Deze kolommen worden gebouwd gebruikend inputkolommen van de zelfde lijst.

### Leeftijd {#age}

Een pagina berekende kolom keert het aantal seconden tussen de huidige tijd en wat inputtijd terug.

In het onderstaande voorbeeld worden `Seconds since customer's most recent order` in de `customers` tabel. Dit kan worden gebruikt om gebruikerslijsten samen te stellen van klanten die geen aankopen hebben gedaan (soms doorverwezen naar als inkopen) binnen `X days`.

![](../../assets/age.gif)

### Valuta-converter

Een berekende valutacoconverter zet de native valuta van een kolom om in een gewenste nieuwe valuta.

In het onderstaande voorbeeld worden `base\_grand\_total In AED`, de `base\_grand\_total` van het is een native valuta naar het AED in de `sales\_flat\_order` tabel. Deze kolom werkt goed voor winkels met meerdere valuta&#39;s die in hun lokale valuta willen rapporteren.

Voor handelscliënten, `base\_currency\_code` in het veld worden doorgaans native valuta&#39;s opgeslagen. De `Spot Time` Dit veld moet overeenkomen met de datum die wordt gebruikt in uw metriek.

![](../../assets/currency_converter.png)

## Een-op-veel berekende kolommen {#onetomany}

`One-to-Many` kolommen [gebruiken een pad tussen twee tabellen](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Dit pad impliceert altijd één tabel, waar een kenmerk woont, en een vele tabel, waar dat kenmerk naar beneden wordt verplaatst. Het pad kan worden beschreven als een `foreign key--primary key` relatie.

### Samengevoegde kolom {#joined}

Een bij elkaar gevoegde kolom verplaatst een kenmerk van de ene tabel naar een andere locatie *tot* de vele tabel. Het klassieke voorbeeld van één/vele is klanten (één) en orden (vele).

In het onderstaande voorbeeld wordt `Customer's group\_id` dimensie wordt samengevoegd tot `orders` tabel.

![](../../assets/joined_column.gif)

## Vele-aan-één berekende kolommen {#manytoone}

Deze kolommen gebruiken de zelfde wegen die één-aan-vele kolommen doen, maar zij richten gegevens in de tegenovergestelde richting. De kolom wordt gemaakt aan de ene kant van het pad, in tegenstelling tot de andere kant. Vanwege deze relatie moet de waarde in de kolom een aggregatie zijn, dat wil zeggen een wiskundige bewerking die wordt uitgevoerd op de gegevenspunten aan de vele zijden. Hiervoor zijn veel gevallen van gebruik en een aantal hiervan wordt hieronder vermeld.

### Aantal {#count}

Dit type van berekende kolom keert de telling van waarden op de vele lijst terug *op* de ene tabel.

In het onderstaande voorbeeld wordt de dimensie `Customer's lifetime number of canceled orders` wordt gemaakt op de `customers` tabel (met een filter voor `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### Som {#sum}

Een som berekende kolom is de som van waarden op de `many` op de ene tabel.

Dit kan worden gebruikt om klant-vlakke dimensies tot stand te brengen zoals `Customer's lifetime revenue`.

### Min. of Max {#minmax}

Een min of max berekende kolom retourneert de kleinste of grootste record aan de vele zijden.

Dit kan worden gebruikt om klant-vlakke dimensies tot stand te brengen zoals `Customer's first order date`.

### Exists {#exists}

Een berekende kolom is een binaire test die de aanwezigheid van een verslag aan de vele kant bepaalt. Met andere woorden, de nieuwe kolom retourneert een `1` als het pad ten minste één rij in elke tabel met elkaar verbindt, en `0` als er geen verbinding kan worden gemaakt.

Dit soort dimensie kan bijvoorbeeld bepalen of een klant ooit een bepaald product heeft gekocht. Een verbinding tussen een `customers` tabel en `orders` tabel, een filter voor een specifiek product, een dimensie `Customer has purchased Product X?` kan worden gebouwd.

## Handmatige verwijzingskaart {#map}

Als u moeite hebt zich te herinneren wat alle input wanneer het creëren van een berekende kolom zijn, houd deze verwijzingskaart handig wanneer u bouwt:

![](../../assets/merged_reference_map.png)

## Geavanceerde berekende kolommen {#advanced}

In uw vraag om vragen over uw zaken te analyseren en te beantwoorden, kunt u een situatie ontmoeten waarin u niet de nauwkeurige kolom kunt bouwen u wilt.

Adobe raadt aan de [Geavanceerde berekende kolomtypen](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) gids om te zien welk soort kolommen het de steunteam van de Adobe kan bouwen. Dat onderwerp behandelt ook de info die u van u nodig hebt om de kolom tot stand te brengen - omvat het met uw verzoek.

## Gerelateerde documentatie

* [Berekende kolommen maken](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Paden voor berekende kolommen maken/verwijderen](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Tabelrelaties begrijpen en evalueren](../../data-analyst/data-warehouse-mgr/table-relationships.md)
