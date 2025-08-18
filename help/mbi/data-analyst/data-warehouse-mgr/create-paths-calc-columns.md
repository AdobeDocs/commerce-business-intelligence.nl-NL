---
title: Paden voor berekende kolommen maken of verwijderen
description: Leer hoe u een pad definieert waarin wordt beschreven hoe de tabel waarin u een kolom maakt, verwant is aan de tabel waaruit u gegevens aan het ophalen bent.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Paden maken of verwijderen voor berekende kolommen

## Vernieuwen van berekende kolommen

Wanneer [ het creëren van berekende kolommen ](../data-warehouse-mgr/creating-calculated-columns.md) in uw Data Warehouse, wordt u gevraagd om een weg te bepalen beschrijvend hoe de lijst u een kolom op creeert verwant met de lijst is u informatie van trekt. Als u een pad wilt maken, moet u twee dingen weten:

1. Hoe de lijsten in uw gegevensbestanden op elkaar betrekking hebben
1. De primaire en buitenlandse sleutels die deze verhouding bepalen

Als u deze informatie kent, kunt u gemakkelijk tot een weg leiden die de instructies in dit onderwerp volgt. U kunt een technische deskundige in uw organisatie vragen of het [ Professionele team van de Diensten ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) contacteren.

## Vernieuwen op tabelrelaties en toetstypen {#refresher}

### Tabelrelaties {#relationships}

Dit concept wordt behandeld in het [ Begrijpen en het evalueren van de artikelen van lijstverhoudingen ](../../data-analyst/data-warehouse-mgr/table-relationships.md), maar een snelle samenvatting doet niemand pijn, niet?

Tabellen kunnen op drie manieren met elkaar worden verbonden:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | De relatie tussen personen en rijbewijsnummers. Een persoon kan slechts één rijbewijsnummer hebben en een rijbewijsnummer behoort slechts tot één persoon. |
| **`one-to-many`** | De relatie tussen orders en items - een order kan veel items bevatten, maar een item behoort tot één bestelling. In dit geval is de tabel met bestellingen de ene zijde en is de tabel met items de vele zijden. |
| **`many-to-many`** | Het verband tussen producten en categorieën: een product kan tot vele categorieën behoren, en een categorie kan vele producten bevatten. |

{style="table-layout:auto"}

Wanneer een verband tussen twee lijsten wordt begrepen, kan het worden gebruikt om te bepalen welke weg zou moeten worden gecreeerd om informatie van één lijst aan een andere te brengen. Voor deze volgende stap moet u weten welke primaire en externe sleutels een tabelrelatie mogelijk maken.

### Primaire en buitenlandse sleutels {#keys}

A `Primary Key` is een onveranderlijke kolom of reeks kolommen die unieke waarden binnen een lijst veroorzaakt. Wanneer een klant bijvoorbeeld een bestelling maakt op een website, wordt een nieuwe rij toegevoegd aan de `orders` -tabel in uw winkelwagentje, met een nieuwe `order_id` . Hierdoor kunnen zowel de klant als het bedrijf de voortgang van die specifieke bestelling volgen. `order_id` Omdat volgorde-id uniek is, is dit doorgaans de `Primary Key` van een `orders` -tabel.

Een `Foreign Key` is een kolom die is gemaakt in een tabel die is gekoppeld aan de kolom `Primary Key` van een andere tabel. Met Buitenlandse sleutels worden verwijzingen tussen tabellen gemaakt, zodat analisten records gemakkelijk kunnen opzoeken en koppelen. Zeg u wilde weten welke orden tot elk van uw klanten behoorden. Met de kolom `customer id` (`Primary Key` van de tabel `customers` ) en de kolom `order_id` (`Foreign Key` in de tabel `customers` die verwijst naar `Primary Key` van de tabel `orders` ) kunnen we deze informatie koppelen en analyseren. Wanneer u een pad maakt, wordt u gevraagd om zowel `Primary Key` als `Foreign Key` te definiëren.

## Een pad maken {#createpath}

Wanneer u een kolom in uw Data Warehouse maakt, moet u het pad definiëren dat informatie van de ene tabel naar een andere overbrengt. Soms worden paden vooraf gevuld, omdat er een pad tussen tabellen bestaat, maar als dit niet gebeurt, moet u er een maken.

Gebruik het verband tussen **klanten** en **orden** om u te tonen hoe het wordt gedaan. Omlaag gebroken:

