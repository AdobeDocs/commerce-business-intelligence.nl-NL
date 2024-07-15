---
title: Consolideer uw tabellen
description: Leer hoe u uw tabellen en databases kunt consolideren.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Consolideer uw tabellen

Als u veelvoudige opslagfronten of op veelvoudige markten in werking stelt, kunt u gelijkaardige gegevensbestanden hebben die afzonderlijk worden opgeslagen. In [!DNL Adobe Commerce Intelligence] is het eenvoudig om vergelijkbare tabellen uit verschillende databases samen te voegen.

U hebt bijvoorbeeld een `orders` tabel voor `Market A` en een vergelijkbare `orders` tabel voor `Market B` . Met [!DNL Commerce Intelligence] kunt u beide tabellen samenvoegen en de gegevens van de geaggregeerde volgorde van zowel `Market A` als `B` bekijken. Daarnaast kunt u de tabellen segmenteren op basis van specifieke markten.

Voor consolidatie van lijsten aan het werk, moeten de inputlijsten **zo ook gestructureerd** zijn. Met andere woorden, alle inputlijsten moeten de gegevenskolommen bevatten die in de geconsolideerde lijst worden vereist.

In dit onderwerp worden enkele van de meest gebruikte gevallen voor geconsolideerde tabellen en de volgende stappen voor het maken van uw eigen tabellen besproken.

## Recommendations for When to Use Consolidated Tables

In het volgende gedeelte wordt besproken wanneer het aangewezen is geconsolideerde tabellen in uw systeem te gebruiken.

### Gegevens van meerdere websites integreren

Als u uw producten onder verschillende merken en websites verkoopt, is het waarschijnlijk dat de tabellen voor elk merk of website op dezelfde manier zijn gestructureerd.

U hebt bijvoorbeeld een `orders` tabel voor websites `A` en een aparte, maar vergelijkbare `orders` tabel voor websites `B` . In dit geval kan het handig zijn om de `orders` tabellen van website `A` en `B` te consolideren. Hier kunt u kijken naar de geconsolideerde inkomsten en het aantal bestellingen van websites `A` en `B` . Bovendien kunt u metingen segmenteren voor deze twee websites.

### Oudere gegevens integreren

Vele bedrijven hebben hun gegevensbestanden in één keer of een andere refactored, en de gegevens van het oude gegevensbestand worden niet altijd omgezet over in het nieuwe systeem. U kunt geconsolideerde lijsten gebruiken om de zeer belangrijke kolommen van erfenislijsten met die van het actieve systeem samen te voegen. Dit staat u toe om een verenigde analyse van uw gegevens door geschiedenis te leiden.

### Gebeurtenissen combineren voor actieve gebruikersanalyse

Stel je een website voor waar gebruikers verschillende dingen kunnen doen: een enquête houden, een spel spelen, een aankoop doen, een vriend doorverwijzen enzovoort. Meestal wordt elk van deze gebeurtenissen in een eigen tabel opgeslagen. Dit maakt het moeilijk om te analyseren hoeveel afzonderlijke gebruikers in een bepaalde periode ten minste één actie van welke aard dan ook hebben ondernomen.

U kunt geconsolideerde tabellen gebruiken om één uniforme lijst van alle gebruikers te maken en wanneer een van deze gebeurtenissen heeft plaatsgevonden. U kunt dan vragen op de geconsolideerde lijst in werking stellen om zulk een analyse gemakkelijk te leiden.

Zoals met alle andere lijsten in uw Data Warehouse, kunt u extra kolommen toevoegen om verschillende soorten grafieken en analyses te aandrijven.

## Een geconsolideerde tabel maken, weergeven of bijwerken

Als u in het toevoegen van een geconsolideerde lijst aan uw Data Warehouse geinteresseerd bent, contacteer [!DNL Commerce Intelligence] [ steun ](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Omdat geconsolideerde tabellen niet kunnen worden weergegeven in de `Data Warehouse Manager` , kan het weergeven en bijwerken van deze tabellen alleen worden uitgevoerd door [!DNL Commerce Intelligence] -ondersteuning.
