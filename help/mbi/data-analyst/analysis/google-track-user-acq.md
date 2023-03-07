---
title: Google Analytics - het Overzicht van de Gegevens van de Bron van de Aankoop van de Gebruiker van het spoor
description: Leer hoe u uw gegevens kunt segmenteren op basis van de aankoopbron van de gebruiker.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: ad95a03193853eebf2b695cd6f5c3cb5a9837f93
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Segmentering op basis van de aankoopbron van de gebruiker

>[!NOTE]
>
>Het onderstaande proces ondersteunt niet [!DNL GoogleUniversal Analytics].

De mogelijkheid om uw gegevens te segmenteren op basis van de aankoopbron van de gebruiker is van essentieel belang voor het effectief beheren van uw marketingplan. Als u de aankoopbron van nieuwe gebruikers kent, ziet u welke kanalen de beste opbrengsten opleveren en stelt u uw team in staat marketingdollars met vertrouwen toe te wijzen.

Als u de aanschafbronnen van gebruikers nog niet bijhoudt in uw database, [!DNL MBI] kunt u helpen aan de slag te gaan:

## Ophaalbron van gebruiker bijhouden

Adobe raadt twee methoden aan om brongegevens van verwijzingen te volgen op basis van uw setup:

### (Optie 1) Brongegevens voor verwijzing bijhouden via [!DNL Google Analytics E-Commerce] (Inclusief [!DNL Shopify] Winkels)

Als u [!DNL Google Analytics E-Commerce] om uw bestelling en verkoopgegevens te volgen, kunt u [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) om de brongegevens van elke opdracht te synchroniseren. Dit staat u toe om opbrengst en bevelen door verwijzingsbron (bijvoorbeeld) te segmenteren `utm_source` of `utm_medium`). U krijgt ook een gevoel van bronnen voor klantaankopen via [!DNL MBI] aangepaste afmetingen zoals `User's first order source`.

>[!NOTE]
>
>Voor gebruikers van Shopify*: Inschakelen [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) voordat u verbinding maakt met uw [!DNL Google Analytics E-Commerce] account aan [!DNL MBI].

### (Optie 2) Opslaan [!DNL Google Analytics]&#39; brongegevens in de database verkrijgen

In dit artikel wordt uitgelegd hoe u het bestand opslaat [!DNL Google Analytics] de informatie van het verwervingskanaal in uw eigen gegevensbestand - namelijk `source`, `medium`, `term`, `content`, `campaign`, en `gclid` parameters die aanwezig waren op het eerste bezoek van een gebruiker aan uw website. Voor een uitleg van deze parameters raadpleegt u de [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Vervolgens verkent u enkele krachtige marketinganalyses die met deze informatie kunnen worden uitgevoerd in [!DNL MBI].

#### Waarom?

Als u alleen naar de standaardinstelling kijkt [!DNL Google Analytics] conversie- en acquisitiemetriek, u krijgt niet het hele beeld. Terwijl het zien van het aantal omzettingen van organisch onderzoek tegenover betaalde onderzoek interessant is, wat kunt u met die informatie doen? Moet je meer geld uitgeven aan betaalde zoekopdrachten? Dat hangt af van de waarde van klanten die uit dat kanaal komen, wat niet iets Google Analytics verstrekt is.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) verhelpt dit probleem door transactiegegevens op te slaan in [!DNL Google Analytics], maar deze oplossing werkt niet voor niet-eCommerce-sites. Ook zijn bepaalde gereedschappen, zoals cohortanalyse, niet eenvoudig in de [!DNL Google Analytics] interface.

Wat als u een follow-up overeenkomst aan alle klanten wilt e-mailen die van een bepaalde e-mailcampagne worden verworven? Of integreer aanschafgegevens met uw CRM-systeem? Dit is onmogelijk in [!DNL Google Analytics] - in feite is het tegen de Servicevoorwaarden voor [!DNL Google Analytics] om gegevens op te slaan die een individu identificeren. Maar je kunt deze gegevens zelf opslaan.

#### De methode

[!DNL Google Analytics] slaat verwijzingsinformatie van de bezoeker in genoemd koekje op `__utmz`. Nadat deze cookie is ingesteld (door [!DNL Google Analytics] traceren code), wordt de inhoud ervan verzonden met elke volgende aanvraag van die gebruiker naar uw domein. In PHP kun je bijvoorbeeld de inhoud van `$_COOKIE['__utmz']` en je zou een string zien die er ongeveer zo uitziet:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Het is duidelijk dat er bepaalde brongegevens voor acquisities in de tekenreeks zijn gecodeerd. Dit wordt getest om te bevestigen dat dit de recentste aanschafbron van de bezoeker en bijbehorende campagnegegevens is. Nu moet u weten hoe u de gegevens kunt extraheren. Gelukkig heeft Justin Cutroni eerder beschreven hoe deze codering werkt en heeft ze JavaScript-code gedeeld om de belangrijkste gegevensfragmenten te extraheren.

Deze code is omgezet in een [PHP-bibliotheek gehost op github](https://github.com/RJMetrics/referral-grabber-php). Als u de bibliotheek wilt gebruiken, `include` een verwijzing naar `ReferralGrabber.php` en vervolgens bellen

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

De geretourneerde `$data` array is een kaart van de keys `source`, `medium`, `term`, `content`, `campaign`, `gclid`en hun respectieve waarden.

Adobe raadt u aan een tabel met de naam toe te voegen aan uw database, bijvoorbeeld `user_referral`, met de volgende kolommen: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Wanneer een gebruiker zich aanmeldt, haalt u de verwijzingsinformatie op en slaat u deze op in deze tabel.

#### Hoe deze gegevens te gebruiken

Hoe kunt u de aanschafbron van de gebruiker nu opslaan?

Stel dat u een SQL-database gebruikt en een `users` tabel met de volgende structuur:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | biologisch |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | direct | - |
| 4 | jess@ghi.com | 2012-01-26 | verwijzing | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | overige | biologisch |
| ... | ... | ... | ... | ... |

Om te beginnen, kunt u het aantal gebruikers tellen die uit elk verwijzingskanaal door de volgende vraag tegen uw gegevensbestand in werking te stellen komen:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Het resultaat ziet er ongeveer als volgt uit:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direct | 156 |
| verwijzing | 55 |
| overige | 16 |

Dat is interessant, maar weinig nuttig. Wat u echt wilt weten is:

* het groeipercentage van deze getallen in de loop der tijd
* het bedrag van de inkomsten die door elke verwervingsbron worden gegenereerd
* a [cohortanalyse](https://en.wikipedia.org/wiki/Cohort_analysis) van gebruikers die uit elke bron afkomstig zijn
* de waarschijnlijkheid dat een gebruiker van één van deze kanalen in de toekomst als klant zal terugkeren.

De query&#39;s die nodig zijn om deze analyses uit te voeren zijn complex. Op basis van deze informatie kunt u de meest winstgevende aanschafkanalen bepalen en de marketingtijd en het geld daarop afstemmen.

### Verwante

* **[Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)**
* **[Verbind uw [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[ROI verhogen in uw reclamecampagnes](../analysis/roi-ad-camp.md)**
* **[Hoe werkt [!DNL Google Analytics] UTM-toewijzingswerk?](../analysis/utm-attributes.md)**
