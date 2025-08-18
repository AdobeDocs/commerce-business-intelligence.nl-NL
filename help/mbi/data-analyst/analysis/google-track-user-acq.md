---
title: Google Analytics - Bekijk het Source-gegevensoverzicht voor het aanschaffen van gebruikers
description: Leer hoe u uw gegevens kunt segmenteren op basis van de aankoopbron van de gebruiker.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Segmentering op basis van de aankoopbron van de gebruiker

>[!NOTE]
>
>Het onderstaande proces ondersteunt [!DNL Google Universal Analytics] niet.

De mogelijkheid om uw gegevens te segmenteren op basis van de aankoopbron van de gebruiker is van essentieel belang voor het effectief beheren van uw marketingplan. Als u de aankoopbron van nieuwe gebruikers kent, ziet u welke kanalen de beste opbrengsten opleveren en stelt u uw team in staat marketingdollars met vertrouwen toe te wijzen.

Als u de aanschafbronnen van gebruikers nog niet bijhoudt in uw database, kunt u met [!DNL Adobe Commerce Intelligence] aan de slag gaan:

## Ophaalbron van gebruiker bijhouden

[!DNL Adobe] raadt twee methoden aan om brongegevens van verwijzingen bij te houden op basis van uw instellingen:

### (Optie 1) Brongegevens voor orderverwijzing bijhouden via [!DNL Google Analytics E-Commerce]

Als u [!DNL Google Analytics E-Commerce] gebruikt om uw bestelling- en verkoopgegevens bij te houden, kunt u de [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) gebruiken om de brongegevens van elke bestelling te synchroniseren. Op deze manier kunt u inkomsten en orders segmenteren op verwijzingsbron (bijvoorbeeld `utm_source` of `utm_medium` ). U krijgt ook een idee van aanschafbronnen van klanten via [!DNL Commerce Intelligence] aangepaste afmetingen zoals `User's first order source` .

### (Optie 2) Brongegevens van de [!DNL Google Analytics] -overname opslaan in uw database

In dit onderwerp wordt uitgelegd hoe u de gegevens van het [!DNL Google Analytics] verwervingskanaal in uw eigen database kunt opslaan, namelijk de parameters `source` , `medium` , `term` , `content` , `campaign` en `gclid` die aanwezig waren op het eerste bezoek van een gebruiker aan uw website. Voor een verklaring van deze parameters, verwijs naar de [[!DNL Google Analytics]  documentatie ](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Vervolgens verkent u enkele krachtige marketinganalyses die met deze informatie in [!DNL Commerce Intelligence] kunnen worden uitgevoerd.

#### Waarom?

Als u alleen de standaard [!DNL Google Analytics] conversie- en acquisitiemetriek bekijkt, krijgt u niet het hele beeld. Terwijl het zien van het aantal omzettingen van organisch onderzoek tegenover betaalde onderzoek interessant is, wat kunt u met die informatie doen? Moet je meer geld uitgeven aan betaalde zoekopdrachten? Dat hangt af van de waarde van klanten die van dat kanaal komen, wat niet iets is dat Google Analytics biedt.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking] ](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) verlicht dit probleem door transactiegegevens in [!DNL Google Analytics] op te slaan, maar deze oplossing werkt niet voor plaatsen buiten eCommerce. Ook zijn bepaalde gereedschappen, zoals cohortanalyse, niet eenvoudig in de interface van [!DNL Google Analytics] .

Wat als u een follow-up overeenkomst aan alle klanten wilt e-mailen die van een bepaalde e-mailcampagne worden verworven? Of integreer aanschafgegevens met uw CRM-systeem? Dit is onmogelijk in [!DNL Google Analytics] - het is in feite tegen de Servicevoorwaarden voor [!DNL Google Analytics] om gegevens op te slaan die een individu identificeren. Maar je kunt deze gegevens zelf opslaan.

#### De methode

[!DNL Google Analytics] slaat de verwijzingsinformatie van de bezoeker in een koekje genoemd `__utmz` op. Nadat dit cookie is ingesteld (door de [!DNL Google Analytics] trackingcode), wordt de inhoud ervan verzonden met elke volgende aanvraag van die gebruiker naar uw domein. In PHP zou je bijvoorbeeld de inhoud van `$_COOKIE['__utmz']` kunnen uitchecken en een string zien die er ongeveer zo uitziet:

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Het is duidelijk dat er bepaalde brongegevens voor acquisities in de tekenreeks zijn gecodeerd. Dit wordt getest om te bevestigen dat dit de recentste aanschafbron van de bezoeker en bijbehorende campagnegegevens is. Nu moet u weten hoe u de gegevens kunt extraheren.

Deze code werd vertaald in a [ PHP bibliotheek die op github ](https://github.com/RJMetrics/referral-grabber-php) wordt ontvangen. Als u de bibliotheek wilt gebruiken, `include` verwijst u naar `ReferralGrabber.php` en roept u vervolgens

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

De geretourneerde `$data` -array is een kaart van de keys `source`, `medium`, `term`, `content`, `campaign`, `gclid` en hun respectievelijke waarden.

Adobe raadt u aan een tabel met de naam `user_referral` toe te voegen aan uw database met de volgende kolommen: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)` . Wanneer een gebruiker zich aanmeldt, haalt u de verwijzingsinformatie op en slaat u deze op in deze tabel.

#### Hoe deze gegevens te gebruiken

Hoe kunt u de aanschafbron van de gebruiker nu opslaan?

Stel dat u een SQL-database gebruikt en een `users` -tabel met de volgende structuur hebt:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 24-01-2012 | goochelaar | biologisch |
| 2 | jim@abc.com | 24-01-2012 | goochelaar | cpc |
| 3 | joe@def.com | 25-01-2012 | direct | - |
| 4 | jess@ghi.com | 26-01-2012 | verwijzing | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | overige | biologisch |
| ... | ... | ... | ... | ... |

Om te beginnen, kunt u het aantal gebruikers tellen die uit elk verwijzingskanaal door de volgende vraag tegen uw gegevensbestand in werking te stellen komen:

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Het resultaat ziet er ongeveer als volgt uit:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| goochelaar | 294 |
| direct | 156 |
| verwijzing | 55 |
| overige | 16 |

Dat is interessant, maar weinig nuttig. Wat u echt wilt weten is:

* Het groeitempo van deze getallen in de loop der tijd
* Het bedrag van de inkomsten die door elke verwervingsbron worden gegenereerd
* A [ cohortanalyse ](https://en.wikipedia.org/wiki/Cohort_analysis) van gebruikers die uit elke bron komen
* De waarschijnlijkheid dat een gebruiker van één van deze kanalen als klant in de toekomst zal terugkeren

De query&#39;s die nodig zijn om deze analyses uit te voeren zijn complex. Op basis van deze informatie kunt u de meest winstgevende aanschafkanalen bepalen en de marketingtijd en het geld daarop afstemmen.

### Verwante

* **[ontdekt uw waardevolste verwervingsbronnen en kanalen](../analysis/most-value-source-channel.md)**
* **[verbind uw  [!DNL Google Adwords]  rekening](../importing-data/integrations/google-adwords.md)**
* **[ROI van de verhoging op uw reclamecampagnes](../analysis/roi-ad-camp.md)**
* **[hoe werkt  [!DNL Google Analytics]  UTM attributie?](../analysis/utm-attributes.md)**
