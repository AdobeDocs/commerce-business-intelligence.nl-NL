---
title: Geavanceerde berekende kolomtypen
description: Leer de grondbeginselen voor de meeste gevallen van de gebruikkolom — maar u kunt berekende kolom willen die een beetje complexer is dan wat de Manager van de Data Warehouse kan tot stand brengen.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---

# Geavanceerde berekende kolomtypen

Vele analyses u zouden kunnen willen tot stand brengen impliceren het gebruik van a **nieuwe kolom** die u `group by` of `filter by` wilt. Het [ Creëren Berekende Kolommen ](../data-warehouse-mgr/creating-calculated-columns.md) leerprogramma behandelt de grondbeginselen voor de meeste gebruiksgevallen, maar u kunt berekende kolom willen die een beetje complexer is dan wat de Manager van de Data Warehouse kan tot stand brengen.
{: #top}

Deze kolomtypen kunnen worden gemaakt door het Adobe-team van Data Warehouse-analisten. Als u een nieuwe berekende kolom wilt definiëren, geeft u ons de volgende informatie:

1. De **`definition`** van deze kolom (inclusief invoer, formules of opmaak)
1. De **`table`** waarop u de kolom wilt maken
1. Alle **`example data points`** die beschrijven wat de kolom moet bevatten

Hier volgen enkele voorbeelden van geavanceerd berekende kolommen die gebruikers vaak nuttig vinden:

* [Order (of rank)-gebeurtenis opeenvolgend](#compareevents)
* [De tijd tussen twee gebeurtenissen zoeken](#twoevents)
* [Opeenvolgende gebeurteniswaarden vergelijken](#sequence)
* [Valuta converteren](#currency)
* [Tijdzones converteren](#timezone)
* [Iets anders](#else)

## Ik probeer gebeurtenissen opeenvolgend te bestellen {#compareevents}

Dit wordt genoemd een **gebeurtenis aantal** berekende kolom. Dit betekent dat u probeert de volgorde te vinden waarin gebeurtenissen zich voor een bepaalde gebeurteniseigenaar hebben voorgedaan, zoals een klant of gebruiker.

Hier volgt een voorbeeld:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00 :00: 00 | 1 |
| 2 | `B` | 2015-01-01 00 :30: 00 | 1 |
| 3 | `A` | 2015-01-01 02 :00: 00 | 2 |
| 4 | `A` | 2015-01-02 13 :00: 00 | 3 |
| 5 | `B` | 2015-01-03 13 :00: 00 | 2 |

{style="table-layout:auto"}

Een kolom met het berekende gebeurtenisaantal kan worden gebruikt om verschillen in gedrag tussen gebeurtenissen voor het eerst, herhalingsgebeurtenissen of nde gebeurtenissen in uw gegevens waar te nemen.

Wilt u de kolom met het ordernummer van de klant in actie zien? Klik het beeld om het als Groep door dimensie in een rapport te zien worden gebruikt.

![ Gebruikend een gebeurtenisaantal berekende kolom aan Groep door het de ordeaantal van de klant.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Om dit type van berekende kolom tot stand te brengen, moet u weten:

* De tabel waarop u deze kolom wilt maken
* Het veld dat de eigenaar van de gebeurtenissen identificeert (`owner\_id` in dit voorbeeld)
* Het veld waarmee u de gebeurtenissen wilt bestellen (`timestamp` in dit voorbeeld)

[Terug naar boven](#top)

## Ik probeer de tijd te vinden tussen twee gebeurtenissen. {#twoevents}

Dit wordt een `date difference` berekende kolom genoemd. Dit betekent dat u de tijd probeert te vinden tussen twee gebeurtenissen die tot één record behoren, op basis van de tijdstempels van de gebeurtenis.

Hier volgt een voorbeeld:

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00 :00: 00 | 2015-01-01 12 :30: 00 | 45000 |
| `B` | 2015-01-01 08 :00: 00 | 2015-01-01 10 :00: 00 | 7200 |

{style="table-layout:auto"}

Een kolom voor het berekende datumverschil kan worden gebruikt om een metrische waarde te maken die de gemiddelde of mediane tijd tussen twee gebeurtenissen berekent. Klik op de onderstaande afbeelding om uit te zoeken hoe de `Average time to first order` -metrische waarde wordt gebruikt in een rapport.

![ Gebruikend een kolom van het datumverschil berekende om Gemiddelde tijd aan eerste orde te berekenen.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Om dit type van berekende kolom tot stand te brengen, moet u weten:

* De tabel waarop u deze kolom wilt maken
* De twee tijdstempels waartussen u het verschil wilt weten

[Terug naar boven](#top)

## Ik probeer opeenvolgende gebeurteniswaarden te vergelijken. {#sequence}

Dit wordt genoemd de opeenvolgende gebeurtenisvergelijking van a **&#x200B;**. Dit betekent dat u probeert de delta tussen een waarde (valuta, aantal, timestamp) en de overeenkomstige waarde voor de vorige gebeurtenis van de eigenaar te vinden.

Hier volgt een voorbeeld:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00 :00: 00 | NULL |
| 2 | `B` | 2015-01-01 00 :30: 00 | NULL |
| 3 | `A` | 2015-01-01 02 :00: 00 | 7720 |
| 4 | `A` | 2015-01-02 13 :00: 00 | 126000 |
| 5 | `B` | 2015-01-03 13 :00: 00 | 217800 |

{style="table-layout:auto"}

Een opeenvolgende gebeurtenisvergelijking kan worden gebruikt om de gemiddelde of mediane tijd tussen elke opeenvolgende gebeurtenis te vinden. Klik het beeld hieronder om **Gemiddelde en Mediane tijd tussen orden** metriek in actie te zien.

= ![ Gebruikend een opeenvolgende gebeurtenisvergelijking berekende kolom om Gemiddelde en Mediane tijd tussen orden te berekenen.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Om dit type van berekende kolom tot stand te brengen, moet u weten:

* De tabel waarop u deze kolom wilt maken
* Het veld dat de eigenaar van de gebeurtenissen aangeeft (`owner\_id` in het voorbeeld)
* Het waardegebied dat u het verschil tussen voor elke opeenvolgende gebeurtenis (`timestamp` in dit voorbeeld) zou willen zien

[Terug naar boven](#top)

## Ik probeer de valuta om te zetten. {#currency}

A **berekende de muntomzetting van 0&rbrace; &lbrace;zet transactiebedragen van een geregistreerde munt in een rapporteringsmunt om, die op de wisselkoers op de gebeurtenistijd wordt gebaseerd.**

Hier volgt een voorbeeld:

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00 :00: 00 | 30 | 33,57 |
| `2` | 2015-01-02 00 :00: 00 | 50 | 55,93 |

{style="table-layout:auto"}

Om dit type van berekende kolom tot stand te brengen, moet u weten:

* De tabel waarop u deze kolom wilt maken
* De kolom met het transactiebedrag die u wilt converteren
* De kolom die de valuta aangeeft waarin de gegevens zijn opgenomen (doorgaans een ISO-code).
* De voorkeursrapporteringsvaluta

[Terug naar boven](#top)

## Ik probeer de tijdzones om te zetten. {#timezone}

De a **berekende kolom van de tijdzoneconversie van 0&rbrace; &lbrace;zet timestamps voor een bepaalde gegevensbron van hun geregistreerde timezone in rapporterende timezone om.**

Hier volgt een voorbeeld:

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00 :00: 00 | 2014-12-31 19 :00: 00 |
| `2` | 2015-01-01 12 :00: 00 | 2015-01-01 07 :00: 00 |

{style="table-layout:auto"}

Om dit type van berekende kolom tot stand te brengen, moet u weten:

* De tabel waarop u deze kolom wilt maken
* De tijdstempelkolom die u wilt converteren
* De tijdzone waarin de gegevens zijn opgenomen
* De voorkeursrapporttijdzone

[Terug naar boven](#top)

## Ik probeer iets te doen dat hier niet vermeld staat. {#else}

Geen zorgen. Dat het hier niet voorkomt, betekent niet dat het niet mogelijk is. Het Adobe team van Data Warehouse Analysts kan helpen.

Om een nieuwe berekende kolom te bepalen, [ voorlegt een steunkaartje ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) met details over precies wat u zou willen bouwen.

## Gerelateerde documentatie

* [Berekende kolommen maken](../data-warehouse-mgr/creating-calculated-columns.md)
* [Berekende kolomtypen](../data-warehouse-mgr/calc-column-types.md)
* [De bouw  [!DNL Google ECommerce]  dimensies met orde en klantengegevens](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
