---
title: Opeenvolgende vergelijking berekende kolom
description: Leer het doel en het gebruik van de Opeenvolgende Berekende kolom van de Vergelijking.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# Opeenvolgende vergelijking berekende kolom

Dit onderwerp schetst het doel en het gebruik van `Sequential Comparison` berekende kolom beschikbaar in de **[!DNL Manage Data > Data Warehouse]** pagina. Hieronder volgt een uitleg van wat het doet, gevolgd door een voorbeeld, en de mechanismen om het te maken.

**Toelichting**

De `Sequential Comparison` kolomtype: Hiermee wordt het verschil tussen opeenvolgende gebeurtenissen gevonden. Het meest voorkomende type `Sequential Comparison` de kolom is `Seconds since previous order` kolom. Er zijn drie invoeren nodig voor deze kolom:

1. `Event Owner`: Deze invoer bepaalt de entiteit waarvoor de rijen zijn gegroepeerd. In het dialoogvenster `Seconds since previous order` kolom, is de gebeurteniseigenaar de klant, omdat u het aantal seconden sinds de vorige orde van de zelfde klant wilt vinden.
1. `Event Date`: Deze invoer dwingt de volgorde van gebeurtenissen af. In het geval van `Seconds since previous order`moet de kolom met het tijdstempel van de volgorde `Event Date`. Deze invoer is altijd een tijdstempel.
1. `Value to Compare`: Deze invoer is de werkelijke waarde die moet worden vergeleken. De waarde van de vorige rij wordt afgetrokken van de waarde van de huidige rij. Daarom wordt een kolom die het tijdverschil tussen opeenvolgende orders van een klant vindt, aangeroepen `Seconds since previous order`. Deze invoer hoeft geen tijdstempel te zijn. Een niet-tijdstempelvoorbeeld is het verschil in orderwaarde tussen opeenvolgende orders van een klant te vinden.

**Voorbeeld**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

In het bovenstaande voorbeeld: `Seconds since owner's previous event` is de `Sequential Comparison` berekende kolom. Voor de `owner_id = A`, wordt eerst een reeks vastgesteld op basis van de `timestamp` kolom, en trekt dan de vorige gebeurtenis af `timestamp` uit de tijdstempel van de huidige gebeurtenis. In de derde rij in de tabel - de tweede rij voor `owner_id A` - de waarde van `Seconds since owner's previous event` is het aantal seconden tussen &#39;2015-01-01 02:00&#39; en &#39;2015-01-01 00&#39;:00:00&quot;. Dit verschil is twee uur = 7200 seconden.

Voor dit berekende kolomtype heeft de rij die overeenkomt met de eerste gebeurtenis van de eigenaar een `NULL` waarde.

**mechanisch**

Om een **Gebeurtenisnummer** kolom:

1. Ga naar de **[!DNL Manage Data** > **Data Warehouse]** pagina.
1. Navigeer naar de tabel waarop u deze kolom wilt maken.
1. Klikken **[!UICONTROL Create New Column]** aan de rechterbovenhoek van het scherm.
1. Selecteren `Same Table` als de `Definition Type` (Als de kolommen die u wilt vergelijken zich niet op de zelfde lijst bevinden kunt u hen moeten verplaatsen).
1. Selecteren `SEQUENTIAL_COMPARISON` als de `Column Definition Equation`.
1. Kies de inputs, zoals hierboven beschreven:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`
1. U kunt ook filters toevoegen om rijen uit te sluiten van overweging. De uitgesloten rijen hebben een NULL-waarde voor deze kolom.
1. Geef een naam op voor de kolom boven aan de pagina en klik op **[!UICONTROL Save]**.
1. De kolom is beschikbaar voor gebruik *onmiddellijk*.

![SEC](../../assets/SEC_new.png)
