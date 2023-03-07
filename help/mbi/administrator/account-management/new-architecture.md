---
title: Nieuwe architectuur
description: Leer meer over de voordelen van een overstap naar een nieuwe architectuur.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nieuwe architectuur

MBI Product- en Engineering-teams hebben zich het afgelopen jaar geconcentreerd op het mogelijk maken van de meest verstrekkende, hoogst gevraagde verbeteringen. Adobe is blij om de beschikbaarheid van een nieuwe [!DNL MBI] productarchitectuur die deze verbeteringen werkelijkheid maakt.

## Voordelen van nieuwe architectuur

* Creeer types van kolommen in de Data Warehouse, met inbegrip van berekende kolommen met SQL.
* Er zijn direct nieuwe kolommen beschikbaar.
* De latentie van gegevens is aanzienlijk verbeterd.

## Technische voordelen

De belangrijkste verschillen worden hierboven vermeld, maar de belangrijkste verandering is de manier berekeningen tijdens de updatecyclus worden uitgevoerd. Berekeningen worden niet meer op elke kolom uitgevoerd tijdens elke update. zij worden in plaats daarvan in werking gesteld op bestelling van Visual Report Builder.

### Naar nieuwe architectuur

Aangezien de rekeningen fundamenteel verschillend worden gebouwd, is er geen automatisch proces om uw Data Warehouse of rapporten aan een nieuwe architectuurrekening te migreren. Als u naar de nieuwe architectuur gaat, moet uw bestaande account opnieuw worden geïmplementeerd.

### Kosten voor overstap naar de nieuwe architectuur

Geen extra kosten! Adobe maakt dit nieuwe account zodat u kunt beginnen met de herimplementatie, die minstens een maand gratis is. Dit staat u tijd toe om beide rekeningen open te hebben zodat u de herimplementatie gemakkelijker kunt uitvoeren en ervoor zorgt dat uw team geen hiaat in de dienst heeft.

### Tijd nodig om account opnieuw te implementeren in de nieuwe architectuur

De tijden van implementatie variëren afhankelijk van wat u wilt herbouwen. Adobe raadt u aan de volgende stappen in uw bestaande account uit te voeren om een idee te krijgen van wat er nodig is voor de herimplementatie:

* Een kernset rapporten/dashboards identificeren.
* Bepaal metriek en afmetingen die worden vereist om die rapporten te bouwen.
* Identificeer de kolommen die worden vereist om die metriek en afmetingen opnieuw te maken.

Wanneer dit volledig is, weet u welke gegevens u aan synchronisatie aan de nieuwe architectuurData Warehouse moet om die kernrapporten te herbouwen.

### Help opvragen

De [!DNL MBI] Het team van de diensten kan uw herimplementatie voor extra kosten uitvoeren. Neem contact op met uw [Adobe-accountteam](../../guide-overview.md) en zijn voorbereid om een lijst van dashboards/rapporten te verstrekken die u het creëren in de nieuwe rekening wilt voorrang geven

### Blijven werken met bestaande architectuur

Als deze functies voor u niet belangrijk zijn, kunt u zich bij uw bestaande account houden. Er zijn geen extra kosten voor het bijhouden van uw bestaande account. Adobe blijft deze accounts zonder wijzigingen steunen.
