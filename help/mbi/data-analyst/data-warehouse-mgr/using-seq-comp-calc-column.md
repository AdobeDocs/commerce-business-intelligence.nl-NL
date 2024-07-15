---
title: Opeenvolgende vergelijking berekende kolom
description: Leer het doel en het gebruik van de Opeenvolgende Berekende kolom van de Vergelijking.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Opeenvolgende vergelijking berekende kolom

Dit onderwerp schetst het doel en het gebruik van de `Sequential Comparison` berekende kolom beschikbaar in de **[!DNL Manage Data > Data Warehouse]** pagina. Hieronder volgt een uitleg van wat het doet, gevolgd door een voorbeeld en de mechanismen om het te maken.

**Verklaring**

Het kolomtype `Sequential Comparison` : zoekt naar het verschil tussen opeenvolgende gebeurtenissen. Het meest voorkomende type `Sequential Comparison` -kolom is de `Seconds since previous order` -kolom. Er zijn drie invoeren nodig voor deze kolom:

1. `Event Owner`: deze invoer bepaalt de entiteit waarvoor rijen zijn gegroepeerd. In de kolom `Seconds since previous order` is de eigenaar van de gebeurtenis bijvoorbeeld de klant, omdat u het aantal seconden wilt vinden dat is verstreken sinds de vorige volgorde van dezelfde klant.
1. `Event Date`: deze invoer dwingt de volgorde van gebeurtenissen af. In de gevallen van `Seconds since previous order` moet de kolom met het tijdstempel van de volgorde de `Event Date` zijn. Deze invoer is altijd een tijdstempel.
1. `Value to Compare`: deze invoer is de werkelijke waarde die moet worden vergeleken. De waarde van de vorige rij wordt afgetrokken van de waarde van de huidige rij. Daarom wordt een kolom die het tijdverschil tussen opeenvolgende bestellingen van een klant vindt, `Seconds since previous order` genoemd. Deze invoer hoeft geen tijdstempel te zijn. Een niet-tijdstempelvoorbeeld is het verschil in orderwaarde tussen opeenvolgende orders van een klant te vinden.

**Voorbeeld**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00 :00: 00 | NULL |
| **`2`** | B | 2015-01-01 00 :30: 00 | NULL |
| **`3`** | A | 2015-01-01 02 :00: 00 | 7200 |
| **`4`** | A | 2015-01-02 13 :00: 00 | 126000 |
| **`5`** | B | 2015-01-03 13 :00: 00 | 217800 |

In het bovenstaande voorbeeld is `Seconds since owner's previous event` de `Sequential Comparison` berekende kolom. Voor de `owner_id = A` wordt eerst een reeks geïdentificeerd op basis van de `timestamp` -kolom en vervolgens wordt de tijdstempel van de vorige gebeurtenis `timestamp` afgetrokken van de huidige gebeurtenis. In de derde rij in de tabel - de tweede rij voor `owner_id A` - is de waarde van `Seconds since owner's previous event` het aantal seconden tussen &#39;2015-01-01 02:00&#39; en &#39;2015-01-01 00 :00: 00&#39;. Dit verschil is twee uur = 7200 seconden.

Voor dit berekende kolomtype heeft de rij die overeenkomt met de eerste gebeurtenis van de eigenaar een `NULL` -waarde.

**Mechanics**

Om een **kolom van het Aantal van de Gebeurtenis** tot stand te brengen:

1. Navigeer naar de pagina **[!DNL Manage Data > Data Warehouse]** .

1. Navigeer naar de tabel waarop u deze kolom wilt maken.

1. Klik op **[!UICONTROL Create New Column]** in de rechterbovenhoek.

1. Selecteer `Same Table` als `Definition Type` (als de kolommen die u wilt vergelijken zich niet in dezelfde tabel bevinden, moet u ze mogelijk verplaatsen).

1. Selecteer `SEQUENTIAL_COMPARISON` als de `Column Definition Equation` .

1. Kies de inputs, zoals hierboven beschreven:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. U kunt ook filters toevoegen om rijen uit te sluiten van overweging. De uitgesloten rijen hebben een `NULL` waarde voor deze kolom.

1. Geef een naam op voor de kolom boven aan de pagina en klik op **[!UICONTROL Save]** .

1. De kolom is beschikbaar om *onmiddellijk* te gebruiken.

![ SEC ](../../assets/SEC_new.png)
