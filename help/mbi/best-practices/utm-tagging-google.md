---
title: UTM-tracking in Google Analytics
description: Meer informatie over de beste praktijken voor het bijhouden van UTM-codes in Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# UTM-tracking

`UTM` tracking is een coderingsconventie voor URL&#39;s waarmee u kunt analyseren waar uw gebruikers vandaan komen. Als u de URL&#39;s bekijkt waarop u klikt in de meeste marketingadvertenties in e-mail- of banneradvertenties, ziet u UTM-codering. Het zijn die lange links die eindigen met dingen als `utm\_source` en `utm\_medium` .

[!DNL Google Analytics] gebruikt `UTM` -tags om te weten waar uw verkeer vandaan komt. Sommige van deze informatie komt uit de [ verwijzer van HTTP ](https://en.wikipedia.org/wiki/HTTP_referer) maar de rest van het u moet van `UTM` parameters voorzien. Wanneer u `google adwords` of `email marketing` ziet, betekent dit dat de `UTM` -parameters worden opgenomen via de oorspronkelijke klik op de koppeling en vervolgens worden opgeslagen in de cookies van de gebruiker. Van daar, [!DNL Google Analytics] gebruikt dat gegevens aan [ attribuut interessant gedrag ](../data-analyst/analysis/google-track-user-acq.md) op uw plaats. Als u begrijpt wat die parameters zijn, kunt u beter begrijpen hoe u UTM-tags het beste kunt instellen en gebruiken.

## Aanbevolen procedures voor UTM-tags

De volgende lijst bevat een overzicht van de vijf belangrijkste zaken die u moet onthouden wanneer u URL&#39;s instelt met `UTM` -tags.

### &#x200B;1. Doel is elke URL waarop u het plaatsen van uw site kunt controleren, van tags te voorzien

Telkens wanneer u mensen vraagt om op een koppeling te klikken, moet u `UTM` -tags instellen. Hieronder vallen al uw e-mailkoppelingen (uw e-mailservicebureau kan uw URL&#39;s mogelijk automatisch coderen), koppelingen, drukartikelen en blogberichten.

### &#x200B;2. Maak een URL met een gereedschap

URL&#39;s met `UTM` -tags kunnen omslachtig zijn. In plaats van het proberen om hen uit lange weg te typen, gebruik een hulpmiddel [ als dit ](https://support.google.com/analytics/answer/1033867?hl=en) om u te helpen. Zo weet u zeker dat u alle nuttige parameters aan de URL wilt toevoegen en dat u de URL voor kopiëren en plakken meteen uit de URL wilt halen. Voor het beheer van sociale koppelingen bevat gereedschap zoals [!DNL Hootsuite] de optie om aangepaste URL-parameters toe te voegen aan al uw koppelingen.

### &#x200B;3. Zorg ervoor dat de parameterwaarden hoofdlettergevoelig zijn

Het is belangrijk om te onthouden dat de tag `utm\_source=adwords` een andere tag is dan `utm\_source=Adwords` . Overweeg om alles in kleine letters te maken.

### &#x200B;4. Sla de UTM-parameterwaarden op in uw database

Telkens wanneer een transactie of gebeurtenis gebeurt, wilt u de prestaties van uw marketing activiteiten evalueren. U kunt dit doen door de waarden van de UTM parameterwaarden van het [[!DNL Google Analytics]  koekje in uw gegevensbestand ](../data-analyst/analysis/google-track-user-acq.md) te lezen.

### &#x200B;5. Denk na over de naam van campagnes

Als u wilt bijhouden hoe uw marketinginspanningen in de loop der tijd verbeteren, moet u op de hoogte zijn van uw naamgevingsconventies. Houd het eenvoudig en minimaliseer het zoveel mogelijk. Gecompliceerde naamgevingssystemen zijn moeilijker te onderhouden.

Zodra u deze gegevens in uw gegevensbestand vangt, kunt u de prestaties van uw marketing en reclame door verfijnde analyse met inbegrip van [ Waarde van het Levensduur van de Klant ](../data-analyst/analysis/ess-expected-ltv.md) evalueren, [ de Tarieven van de Aankoop van de Herhaal ](../data-analyst/analysis/repurchase-behavior.md), en [ Gemiddelde Waarde van de Orde ](../data-analyst/analysis/basic-analytics.md).
