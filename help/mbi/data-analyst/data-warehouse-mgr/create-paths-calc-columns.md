---
title: Paden voor berekende kolommen maken of verwijderen
description: Leer hoe u een pad definieert waarin wordt beschreven hoe de tabel waarop u een kolom maakt, verwant is aan de tabel waaruit u gegevens aan het ophalen bent.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Paden maken of verwijderen voor berekende kolommen

## Vernieuwen van berekende kolommen

Wanneer [berekende kolommen maken](../data-warehouse-mgr/creating-calculated-columns.md) in uw Data Warehouse, wordt u gevraagd om een weg te bepalen die hoe de lijst beschrijft u een kolom op creeert verwant met de lijst is u aan informatie trekt. Als u een pad wilt maken, moet u twee dingen weten:

1. Hoe de lijsten in uw gegevensbestanden op elkaar betrekking hebben
1. De primaire en buitenlandse sleutels die deze verhouding bepalen

Als u deze informatie kent, kunt u gemakkelijk tot een weg leiden die de instructies in dit onderwerp volgt. U kunt een technische deskundige in uw organisatie vragen of contact opnemen met de [Team voor professionele services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Vernieuwen op tabelrelaties en toetstypen {#refresher}

### Tabelrelaties {#relationships}

Dit concept wordt behandeld in het [Artikel over tabelrelaties begrijpen en evalueren](../../data-analyst/data-warehouse-mgr/table-relationships.md)Maar een korte samenvatting doet niemand pijn, toch?

Tabellen kunnen op drie manieren met elkaar worden verbonden:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | De relatie tussen personen en rijbewijsnummers. Een persoon kan slechts één rijbewijsnummer hebben en een rijbewijsnummer behoort slechts tot één persoon. |
| **`one-to-many`** | De relatie tussen bestellingen en items - een bestelling kan veel items bevatten, maar een item behoort tot één bestelling. In dit geval is de tabel met bestellingen de ene zijde en is de tabel met items de vele zijden. |
| **`many-to-many`** | De relatie tussen producten en categorieën: een product kan tot veel categorieën behoren en een categorie kan veel producten bevatten . |

{style="table-layout:auto"}

Wanneer een verband tussen twee lijsten wordt begrepen, kan het worden gebruikt om te bepalen welke weg zou moeten worden gecreeerd om informatie van één lijst aan een andere te brengen. Voor deze volgende stap moet u weten welke primaire en externe sleutels een tabelrelatie mogelijk maken.

### Primaire en buitenlandse sleutels {#keys}

A `Primary Key` is een onveranderlijke kolom of een reeks kolommen die unieke waarden binnen een lijst veroorzaakt. Wanneer een klant bijvoorbeeld een bestelling maakt op een website, wordt een nieuwe rij toegevoegd aan de `orders` tafel in uw winkelwagentje, met een nieuwe `order_id`. Dit `order_id` staat zowel de klant als de zaken toe om de vooruitgang van die specifieke orde te volgen. Omdat volgorde-id uniek is, is dit doorgaans de `Primary Key` van een `orders` tabel.

A `Foreign Key` is een kolom die binnen een lijst wordt gecreeerd die met verbindt `Primary Key` kolom van een andere tabel. Met Buitenlandse sleutels worden verwijzingen tussen tabellen gemaakt, zodat analisten records gemakkelijk kunnen opzoeken en koppelen. Zeg u wilde weten welke orden tot elk van uw klanten behoorden. De `customer id` kolom (`Primary Key` van de `customers` de `order_id` kolom (`Foreign Key` in de `customers` tabel, verwijzen naar de `Primary Key` van de `orders` tabel ) stelt ons in staat deze informatie te koppelen en te analyseren . Wanneer u een pad maakt, wordt u gevraagd om beide `Primary Key` en `Foreign Key`.

## Een pad maken {#createpath}

Wanneer u een kolom in de Data Warehouse maakt, moet u het pad definiëren dat informatie van de ene tabel naar een andere overbrengt. Soms worden paden vooraf gevuld, omdat er een pad tussen tabellen bestaat, maar als dit niet gebeurt, moet u er een maken.

De relatie gebruiken tussen **klanten** en **orders** om u te tonen hoe het wordt gedaan. Omlaag gebroken:

* De relatie is `one-to-many` - een klant kan vele bestellingen hebben, maar een bestelling kan slechts één klant hebben. Dit vertelt ons de richting van de verhouding, of waar de berekende kolom zou moeten worden gecreeerd. In dit geval betekent het informatie van de `orders` de tabel kan in `customers` tabel.
* De `primary key` u wilt gebruiken is `customers.customerid`of de `customer ID` in de `customers` tabel.
* De `foreign key` u wilt gebruiken is `orders.customerid`of de `customer ID` in de `orders` tabel.

U kunt nu het pad maken.

1. Klikken **[!UICONTROL Data > Data Warehouse]**.
1. Klik in de tabellijst op de tabel waarin u de kolom wilt maken. In dit voorbeeld is het `customers` tabel.
1. Het tabelschema wordt weergegeven. Klikken **[!UICONTROL Create New Column]**.
1. Geef uw kolom bijvoorbeeld een naam, `Customer's orders`.
1. Selecteer de definitie voor de kolom. Kijk uit de [Berekende kolomhulplijn](../data-warehouse-mgr/creating-calculated-columns.md) voor een handig bedriegblad.
1. In de [!UICONTROL Select table and column] vervolgkeuzelijst, klikt u op de knop **[!UICONTROL Create new path]** optie.

   ![Paden maken voor de modale berekende kolommen](../../assets/Creating_Paths_modal.png)

1. Selecteer met behulp van de vervolgkeuzelijsten de primaire en externe toetsen voor elke tabel.

   Op de `Many` zijde, selecteert u `orders.customerid` - Vergeet niet dat klanten veel bestellingen kunnen hebben.

   Op de `One` zijde, selecteert u `customers.customerid` - een bestelling kan slechts één klant hebben.

1. Klikken **[!UICONTROL Save]** om het pad op te slaan en de kolom te maken.

### Beperkingen voor het maken van paden {#limits}

* **[!DNL Commerce Intelligence]kan geen primaire/externe sleutelrelaties raden**. U wilt geen onjuiste gegevens in uw account introduceren, dus het maken van paden moet handmatig gebeuren.

* **U kunt momenteel alleen paden opgeven tussen twee verschillende tabellen**. Vormt de logica die u probeert opnieuw te maken meer dan twee tabellen? Het zou dan aan (1) zin kunnen hebben om de kolommen aan een intermediaire lijst eerst, dan aan de &quot;definitieve bestemmings&quot;lijst te verbinden, of (2) overleg met [Team voor professionele services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om de beste benadering van uw doelstellingen te vinden.

* **Een kolom kan slechts de buitenlandse belangrijkste verwijzing voor ÉÉN weg tegelijkertijd zijn**. Als `order_items.order_id` punten naar `orders.id`vervolgens `order_items.order_id` kan niet op iets anders wijzen.

* **`Many-to-many`paden kunnen technisch worden gemaakt, maar produceren vaak slechte gegevens omdat geen van beide zijden waar is `one-to-many` buitenlandse sleutel**. De beste manier om deze wegen te benaderen hangt altijd van de specifieke gewenste analyse af. Raadpleeg het RJ Analyst-team om de beste oplossing te ontdekken.

Als u geen berekende kolom kunt maken vanwege een of meer van de bovenstaande beperkingen, neemt u contact op met de technische ondersteuning en een beschrijving van de kolom

## Een berekend kolompad verwijderen {#delete}

Een onjuist pad in de Data Warehouse gemaakt? Of misschien doe je een beetje lentesreiniging en wil je opruimen? Als u een pad van uw account moet verwijderen, kunt u [stuur een kaartje naar Adobe-ondersteuningsanalisten](../../guide-overview.md#Submitting-a-Support-Ticket). **Zorg ervoor dat u de naam van het pad opneemt!**

## Omloop {#wrapup}

Nu kunt u op een comfortabele manier paden maken voor berekende kolommen in uw Data Warehouse. Als u nog steeds niet zeker bent van een bepaald pad, vergeet dan niet dat u altijd op **[!UICONTROL Support]** in uw [!DNL Commerce Intelligence] account om hulp te krijgen.

## Verwante

* [Tabelrelaties begrijpen en evalueren](../data-warehouse-mgr/table-relationships.md)
* [Paden maken voor berekende kolommen](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Berekende kolomtypen](../data-warehouse-mgr/calc-column-types.md) proberen te maken.
