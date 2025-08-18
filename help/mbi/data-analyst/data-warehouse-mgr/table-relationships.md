---
title: Tabelrelaties begrijpen en evalueren
description: Leer hoe u begrijpt hoeveel mogelijke exemplaren in een tabel tot een entiteit in een andere tabel kunnen behoren.
exl-id: e7256f46-879a-41da-9919-b700f2691013
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Tabelrelaties begrijpen en evalueren

Wanneer u de relatie tussen twee gegeven tabellen beoordeelt, moet u begrijpen hoeveel mogelijke voorvallen in een tabel tot een entiteit in een andere tabel kunnen behoren, en omgekeerd. Gebruik bijvoorbeeld een `users` -tabel en een `orders` -tabel. In dit geval, wilt u weten hoeveel **orden** a bepaalde **gebruiker** heeft geplaatst en hoeveel mogelijke **gebruikers** en **orde** tot kon behoren.

Het begrip van verhoudingen is essentieel aan het handhaven van gegevensintegriteit, aangezien het de nauwkeurigheid van uw [ berekende kolommen ](../data-warehouse-mgr/creating-calculated-columns.md) en [ dimensies ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) beïnvloedt. Meer leren, zie [ relatietypen ](#types) en [ hoe te om de lijsten in uw Data Warehouse te evalueren.](#eval)

## Relatietypen {#types}

Er zijn drie soorten relaties die tussen twee tabellen kunnen bestaan:

1. [&quot;one-to-one&quot;](#onetoone)
1. [&quot;one-to-many&quot;](#onetomany)
1. [&quot;many-to-many&quot;](#manytomany)

### `One-to-One` {#onetoone}

In een `one-to-one` -relatie behoort een record in de tabel `B` tot slechts één record in de tabel `A` . En een record in Tabel `A` behoort tot slechts één record in Tabel `B` .

In de relatie tussen personen en de rijbewijsnummers kan een persoon bijvoorbeeld slechts één rijbewijsnummer hebben, terwijl het rijbewijsnummer alleen aan de persoon toebehoort.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

In een `one-to-many` -relatie kan een record in een tabel `A` mogelijk tot meerdere records in de tabel `B` behoren. Denk aan de relatie tussen `orders` en `items` - een orde kan vele punten bevatten, maar een punt behoort tot één enkele orde. In dit geval is de tabel `orders` de ene zijde en de tabel `items` de vele zijden.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

In een `many-to-many` -relatie kan een record in een tabel `B` mogelijk tot meerdere records in de tabel `A` behoren. En omgekeerd, kan een verslag in lijst `A` tot verscheidene verslagen in Lijst `B` behoren.

Denk over het verband tussen **producten** en **categorieën**: een product kan tot vele categorieën behoren, en een categorie kan vele producten bevatten.

![](../../assets/many-to-many.png)

## Uw tabellen evalueren {#eval}

Gezien de soorten verhoudingen die tussen lijsten bestaan, kunt u leren hoe te om de lijsten in uw Data Warehouse te evalueren. Aangezien deze relaties bepalen hoe berekende kolommen met meerdere tabellen worden gedefinieerd, is het belangrijk dat u begrijpt hoe tabelrelaties worden geïdentificeerd en tot welke zijde - `one` of `many` - de tabel behoort.

Er zijn twee methoden die u kunt gebruiken om de relaties van een bepaald paar tabellen in uw Data Warehouse te evalueren. De eerste methode stelt a [ conceptueel kader ](#concept) in dienst dat overweegt hoe de entiteiten van de lijst met elkaar in wisselwerking staan. De tweede methode gebruikt het [ schema van de lijst ](#schema).

### Het conceptuele kader gebruiken {#concept}

Deze methode gebruikt een conceptueel kader om te beschrijven hoe de entiteiten in de twee lijsten met elkaar kunnen communiceren. Het is belangrijk te begrijpen dat dit kader beoordeelt wat mogelijk is, gezien de relatie.

Wanneer u bijvoorbeeld nadenkt over gebruikers en bestellingen, moet u rekening houden met alles wat mogelijk is in de relatie. Een geregistreerde gebruiker kan binnen zijn levensduur geen bestellingen, slechts één bestelling of meerdere bestellingen plaatsen. Als u uw zaken hebt gelanceerd en geen orden geplaatst, is het mogelijk dat een bepaalde gebruiker vele orden in hun leven kan plaatsen. De tabellen zijn hierop afgestemd.

Deze methode gebruiken:

1. Identificeer de entiteit die in elke tabel wordt beschreven. **Hint: het is gewoonlijk een zelfstandig naamwoord**. In de tabellen `user` en `orders` worden bijvoorbeeld expliciet gebruikers en bestellingen beschreven.

1. Identificeer een of meer werkwoorden die beschrijven hoe deze entiteiten op elkaar inwerken. Wanneer gebruikers bijvoorbeeld met bestellingen vergelijken, plaatsen gebruikers bestellingen. In de andere richting zijn de bestellingen &quot;van&quot; gebruikers.

Dit type framework kan worden toegepast op elke koppeling van tabellen in uw Data Warehouse. Zo kunt u gemakkelijk het type relatie identificeren en zien welke tabel één zijde heeft en welke tabel een vele zijde heeft.

Zodra u de terminologie hebt geïdentificeerd die beschrijft hoe de twee lijsten interactie aangaan, kader de interactie in beide richtingen door te overwegen hoe één bepaalde geval van de eerste entiteit op de tweede betrekking heeft. Hier zijn enkele voorbeelden van elke relatie:

### `One-to-One`

Eén persoon kan slechts één rijbewijsnummer hebben. Een bepaald rijbewijsnummer behoort alleen tot de persoon.

Dit is een `one-to-one` -relatie waarbij elke tabel een ene kant heeft.

![](../../assets/one-to-one3.png)

### `One-to-Many`

Een bepaalde volgorde kan veel items bevatten. Eén gegeven item behoort tot slechts één bestelling.

Dit is een `one-to-many` -relatie waarbij de tabel met bestellingen de ene kant is en de tabel met items de vele kant.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

Eén bepaald product kan tot veel categorieën behoren. Een bepaalde categorie kan vele producten bevatten.

Dit is een `many-to-many` -relatie waarbij elke tabel een vele kanten heeft.

![](../../assets/many-to-many3.png)

### Het schema van de tabel gebruiken {#schema}

De tweede methode gebruikt het tabelschema. Het schema bepaalt welke kolommen de [`Primary` ](https://en.wikipedia.org/wiki/Unique_key) en [`Foreign` ](https://en.wikipedia.org/wiki/Foreign_key) sleutels zijn. U kunt deze sleutels gebruiken om lijsten samen te verbinden en hulp bepalen relatietypen.

Zodra u de kolommen identificeert die twee lijsten samen verbinden, gebruik de kolomtypes om de lijstverhouding te evalueren. Hier volgen enkele voorbeelden:

### `One-to-one`

Als de tabellen zijn gekoppeld met behulp van `primary key` van beide tabellen, wordt in elke tabel dezelfde unieke entiteit beschreven en is de relatie `one-to-one` .

Een `users` -tabel kan bijvoorbeeld de meeste gebruikerskenmerken (zoals de naam) bevatten, terwijl een aanvullende `user_source` -tabel gebruikersregistratiebronnen vastlegt. In elke tabel staat een rij voor één gebruiker.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>Accepteer je gastorders? Zie [ Gast Orden ](../data-warehouse-mgr/guest-orders.md) om te leren hoe de gastorden uw lijstverhoudingen kunnen beïnvloeden.

Wanneer tabellen worden gekoppeld met een `Foreign key` die verwijst naar een `primary key` , wordt met deze instelling een `one-to-many` -relatie beschreven. De ene kant is de tabel met de `primary key` en de andere kant is de tabel met de `foreign key` .

![](../../assets/one-to-many1.png)

### `Many-to-many`

Als een van de volgende twee true is, is de relatie `many-to-many` :

* `Non-primary key` kolommen worden gebruikt om twee tabellen te koppelen
  ![](../../assets/many-to-many1.png)
* Een deel van een samenstelling `primary key` wordt gebruikt om twee tabellen te koppelen

![](../../assets/many-to-mnay2.png)

## Volgende stappen

Het correct beoordelen van lijstverhoudingen is essentieel om uw gegevens nauwkeurig te modelleren. Nu u begrijpt hoe de lijsten met elkaar verwant zijn, zie [ wat u met de Manager van Data Warehouse ](../data-warehouse-mgr/tour-dwm.md) kunt doen.
