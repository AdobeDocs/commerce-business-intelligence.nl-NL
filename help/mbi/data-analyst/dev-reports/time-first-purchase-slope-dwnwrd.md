---
title: Gemiddelde tijd tot eerste aankooprapport
description: Leer hoe u het rapport Gemiddelde tijd voor eerste aankoop gebruikt.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Gemiddelde tijd tot eerste aankooprapport

Veel Adobe-klanten hebben een metrische en diagramnaam `Average time to first purchase` die de gemiddelde tijd tussen de registratiedatum van een groep gebruikers en de eerste aankoopdatum weergeven. De gegevens slinken bijna altijd naar beneden naarmate de tijd dichter bij het heden komt.

![&#x200B; gemiddelde tijd aan eerste orde &#x200B;](../../assets/average-time-to-first-order.png)

Dit komt omdat deze nieuwere klanten nog niet de gelegenheid hebben gehad om aankopen te genereren die meer dan een maand na hun datum van toetreding zijn gedaan. Omdat gebruikers die nooit een aankoop hebben gedaan helemaal niet worden opgenomen (totdat ze wel een aankoop doen), is dit een nadeel voor nieuwere groepen klanten.

Er zijn een paar andere mogelijke manieren om naar deze metrische methode te kijken die minder vooroordelen introduceert. Onderzoek één voorbeeld.

## Voorbeeld: een `cohort` analyse van eerste bestellingen uitvoeren

U kunt een grafiek op uw `Users` dashboard hebben genoemd `Time to first order cohort`. Dit rapport gebruikt `Distinct buyers` metrisch, groepeert gebruikers door `cohort` weken of maanden van registratie, en toont de verhouding (tussen `0` en `1`) van gebruikers die een eerste aankoop in de volgende weken of maanden na registratie maakten.

In het diagram kan worden weergegeven dat voor gebruikers die in december 2014 zijn geregistreerd, `0.56` (of `56%`) een eerste bestelling per maand 2 heeft uitgevoerd (bijvoorbeeld januari 2015).

Deze cohortanalyse is een goede indicator van het activeringspercentage van de gebruiker in de loop der tijd. Als dit diagram begint met afvlakken of plateau en u nog steeds niet bijna 100% omzet in kopers, kan het tijd zijn om de resterende gebruikers via e-mailcampagnes te activeren.
