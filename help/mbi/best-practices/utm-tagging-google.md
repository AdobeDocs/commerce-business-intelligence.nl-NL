---
title: UTM-tracking in Google Analytics
description: Meer informatie over de beste praktijken voor het bijhouden van UTM-codes (tagging) in Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM-tracking

`UTM` het volgen is een etiketteringsovereenkomst voor URLs die u toelaat om te analyseren waar uw gebruikers komen van. Als u de URL&#39;s bekijkt waarop u klikt in de meeste marketingadvertenties in e-mail- of banneradvertenties, ziet u UTM-codering. Het zijn die lange verbindingen die eindigen met dingen als `utm\_source` en `utm\_medium`.

[!DNL Google Analytics] gebruik `UTM` labelen om te weten waar uw verkeer vandaan komt. Een deel van deze informatie is afkomstig uit de [HTTP-referentie](https://en.wikipedia.org/wiki/HTTP_referer) maar de rest moet je zelf bevoorraden `UTM` parameters. Wanneer u ziet `google adwords` of `email marketing`, betekent het `UTM` De parameters die van de originele verbinding worden geregistreerd klikken en dan opgeslagen in de koekjes van gebruikers. Van daaruit, [!DNL Google Analytics] gebruikt die gegevens aan [interessant gedrag voor kenmerken](../data-analyst/analysis/google-track-user-acq.md) op uw site. Als u begrijpt wat die parameters zijn, kunt u beter begrijpen hoe u UTM-tags het beste kunt instellen en gebruiken.

## Aanbevolen procedures voor UTM-codering

De volgende lijst maakt een lijst van de vijf belangrijkste dingen om te herinneren wanneer vestiging uw URLs met `UTM` labelen.

### 1. Doel is om elke URL waarop u het komen naar uw site kunt controleren, van een tag te voorzien

Telkens als u mensen vraagt om een verbinding te klikken, zou u opstelling moeten zijn `UTM` labelen. Hieronder vallen al uw e-mailkoppelingen (uw e-mailservicebureau kan uw URL&#39;s mogelijk automatisch coderen), koppelingen, drukartikelen en blogberichten.

### 2. Een gereedschap gebruiken om de URL te maken

`UTM`URL&#39;s met codes kunnen omslachtig zijn. Gebruik een gereedschap in plaats van ze langer te typen [zoals dit](https://support.google.com/analytics/answer/1033867?hl=en) om u te helpen. Zo weet u zeker dat u alle nuttige parameters aan de URL wilt toevoegen en dat u de URL voor kopiëren en plakken meteen uit de URL wilt halen. Voor het beheren van sociale koppelingen, gereedschappen zoals [!DNL Hootsuite] bevat de optie om aangepaste URL-parameters toe te voegen aan al uw koppelingen.

### 3. Zorg ervoor dat de parameterwaarden hoofdlettergevoelig zijn

Het is belangrijk te onthouden dat de tag `utm\_source=adwords` is een andere tag dan `utm\_source=Adwords`. Overweeg om alles in kleine letters te maken.

### 4. Sla de UTM-parameterwaarden op in uw database

Telkens wanneer een transactie of gebeurtenis gebeurt, wilt u de prestaties van uw marketing activiteiten evalueren. U kunt dit doen door de waarden van de UTM-parameterwaarden van de [[!DNL Google Analytics] cookie in uw database](../data-analyst/analysis/google-track-user-acq.md).

### 5. Denk na over hoe u campagnes noemt

Als u wilt bijhouden hoe uw marketinginspanningen in de loop der tijd verbeteren, moet u op de hoogte zijn van uw naamgevingsconventies. Houd het eenvoudig en minimaliseer het zoveel mogelijk. Gecompliceerde naamgevingssystemen zijn moeilijker te onderhouden.

Zodra u deze gegevens in uw gegevensbestand vangt, kunt u de prestaties van uw marketing en reclame door verfijnde analyse evalueren met inbegrip van [Levensduur van klant](../data-analyst/analysis/ess-expected-ltv.md), [Aankooptarieven herhalen](../data-analyst/analysis/repurchase-behavior.md), en [Gemiddelde bestelwaarde](../data-analyst/analysis/basic-analytics.md).
