---
title: De berekende kolom Datumverschil gebruiken
description: Leer het doel en het gebruik van de berekende kolom van het Verschil van de Datum.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 2%

---

# Datumverschil Berekende kolom

Dit onderwerp schetst het doel en het gebruik van `Date Difference` berekende kolom beschikbaar in de **[!DNL Manage Data > Data Warehouse]** pagina. Hieronder volgt een uitleg van wat het doet, gevolgd door een voorbeeld, en de mechanismen om het te maken.

**Toelichting**

De `Date Difference` kolomtype: zoekt de tijd tussen twee gebeurtenissen die tot één record behoren, op basis van de tijdstempels van de gebeurtenis. De onbewerkte waarde die in deze kolom wordt berekend, is in seconden, maar wordt automatisch omgezet in minuten, uren, dagen enzovoort voor weergave in rapporten. Wanneer u deze waarde echter als filter/groep gebruikt, wilt u deze in seconden gebruiken.

A `date difference` de berekende kolom zou kunnen worden gebruikt om metrisch tot stand te brengen die de gemiddelde of mediane tijd tussen twee gebeurtenissen, zoals gemiddelde tijd tussen klantenregistratie en hun eerste orden berekent.

**Voorbeeld**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}


In het bovenstaande voorbeeld wordt `Date Difference` de kolom is `Seconds between timestamp_2 and timestamp_1` kolom. Het voert de berekening uit `timestamp_2 minus timestamp_1`.

**mechanisch**

In de volgende stappen wordt beschreven hoe u een `Date Difference` kolom.

1. Ga naar de **[!DNL Manage Data > Data Warehouse]** pagina.
1. Navigeer naar de tabel waarop u deze kolom wilt maken.
1. Klikken **[!UICONTROL Create a Column]** en configureer de kolom als volgt:
   * Selecteren `Column Definition Type` > `Same Table`
   * Selecteren `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Selecteren `Ending DATETIME` kolom > Kies het einddatumveld. Dit is doorgaans de gebeurtenis die later plaatsvindt
   * Selecteren `Starting DATETIME` kolom** > Kies het begindatumveld. Dit is doorgaans de gebeurtenis die eerder plaatsvindt

1. Geef een naam op voor de kolom en klik op **[!UICONTROL Save]**.
1. De kolom is beschikbaar voor gebruik *onmiddellijk*.

Als voorbeeld wordt het volgende voorbeeld geconfigureerd om het `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
