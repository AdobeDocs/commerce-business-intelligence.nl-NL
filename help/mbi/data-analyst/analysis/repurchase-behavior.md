---
title: Gedrag voor het opnieuw aanschaffen van klanten analyseren
description: Leer hoe u het terugkoopgedrag van klanten kunt analyseren.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 1%

---

# Gedrag voor terugkerende klantenservice

Als u meer dan één product aanbiedt, vraagt u zich waarschijnlijk af hoe klanten die een specifiek product aanschaffen zich in de loop der tijd anders gedragen dan andere klanten. Dit onderwerp verkent analyses die u kunnen helpen de volgende vragen beantwoorden.

Onder klanten die een *specifiek item*,

* Hoe groot is de kans dat ze een andere aankoop doen?
* Hoe lang duurt het voordat ze een andere aankoop doen?
* Wat is het gemiddelde aantal orders dat klanten op korte of lange termijn plaatsen?
* Wat zijn de gemiddelde inkomsten die klanten op korte/lange termijn genereren?

## Aanbevolen meetwaarden

Bij het samenstellen van analyses van de terugkoopactiviteiten van klanten raadt Adobe u aan de volgende meetwaarden te gebruiken:

### Herhalingsvolgordeningswaarschijnlijkheid

Deze maatregel wordt gedefinieerd als het totale aantal herhalingsorders, als percentage van het totale aantal bestellingen. Met andere woorden, dit is de waarschijnlijkheid dat een orde door een andere orde wordt gevolgd. Deze maatregel identificeert punten die klanten waarschijnlijk zullen aansporen om terug naar uw opslag te komen.

### Gemiddeld aantal geplaatste orders

Dit stelt het aankoopgedrag van uw klanten bloot, specifiek hoeveel orden uw klanten over een bepaalde tijdspanne hebben geplaatst. U kunt deze maatregel beperken om het gedrag van klanten op korte, middellange of lange termijn te zien. Sommige producten kunnen klanten aanmoedigen om frequente aankopen op de kortere termijn te doen, terwijl anderen de loyaliteit van een klant op lange termijn kunnen beïnvloeden. Als dit aantal hoger is voor een object dan voor andere objecten, wordt voorgesteld dat kopers van dit object terugkeren naar je winkel.

### Gemiddelde omzet tijdens de levensduur van de klant

Deze metrisch staat u toe om te begrijpen of klanten die specifieke punten kopen waardevoller tijdens hun leven zijn. Als dit aantal hoger is voor één object dan voor andere objecten met vergelijkbare prijzen, kan dit erop wijzen dat uw klanten met een hogere waarde dit object doorgaans kopen.

### Tijd tot volgende bestelling

Deze maatregel toont de het bestellen frequentie van de klant, of de tijd het voor de klant neemt om opnieuw te bestellen. Als de tijd tot de volgende bestelling korter is voor een bepaald artikel in vergelijking met andere objecten, is het raadzaam dat de kopers van dit object sneller terugkeren.

## Voorbeeld van vandaag: koffieproducten

Houd bovenstaande cijfers in gedachten en bekijk een voorbeeld met koffieproducten.

| **Productnaam** | **Herhalingsvolgordeningswaarschijnlijkheid** | **Gemiddeld aantal orders tijdens de levensduur** | **Gem. inkomsten** | **Mediane tijd tot volgende bestelling** |
|-----|-----|-----|-----|-----|
| Koffiebrouwerij voor één beker | 94.98% | 7.92 | $549.82 | 57,01 dagen |
| Koffiecapsules | 93.82% | 8.68 | $479.98 | 63,48 dagen |
| Koffiebonen | 41.92% | 6.07 | $99.82 | 27,31 dagen |

{style="table-layout:auto"}

Wat betekent dit voor elk van je metriek?

### Herhalingsvolgordeningswaarschijnlijkheid

In dit voorbeeld is de waarschijnlijkheid van de herhalingsvolgorde - of de waarschijnlijkheid dat een bestelling wordt gevolgd door een andere bestelling - veel hoger voor de koffiebrouwerijen en koffiecapsules dan voor de koffiebonen.

Aangezien klanten die de brouwerij kopen zich &quot;ertoe verbinden&quot; de bijbehorende capsules te kopen, is dit logisch. Ook de klanten die capsules hebben gekocht, hebben een brouwerij die compatibel is met de capsules. koffiebonen zijn echter niet specifiek voor een bepaalde brouwerij.

### Gemiddeld aantal orders gedurende de looptijd

Op basis van bovenstaande gegevens kunt u zien dat mensen die de brouwerij of capsules kopen gemiddeld meer aankopen hebben gedaan in hun leven, vergeleken met klanten die koffiebonen hebben gekocht.

### Gemiddelde omzet tijdens de levensduur van de klant

Klanten die de brouwerij kopen, hebben de hoogste gemiddelde levensduurinkomsten, wat logisch is, aangezien de kosten van de brouwerij in deze maatregel zijn opgenomen. Daarentegen kopen klanten die koffiebonen kopen doorgaans alleen goedkope artikelen.

### Tijd tot volgende bestelling

Onder klanten die koffiecapsules hebben gekocht, maakt de helft een herhalingsbestelling in ongeveer twee maanden. Onder klanten die koffiebonen hebben aangeschaft, maakt de helft echter binnen ongeveer een maand een herhalingsbestelling. Dit kan zijn omdat mensen die capsules bestellen (1) niet zo veel koffie drinken of (2) bestellingen in bulk plaatsen (bijvoorbeeld om koffie van twee maanden in één bestelling te kopen).

## Welke andere analyses kan ik maken?

Met behulp van de metriek die in dit onderwerp wordt geschetst, kunt u andere nuttige het terugkopen analyses ook bouwen. U kunt bijvoorbeeld ook zien hoe klanten hun aankopen terugkopen **hetzelfde item** - bijvoorbeeld wanneer zij regelmatig vullingen kopen. Capsules en koffiebonen kunnen regelmatig worden teruggekocht, maar het zou onverwacht zijn als klanten de koffiebrouwerij herhaaldelijk zouden kopen. Als uw zaken zich op vult of herbevolkt concentreert, zou deze analyse nuttig zijn.

Naast het analyseren van het terugkoopgedrag van uw klanten, kunt u analyses ook bouwen die klantenloyaliteit bekijken. Overweeg patronen in klantenkring te analyseren - waar verlaten uw klanten uw plaats en komen niet terug? In welk tempo gebeurt dit?

Als u hebt vastgesteld waarom er een fout optreedt, kunt u uw analyse gebruiken om een `reactivation` campagne. Met deze gegevens kunt u gebruikers identificeren die inactief zijn geworden, hoe lang het is sinds hun laatste bezoek, wat hun laatste aankoop was, enzovoort. Dit staat u toe om actieable besluiten te nemen die uw klanten ertoe aanzetten om terug te komen.

Voor hulp bij de analyse [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
