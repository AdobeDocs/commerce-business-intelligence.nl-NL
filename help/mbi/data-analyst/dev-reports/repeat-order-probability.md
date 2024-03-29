---
title: Rapport voor waarschijnlijkheid van bestelling herhalen
description: Leer en begrijp het rapport Herhalingskans bestelling.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Rapport voor waarschijnlijkheid van bestelling herhalen

## Wanneer is het `Incremental Event Probability` perspectief beschikbaar?

De `incremental event probability` perspectief is alleen beschikbaar wanneer filters afmetingen gebruiken die gelijk zijn voor alle bestellingen (bijvoorbeeld `gender`, gebruikers `age` of van gebruikers `source`).

Dit is omdat dit perspectief afhankelijk is van een dimensie die `User's order number` voor segmentatie, die de aankopen van een gebruiker (bijvoorbeeld, eerste, tweede, en 3de orden van John) nummert.

Als u een filter hebt toegevoegd dat een dimensie gebruikt die niet gelijk is voor alle orders (bijvoorbeeld `Order's Region`), `User's order number` de dimensie zou niet langer accuraat zijn . Dit is omdat het geen rekening voor specifieke gebieden wanneer het nummeren van de orden van een gebruiker (bijvoorbeeld, zijn de eerste, tweede, derde orden van John nog het zelfde, ongeacht hun regio).

## Het veranderen van een orde-specifieke afmeting in een gebruiker-specifieke afmeting

In bepaalde gevallen kunt u `order-specific` dimensie in een `user-specific` dimensie die als filter moet worden toegevoegd in het dialoogvenster `Repeat Order Probability` grafiek. In deze gevallen retourneert u het orderkenmerk van de eerste of laatste volgorde van een gebruiker (bijvoorbeeld de naam van het eerste bestelgebied van de gebruiker).

Als u zo&#39;n nieuwe dimensie wilt creëren, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Herhalingswaarschijnlijkheid van orders met verschillende kenmerken vergelijken

Om het aantal herhaalde aankopen voor verschillende ordekenmerken (bijvoorbeeld, orde te vergelijken `region`), raadt Adobe aan een grafiek te maken die lijkt op `Users by lifetime number of orders`. Dit toont u het aantal gebruikers dat 1, 2, 3,... levenslevensaantal orden maakte, en voegt de filter van het ordeniveau toe. (Met andere woorden, dit kan u tonen of de gebruikers meer of minder herhaalde aankopen in één regio of een andere. maken)

De getallen waaruit een dergelijk diagram bestaat, kunnen vervolgens worden geëxporteerd naar Excel om de waarschijnlijkheidsverhouding van de herhaalde volgorde te berekenen. De waarschijnlijkheid van klanten die `(x)` bestellingen `(x+1)` bestellingen, eenvoudig` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` aankopen.

### Voorbeeld:

| Categorie | Waarde |
|---|---|
| Aantal klanten die 1 aankoop in hun leven hebben gedaan | `90` |
| Aantal klanten die twee aankopen hebben gedaan tijdens hun levensduur | `30` |
| Aantal klanten dat tijdens hun levensduur 3 aankopen heeft gedaan | `10` |
| De waarschijnlijkheid van de herhaalde orde van klanten die één aankoop in hun leven hebben gemaakt om een tweede aankoop te maken | `(30 + 10) / (30+10+90) = 30.77%` |
