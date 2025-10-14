---
title: Google Analytics - Gebruikersapparaat en browsergegevens bijhouden in uw database
description: Leer hoeveel gebruikers zich daadwerkelijk aanmelden via mobiele apparaten en hoe dat de levensduurwaarde van deze gebruikers beïnvloedt.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] Tekstspatiëring

Met [!UICONTROL Google Analytics] kunt u [&#x200B; verwijzingsbroninformatie &#x200B;](../analysis/google-track-user-acq.md) bewaren om te begrijpen waar uw waardevolste gebruikers uit komen. Dit onderwerp bespreekt het platform (bijvoorbeeld, apparaat of browser) uw gebruikers werken aan. Met dit, zult u kunnen begrijpen hoeveel gebruikers eigenlijk het programma openen via mobiele apparaten en hoe dat de levenwaarde van die gebruikers beïnvloedt.

## Gebruikersapparaat en browsergegevens opslaan

Telkens wanneer een verzoek aan uw website wordt gedaan, verzendt browser van de gebruiker een user-Agent koord met informatie over het platform die het verzoek doet. Hier zijn sommige voorbeelden van het user-Agent koord:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Als u goed kijkt, ziet u dat de tekenreeks informatie bevat over het besturingssysteem, de browser en de naam van het apparaat dat de gebruiker gebruikt (als deze een naam heeft). Hoewel de gebruiker-agent koorden ver over platforms en zelfs versies van het zelfde platform variëren, is het over het algemeen waar dat de platformnaam ergens binnen zal bestaan. #1 hierboven is bijvoorbeeld een Mac met de Chrome-browser, #2 hierboven is een Windows-computer met de Firefox-browser, #3 is een iPhone, #4 is een iPad en #5 is een Android-apparaat.

Deze gegevens zijn voor elke server toegankelijk wanneer een aanvraag wordt ingediend. In PHP wordt de user-Agent string opgeslagen in `$_SERVER['HTTP_USER_AGENT']` . In Ruby op Rails wordt het opgeslagen in `request.env['HTTP_USER_AGENT']`. Andere talen en omgevingen bieden u op vergelijkbare wijze toegang tot deze taal.

### Wanneer moet u deze gegevens vastleggen?

[!DNL Adobe] raadt u aan een nieuw veld met de naam `Platform` of `User-Agent` toe te voegen aan uw databasetabellen `Customers` en `Orders` om deze gegevens op te slaan wanneer een gebruiker wordt gemaakt of een order wordt geplaatst. Als u een SQL-database gebruikt, moet dit veld een `VARCHAR(255)` zijn. 

>[!NOTE]
>
>De tekenreeks `User-Agent` mag veel langer zijn dan deze, maar in de praktijk overschrijdt deze lengte zelden.

### Hoe parseer ik de nuttige segmenten?

Er zijn een aantal bibliotheken beschikbaar waarmee u de tekenreeks `User-Agent` kunt parseren in componenten zoals het besturingssysteem, het apparaat enzovoort. Verwijs naar het [&#x200B; ua-parser project &#x200B;](https://github.com/tobie/ua-parser) om meer te leren.

Met deze nieuwe informatie kunt u beter begrijpen hoe gebruikers toegang krijgen tot uw site. Vervolgens kunt u hun ervaring op maat maken of marketingcampagnes voor bepaalde groepen maken.

## Verwante

* [De verwijzingsbron van de orde van het spoor via  [!DNL Google Anaytics]  E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)
* [Verbind uw  [!DNL Google Adwords]  rekening](../importing-data/integrations/google-adwords.md)
* [ROI verhogen in uw reclamecampagnes](../analysis/roi-ad-camp.md)
* [Hoe werkt  [!DNL Google Analytics]  UTM attributie?](../analysis/utm-attributes.md)
