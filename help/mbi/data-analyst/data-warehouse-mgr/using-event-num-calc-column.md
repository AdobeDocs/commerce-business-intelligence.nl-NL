---
title: Gebeurtenisnummer berekende kolom
description: Leer het doel en het gebruik van de berekende kolom van het Aantal gebeurtenissen.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Gebeurtenisnummer berekende kolom

Dit onderwerp schetst het doel en het gebruik van de `Event Number` berekende kolom beschikbaar in de **[!DNL Manage Data > Data Warehouse]** pagina. Hieronder volgt een uitleg van wat het doet, gevolgd door een voorbeeld, en de mechanismen om het te maken.

**Verklaring**

Het `Event Number` kolomtype identificeert de opeenvolging waarin de gebeurtenissen voor een bepaalde **gebeurteniseigenaar** voorkwamen, als a `customer` of `user`. Als u bekend bent met SQL, is dit kolomtype identiek aan de functie `RANK` . Het kan worden gebruikt om verschillen in gedrag tussen gebeurtenissen voor het eerst, herhalingsgebeurtenissen of nde gebeurtenissen in uw gegevens waar te nemen.

In gevallen van een tijd, bevat deze kolom de zelfde **rang** voor de gebonden gebeurtenissen, en slaat de verdere aantallen over. Als bijvoorbeeld de cijfers 5,8,10,10,12 worden gerangschikt, zouden de ranks 1,2,3,3,5 zijn.

Het meest gebruikte geval in deze kolom is om kopers voor het eerst te analyseren en kopers te herhalen. De eerste keer dat kopers worden geïdentificeerd door een filter (aan een metrische waarde of rapport) toe te voegen op `Customer's order number` = 1. `Customer's order number` is een kolom van het type `Event Number` .

**Voorbeeld**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00 :00: 00 | 1 |
| **2 | B | 2015-01-01 00 :30: 00 | 1 |
| **3 | A | 2015-01-01 02 :00: 00 | 2 |
| **4 | A | 2015-01-02 13 :00: 00 | 3 |
| **5 | B | 2015-01-03 13 :00: 00 | 2 |

In het bovenstaande voorbeeld is de kolom `Owner's event number` een `Event Number` -kolom. De gebeurtenissen van de eigenaar worden in de volgorde gerangschikt waarin ze zijn opgetreden (op basis van de kolom `timestamp` ).

Neem bijvoorbeeld alle rijen waar `owner_id = A` staat. De eerste rij in de tabel is de oudste tijdstempel voor deze eigenaar, gevolgd door de derde rij in de tabel, gevolgd door de vierde rij in de tabel.

**Mechanics**

Hier volgen enkele instructies voor het maken van een kolom `Event Number` :

1. Navigeer naar de pagina **[!UICONTROL Manage Data > Data Warehouse]** .

1. Navigeer naar de tabel waarop u deze kolom wilt maken.

1. Klik op **[!UICONTROL Create a Column]** en kies het kolomtype `EVENT_NUMBER (…)` onder de sectie `Same Table` .

1. De eerste vervolgkeuzelijst `Event Owner` geeft de entiteit aan waarvoor de rang moet worden bepaald. In het geval waarin een `Customer's order number` , een klant-id zoals `customer_id` of `customer_email` de `Event Owner` zou zijn.

1. De tweede vervolgkeuzelijst `Event Rank` geeft de kolom aan die de volgorde afdwingt die de positie van de rij bepaalt. In het geval waarin een `Customer's order number` is, is de `created_at` timestamp de `Event Rank` .

1. Onder het vervolgkeuzemenu `Options` kunt u filters toevoegen om rijen uit te sluiten van het overwegen. De uitgesloten rijen hebben een `NULL` waarde voor deze kolom.

1. Geef de kolom een naam en klik op **[!UICONTROL Save]** .

1. De kolom is beschikbaar om _onmiddellijk te gebruiken._
