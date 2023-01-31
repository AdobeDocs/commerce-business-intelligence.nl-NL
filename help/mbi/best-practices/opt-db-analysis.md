---
title: Uw database optimaliseren voor analyse
description: Leer hoe u uw database kunt optimaliseren voor analyse.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Uw database optimaliseren

Het belangrijkste voordeel van het gebruiken van een operationeel gegevensbestand voor bedrijfsintelligentie is dat niets moet worden gebouwd of worden gewijzigd om gegevens te verzamelen. Er is al waardevolle informatie voorhanden; alles wat je hoeft te doen is het ontgrendelen.

Dit onderwerp bevat een aantal aanbevelingen om u te helpen uw gegevensbestand voor analyse optimaliseren en actionable inzichten van ruwe gegevens trekken.

## Gegevens niet verwijderen

>[!TIP]
>
>De lokale en internationale wetten die uw zaken (en uw eigen termijnen van de dienst) beïnvloeden kunnen beïnvloeden welke types van gegevens u kunt behouden en hoe lang u het kunt bewaren voor. Naleving van deze wetten zou uw eerste prioriteit moeten zijn.

Wanneer een bestelling wordt geannuleerd, een gebruiker zijn account deactiveert of een product wordt stopgezet, is het verleidelijk om de bijbehorende informatie in de database te verwijderen. Tabellen groeien en rommel verwijderen lijkt een verstandig idee. Nochtans, betekent het schrappen van rijen dat deze informatie voor altijd verloren gaat of dat u door oude steunen zult moeten graven om het te vinden.

In plaats daarvan kunt u een statuskolom aan de tabel toevoegen die aangeeft wanneer de rij niet meer actief of relevant is. Het wordt ook geadviseerd om een kolom toe te voegen die de datum opslaat de verandering werd aangebracht, of een logboek voor historische veranderingen tot stand te brengen. Als tabellen groot genoeg worden om de prestaties te verminderen, kunt u de oude gegevens archiveren tot een tabel die wordt gebruikt voor analyses.

## Gegevens zelden overschrijven

Het overschrijven van gegevens moet spaarzaam en met voorzichtigheid gebeuren.

Gebruikend login data als voorbeeld, zullen vele bedrijven de laatste login datum eerder dan een lijst van historische logins opslaan. Hoewel u de laatste aanmeldingsdatum alleen nodig hebt voor functionele doeleinden, zijn deze overschreven gegevens een groot verlies voor de analyse. Als u geen volledig logboek van deze acties bijhoudt, kunt u niet zien hoeveel gebruikers gedurende lange tijd weg zijn gebleven en vervolgens opnieuw zijn geactiveerd. Het maakt het ook onmogelijk om dingen zoals de cohortanalyses van de gebruikersbetrokkenheid op basis van logins te bouwen.

Als u een record bijwerkt als gevolg van een actie van een gebruiker, moet u in het algemeen geen informatie overschrijven over een eerdere of aparte actie van een gebruiker.

## Inclusief `Updated_at` Kolommen voor gegevens die in de loop der tijd zijn bijgewerkt

Als de waarden van rijen van een tabel in de loop der tijd veranderen, bijvoorbeeld **order\_status** wijzigingen van`processing` tot `complete`, omvat een **bijgewerkt\_op** kolom om op te nemen wanneer de recentste verandering voorkomt. Zorg ervoor dat een **bijgewerkt\_op** Deze waarde is beschikbaar wanneer u de nieuwe gegevensrij voor het eerst invoegt. Op dat moment wordt de **bijgewerkt\_op** datum komt overeen met de **gemaakt\_op** datum.

Naast optimalisering voor analyse, **bijgewerkt\_op** ook kunt u kolommen gebruiken [Incrementele replicatiemethoden](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), waardoor de duur van de updatecycli kan worden verkort.

## Ophaalbron van gebruiker opslaan

Een van de meest voorkomende fouten is de [aankoopbron gebruiker](../data-analyst/analysis/google-track-user-acq.md) (UAS) die niet in het operationele gegevensbestand wordt opgeslagen. In de meeste situaties waarin dit een probleem is, wordt de UAS alleen gevolgd [!DNL Google Analytics] of een ander hulpprogramma voor webanalyse. Hoewel deze instrumenten uiterst waardevol kunnen zijn, zijn er enkele nadelen om UAS in hen uitsluitend op te slaan; U kunt bijvoorbeeld geen gegevens op gebruikersniveau uit deze gereedschappen extraheren. Wanneer dat mogelijk is, is het meestal een moeilijk proces. Het zou gemakkelijk moeten zijn om deze informatie te krijgen en het met gegevens uit andere bronnen, zoals gedragsinformatie en transactionele informatie te combineren die ook in uw gegevensbestand wordt opgeslagen.

Het opslaan van UAS in uw eigen gegevensbestand is vaak de grootste verbetering een online zaken aan zijn analytische mogelijkheden kunnen maken. Dit staat voor de analyse van verkoop, gebruikersovereenkomst, terugbetalingsperioden, waarde van het klantenleven, prijs, en andere kritieke metriek door UAS toe. [Deze gegevens zijn van cruciaal belang wanneer u bepaalt waar u marketingmiddelen wilt investeren](../data-analyst/analysis/most-value-source-channel.md).

Te veel bedrijven richten zich uitsluitend op het zoeken naar kanalen die nieuwe gebruikers tegen de laagste kosten voorzien, maar als u de kwaliteit van gebruikers niet volgt die van elk kanaal worden verworven, loopt u het risico om gebruikers aan te trekken die geen bedrijfswaarde produceren.

## Gegevenstabelinstelling

### Primaire sleutel instellen

A [primaire sleutel](http://en.wikipedia.org/wiki/Unique_key) is een onveranderlijke kolom (of een reeks kolommen) die unieke waarden binnen een lijst veroorzaakt. Primaire toetsen zijn ongelooflijk belangrijk, omdat ze ervoor zorgen dat uw tabellen correct worden gerepliceerd in [!DNL MBI].

Gebruik bij het bouwen van primaire sleutels een gegevenstype voor gehele getallen voor de kolom die automatisch wordt verhoogd. We raden u ook aan om waar mogelijk het gebruik van meerdere primaire kolomsleutels te vermijden.

Als uw tabel een SQL-weergave is, voegt u een kolom toe die als primaire sleutel kan fungeren. [!DNL MBI] kan deze kolom automatisch identificeren als een primaire sleutel.

### Een gegevenstype toewijzen aan uw gegevenskolom

Als een gegevenskolom geen toegewezen [gegevenstype](http://en.wikipedia.org/wiki/Data_type), [!DNL MBI] Hiermee raden we welk gegevenstype u wilt gebruiken. Als het systeem verkeerd gokt, kunt u niet de relevante analyses kunnen uitvoeren tot ons ondersteuningsteam de kolom aan het juiste gegevenstype aanpast. Als een datumkolom bijvoorbeeld als een numeriek gegevenstype wordt geraden, kunt u zich in de loop van de tijd ontwikkelen met die datumdimensie.

### Voeg prefixen aan uw Lijsten van Gegevens toe als u veelvoudige Gegevensbestanden hebt

Als er meerdere databases zijn verbonden met [!DNL MBI]We raden u aan voorvoegsels aan uw tabellen toe te voegen om verwarring te voorkomen. Met voorvoegsels kunt u zich herinneren van waaruit metriek- of gegevensafmetingen afkomstig zijn.
