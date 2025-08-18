---
title: Uw database optimaliseren voor analyse
description: Leer hoe u uw database kunt optimaliseren voor analyse.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Uw database optimaliseren

Het belangrijkste voordeel van het gebruik van een operationele database voor [!DNL Adobe Commerce Intelligence] is dat er niets hoeft te worden gemaakt of gewijzigd om gegevens te verzamelen. Waardevolle informatie is er al. U hoeft deze alleen maar te ontgrendelen.

Dit onderwerp bevat een aantal aanbevelingen om u te helpen uw gegevensbestand voor analyse optimaliseren en actionable inzichten van ruwe gegevens trekken.

## Gegevens niet verwijderen

>[!TIP]
>
>De lokale en internationale wetten die uw zaken (en uw eigen termijnen van de dienst) beïnvloeden kunnen beïnvloeden welke types van gegevens u kunt behouden en hoe lang u het kunt bewaren voor. Naleving van deze wetten zou uw eerste prioriteit moeten zijn.

Wanneer een bestelling wordt geannuleerd, een gebruiker zijn account deactiveert of een product wordt stopgezet, is het verleidelijk om de bijbehorende informatie in de database te verwijderen. Tabellen groeien en rommel verwijderen lijkt een verstandig idee. Als u echter rijen verwijdert, gaat deze informatie voorgoed verloren of moet u oude back-ups doorzoeken om deze te vinden.

In plaats daarvan kunt u een statuskolom aan de tabel toevoegen die aangeeft wanneer de rij niet langer actief of relevant is. Het wordt ook geadviseerd om een kolom toe te voegen die de datum opslaat de verandering werd aangebracht, of een logboek voor historische veranderingen tot stand te brengen. Als tabellen groot genoeg worden om de prestaties te verminderen, kunt u de oude gegevens archiveren tot een tabel die wordt gebruikt voor analyses.

## Gegevens zelden overschrijven

Het overschrijven van gegevens moet spaarzaam en met voorzichtigheid gebeuren.

Gebruikend login data als voorbeeld, slaan vele bedrijven de laatste login datum eerder dan een lijst van historische logins op. Hoewel u de laatste aanmeldingsdatum alleen nodig hebt voor functionele doeleinden, zijn deze overschreven gegevens een groot verlies voor de analyse. Als u geen volledig logboek van deze acties bijhoudt, kunt u niet zien hoeveel gebruikers gedurende lange tijd weg zijn gebleven en vervolgens opnieuw zijn geactiveerd. Het maakt het ook onmogelijk om dingen zoals de cohortanalyses van de gebruikersbetrokkenheid op basis van logins te bouwen.

Als u een record bijwerkt door een handeling van een gebruiker, moet u de informatie over een eerdere of aparte handeling van de gebruiker over het algemeen niet overschrijven.

## Inclusief `Updated_at` kolommen voor gegevens die in de loop der tijd zijn bijgewerkt

Als de rijen van een lijst veranderende waarden in tijd zullen hebben, bijvoorbeeld, **orde \_status** veranderingen van `processing` in `complete`, omvat een **bijgewerkte \_at** kolom om te registreren wanneer de recentste verandering voorkomt. Zorg ervoor dat een **bijgewerkte \_bij** waarde beschikbaar is wanneer eerst het opnemen van de nieuwe gegevensrij, wanneer de **bijgewerkte \_bij** datum aan **gecreeerd \_bij** datum beantwoordt.

Naast het optimaliseren voor analyse, **bijgewerkt \_bij** kolommen staat u ook toe om [ de Incrementele methodes van de Replicatie ](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) te gebruiken, die de lengte van uw updatecycli kunnen helpen verkorten.

## Ophaalservice Source van winkelgebruiker

Één van de gemeenschappelijkste fouten is de [ bron van de gebruikersverwerving ](../data-analyst/analysis/google-track-user-acq.md) (UAS) niet die in het operationele gegevensbestand wordt opgeslagen. In de meeste situaties waarin dit een probleem is, worden UAS alleen bijgehouden via [!DNL Google Analytics] of een ander hulpprogramma voor webanalyse. Hoewel deze gereedschappen waardevol kunnen zijn, zijn er enkele nadelen om UAS uitsluitend in de gereedschappen op te slaan. U kunt bijvoorbeeld geen gegevens op gebruikersniveau uit deze gereedschappen extraheren. Wanneer dat mogelijk is, is het meestal een moeilijk proces. Het zou gemakkelijk moeten zijn om deze informatie te krijgen en het met gegevens uit andere bronnen, zoals gedragsinformatie en transactionele informatie te combineren die ook in uw gegevensbestand wordt opgeslagen.

Het opslaan van UAS in uw eigen gegevensbestand is vaak de grootste verbetering die een online zaken aan zijn analytische mogelijkheden kan maken. Dit staat voor de analyse van verkoop, gebruikersovereenkomst, terugbetalingsperioden, waarde van het klantenleven, prijs, en andere kritieke metriek door UAS toe. [ Dit gegeven is cruciaal wanneer het beslissen waar te om marketing middelen ](../data-analyst/analysis/most-value-source-channel.md) te investeren.

Te veel bedrijven richten zich uitsluitend op het vinden van kanalen die nieuwe gebruikers tegen de laagste kosten voorzien. Als u de kwaliteit van gebruikers die via elk kanaal zijn opgehaald niet bijhoudt, loopt u het risico gebruikers aan te trekken die geen bedrijfswaarde genereren.

## Gegevenstabelinstelling

### Primaire sleutel instellen

A [ primaire sleutel ](https://en.wikipedia.org/wiki/Unique_key) is een onveranderlijke kolom (of reeks kolommen) die unieke waarden binnen een lijst veroorzaakt. Primaire toetsen zijn ongelooflijk belangrijk, omdat ze ervoor zorgen dat uw tabellen correct worden gerepliceerd in [!DNL Commerce Intelligence] .

Gebruik bij het bouwen van primaire sleutels een gegevenstype voor gehele getallen voor de kolom die automatisch wordt verhoogd. Adobe raadt u aan zoveel mogelijk het gebruik van meerdere primaire kolomsleutels te vermijden.

Als uw tabel een SQL-weergave is, voegt u een kolom toe die als primaire sleutel kan fungeren. [!DNL Commerce Intelligence] kan deze kolom automatisch identificeren als een primaire sleutel.

### Een gegevenstype toewijzen aan uw gegevenskolom

Als een gegevenskolom geen toegewezen [ gegevenstype ](https://en.wikipedia.org/wiki/Data_type) heeft, [!DNL Commerce Intelligence] gokt welk gegevenstype aan gebruik. Als het systeem verkeerd gokt, kunt u niet de relevante analyses kunnen uitvoeren tot het de steunteam van Adobe de kolom aan het juiste gegevenstype aanpast. Als een datumkolom bijvoorbeeld wordt geraden als een numeriek gegevenstype, kunt u zich in de loop van de tijd ontwikkelen met die datumdimensie.

### Voeg prefixen aan uw Lijsten van Gegevens toe als u veelvoudige Gegevensbestanden hebt

Als u meer dan één database hebt aangesloten op [!DNL Commerce Intelligence] , raadt Adobe u aan om voorvoegsels aan uw tabellen toe te voegen om verwarring te voorkomen. Met voorvoegsels kunt u onthouden van waar metrische gegevens of gegevensdimensies vandaan komen.
