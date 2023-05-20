---
title: UTM bijhouden in Google Analytics
description: Meer informatie over de beste praktijken voor het bijhouden van UTM-codes (tagging) in Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM-tracking

`UTM` bijhouden is een coderings Conventie voor Url&#39;s waarmee u kunt analyseren waar uw gebruikers vandaan komen. Als je de Url&#39;s ziet waarop je klikt van de meeste marketing-mail-of banneradvertenties, zie je UTM codering. Dit zijn de lange koppelingen die eindigen op zaken als `utm\_source` en `utm\_medium` .

[!DNL Google Analytics] gebruikt `UTM` codering om te weten te komen waar het verkeer vandaan komt. Een deel van deze informatie is afkomstig van de [ http-verwijzings ](https://en.wikipedia.org/wiki/HTTP_referer) functie, maar de rest ervan, moet u zelf aan parameters door `UTM` geven. Wanneer u het bestand ziet `google adwords` of `email marketing` , worden de parameters die `UTM` u van de oorspronkelijke koppeling hebt vastgelegd, geklikt en vervolgens opgeslagen in de cookies van gebruikers. [!DNL Google Analytics]Hiermee gebruikt u deze gegevens om het kenmerk interessant gedrag ](../data-analyst/analysis/google-track-user-acq.md) op uw site te [ kenmerken. Leer hoe u deze parameters kunt gebruiken om te leren hoe u UTM-codering het beste kunt instellen en gebruiken.

## Aanbevolen procedures voor het coderen van UTM

Hier volgt een overzicht van de belangrijkste vijf belangrijkste zaken die u kunt onthouden bij het instellen van uw Url&#39;s met `UTM` codering.

### 1. streeft ernaar een label te geven voor elke URL die u kunt controleren op uw site

Telkens wanneer u personen vraagt om op een koppeling te klikken, dient u codering in te stellen `UTM` . Dit geldt ook voor al uw e-mail koppelingen (uw e-mail serviceprovider heeft een manier om uw Url&#39;s automatisch te labelen), ad links, pers artikelen, blogberichten.

### 2. Een gereedschap gebruiken om de URL te maken

`UTM`gelabelde Url&#39;s kunnen omslachtig zijn. In plaats van te proberen om deze te typen uit lange versie, gebruikt u een dergelijk ](https://support.google.com/analytics/answer/1033867?hl=en) hulpmiddel [ om u te helpen. Dit zorgt ervoor dat u alle bedachte parameters aan de URL toevoegt en u krijgt de URL die u kunt kopiëren-plakken. Voor het beheren van sociale koppelingen [!DNL Hootsuite] kunt u bijvoorbeeld de volgende opties gebruiken om aangepaste URL-parameters toe te voegen aan al uw koppelingen.

### 3. Zorg ervoor dat u hoofdlettergevoelig bent in de parameterwaarden

Het is belangrijk te weten dat de tag `utm\_source=adwords` een andere code is dan `utm\_source=Adwords` . Maak een voorbeeld van wat kleine letters.

### 4. Sla de waarden voor de UTM-parameters op in uw database

Telkens wanneer een transactie of gebeurtenis optreedt, wilt u de prestaties van uw marketingactiviteiten evalueren. U kunt dit doen door de waarden van de UTM-parameterwaarden van de [[!DNL Google Analytics]  cookie te lezen in uw database ](../data-analyst/analysis/google-track-user-acq.md) .

### 5. denk eens aan de naam van campagnes

Als u wilt bijhouden hoe uw marketinginspanningen in de loop der tijd verbeteren, moet u op de hoogte zijn van uw naamgevingsconventies. Houd het eenvoudig en minimaliseer het zoveel mogelijk. Gecompliceerde naamgevingssystemen zijn moeilijker te onderhouden.

Zodra u deze gegevens in uw gegevensbestand vangt, kunt u de prestaties van uw marketing en reclame door verfijnde analyse evalueren met inbegrip van [Levensduur van klant](../data-analyst/analysis/ess-expected-ltv.md), [Aankooptarieven herhalen](../data-analyst/analysis/repurchase-behavior.md), en [Gemiddelde bestelwaarde](../data-analyst/analysis/basic-analytics.md).