* De relatie is `one-to-many` - een klant kan veel bestellingen hebben, maar een bestelling kan slechts één klant hebben. Dit vertelt ons de richting van de verhouding, of waar de berekende kolom zou moeten worden gecreeerd. In dit geval betekent dit dat informatie uit de tabel `orders` kan worden overgebracht naar de tabel `customers` .
* De `primary key` die u wilt gebruiken, is `customers.customerid` of de `customer ID` -kolom in de `customers` -tabel.
* De `foreign key` die u wilt gebruiken, is `orders.customerid` of de `customer ID` -kolom in de `orders` -tabel.

U kunt nu het pad maken.

1. Klik op **[!UICONTROL Data > Data Warehouse]**.
1. Klik in de tabellijst op de tabel waarin u de kolom wilt maken. In dit voorbeeld is dit de `customers` -tabel.
1. Het tabelschema wordt weergegeven. Klik op **[!UICONTROL Create New Column]**.
1. Geef uw kolom een naam, bijvoorbeeld, `Customer's orders`.
1. Selecteer de definitie voor de kolom. Controle uit de [ Berekende Gids van de Kolom ](../data-warehouse-mgr/creating-calculated-columns.md) voor een handig bedriegblad.
1. Klik in het vervolgkeuzemenu [!UICONTROL Select table and column] op de optie **[!UICONTROL Create new path]** .

   ![ Creërend wegen voor berekende kolommen modaal ](../../assets/Creating_Paths_modal.png)

1. Selecteer met behulp van de vervolgkeuzelijsten de primaire en externe toetsen voor elke tabel.

   Aan de zijde van `Many` selecteert u `orders.customerid` - onthoud dat klanten veel bestellingen kunnen hebben.

   Aan de zijde van `One` selecteert u `customers.customerid` - een bestelling kan slechts één klant hebben.

1. Klik op **[!UICONTROL Save]** om het pad op te slaan en de kolom te maken.

### Beperkingen voor het maken van paden {#limits}

* **[!DNL Commerce Intelligence]kan primaire/buitenlandse zeer belangrijke verhoudingen niet raden**. U wilt geen onjuiste gegevens in uw account introduceren, dus het maken van paden moet handmatig gebeuren.

* **momenteel, kunnen de wegen slechts tussen twee verschillende lijsten** worden gespecificeerd. Vormt de logica die u probeert opnieuw te maken meer dan twee tabellen? Het zou dan zin aan (1) kunnen hebben zich bij de kolommen aan een intermediaire lijst eerst, dan aan de &quot;definitieve bestemmings&quot;lijst, of (2) overleg met het [ Professionele team van de Diensten ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) om de beste benadering aan uw doelstellingen te vinden.

* **de kolom van A kan slechts de buitenlandse zeer belangrijke verwijzing voor ÉÉN weg tegelijkertijd zijn**. Als `order_items.order_id` bijvoorbeeld naar `orders.id` verwijst, kan `order_items.order_id` niet naar iets anders wijzen.

* **`Many-to-many`de wegen kunnen technisch worden gecreeerd, maar veroorzaken vaak slechte gegevens omdat geen van beide kant een ware `one-to-many` buitenlandse sleutel** is. De beste manier om deze wegen te benaderen hangt altijd van de specifieke gewenste analyse af. Raadpleeg het RJ Analyst-team om de beste oplossing te ontdekken.

Als u geen berekende kolom kunt maken vanwege een of meer van de bovenstaande beperkingen, neemt u contact op met de technische ondersteuning en een beschrijving van de kolom

## Een berekend kolompad verwijderen {#delete}

Een onjuist pad gemaakt in uw Data Warehouse? Of misschien doe je een beetje lentesreiniging en wil je opruimen? Als u een weg van uw rekening moet schrappen, kunt u [ een kaartje over naar Adobe steunanalisten ](../../guide-overview.md#Submitting-a-Support-Ticket) verzenden. **ben zeker om de naam van de weg te omvatten!**

## Omloop {#wrapup}

Nu kunt u op een comfortabele manier paden maken voor berekende kolommen in uw Data Warehouse. Als u nog steeds niet zeker bent over een bepaald pad, vergeet dan niet dat u altijd op **[!UICONTROL Support]** in uw [!DNL Commerce Intelligence] -account kunt klikken voor hulp.

## Verwante

* [Tabelrelaties begrijpen en evalueren](../data-warehouse-mgr/table-relationships.md)
* [Paden maken voor berekende kolommen](../data-warehouse-mgr/create-paths-calc-columns.md)
* [ Berekende de Types van Kolom ](../data-warehouse-mgr/calc-column-types.md) proberen om tot stand te brengen.
