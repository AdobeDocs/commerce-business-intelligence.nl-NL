---
title: De berekende kolom Datumverschil gebruiken
description: Leer het doel en het gebruik van de berekende kolom van het Verschil van de Datum.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Datumverschil Berekende kolom

Dit onderwerp schetst het doel en het gebruik van de `Date Difference` berekende kolom beschikbaar in de **[!DNL Manage Data > Data Warehouse]** pagina. Hieronder volgt een uitleg van wat het doet, gevolgd door een voorbeeld, en de mechanismen om het te maken.

**Verklaring**

Het kolomtype `Date Difference` berekent de tijd tussen twee gebeurtenissen die tot één record behoren, op basis van de tijdstempels van de gebeurtenis. De onbewerkte waarde die in deze kolom wordt berekend, is in seconden, maar het wordt automatisch omgezet in minuten, uren, dagen, enzovoort, voor weergave op rapporten. Wanneer u deze waarde echter als filter/groep gebruikt, wilt u deze in seconden gebruiken.

Een `date difference` berekende kolom kan worden gebruikt om metrisch tot stand te brengen die de gemiddelde of mediane tijd tussen twee gebeurtenissen, zoals gemiddelde tijd tussen klantenregistratie en hun eerste orden berekent.

**Voorbeeld**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00 :00: 00 | 2015-01-01 12 :30: 00 | 45000 |
| `B` | 2015-01-01 08 :00: 00 | 2015-01-01 10 :00: 00 | 7200 |

{style="table-layout:auto"}


In het bovenstaande voorbeeld is de kolom `Date Difference` de kolom `Seconds between timestamp_2 and timestamp_1` . Deze voert de berekening uit `timestamp_2 minus timestamp_1` .

**Mechanics**

In de volgende stappen wordt beschreven hoe u een kolom `Date Difference` maakt.

1. Navigeer naar de pagina **[!DNL Manage Data > Data Warehouse]** .
1. Navigeer naar de tabel waarop u deze kolom wilt maken.
1. Klik op **[!UICONTROL Create a Column]** en configureer de kolom als volgt:
   * Selecteren `Column Definition Type` > `Same Table`
   * Selecteren `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Selecteer `Ending DATETIME` column > Choose the ending datetime field, which is typisch the event that occur later
   * Selecteer `Starting DATETIME` column** > Kies het veld Begindatum en tijd. Dit is doorgaans de gebeurtenis die eerder plaatsvindt.

1. Geef de kolom een naam en klik op **[!UICONTROL Save]** .
1. De kolom is beschikbaar om *onmiddellijk* te gebruiken.

Het volgende voorbeeld is geconfigureerd om de waarde `Seconds between order date and customer's creation date` te berekenen:

![&#x200B; de configuratie van de de verschilberekening van de Datum die de kolomselecties van de datetime toont &#x200B;](../../assets/date_diff.png)
