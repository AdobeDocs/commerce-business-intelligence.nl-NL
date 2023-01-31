---
title: Google Analytics- en UTM-kenmerk
description: Meer informatie over het toewijzingsproces van de bron Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analytics- en UTM-kenmerk

Het is van essentieel belang om [verwervingsbron voor gebruiker bijhouden](../../data-analyst/analysis/google-track-user-acq.md) tot [de best presterende reclamecampagnes te identificeren](../../data-analyst/analysis/most-value-source-channel.md). In deze zelfstudie verkennen we het attributieproces van de bron van Google Analytics. Met andere woorden, welk deel van de informatie wordt geregistreerd wanneer.

## Wat is attributie?

`Attribution` gaat over het opgeven van een verwijzingsbron van een bepaalde activiteit. Deze activiteiten zijn meestal macroconversies of microconversies, macro zijn dingen als **aankopen**, micro-objecten zoals **registratie, e-mailaanmelding, blogcommentaar,** enzovoort.

In het ideale geval wordt telkens wanneer een conversiegebeurtenis plaatsvindt, een verwijzingsbron vastgelegd. Maar hoe wordt de bron bepaald?

De realiteit is dat gebruikers vaak uit vele bronnen komen voordat ze een micro- of macroconversie hebben ondergaan (ze kunnen bijvoorbeeld via organische kanalen naar de site komen, dan vertrekken, via betaalde zoekopdrachten, dan vertrekken en vervolgens rechtstreeks naar de site zelf komen). Deze brontraceringsinformatie wordt vaak via UTM-parameters aan de site verstrekt, maar er zijn ook meer geavanceerde systemen. Voor ons doel zullen we ons richten op [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Hoe werkt [!DNL Google Analytics] verwijzingsbronnen via UTM-parameters attribuut?

Wanneer de UTM-parameters op de URL worden opgegeven, worden deze geparseerd en in een [!DNL Google Analytics] [koekje](https://en.wikipedia.org/wiki/HTTP_cookie). Als een website geen [!DNL Google Analytics]Het heeft geen zin om UTM&#39;s te hebben. [!DNL Google Analytics] heeft regels voor hoe het met een gebruiker behandelt die veelvoudige URLs met UTMs tijdens hun leven (meer op dat later) raakt. Ervan uitgaande dat de website is geconfigureerd om UTM-parameters vast te leggen in een externe database, op elk moment dat een micro- of macroconversie plaatsvindt, wat zich ook in de [!DNL Google Analytics] cookie op het moment van omzetting wordt gerepliceerd naar de database.

## Eerste klik versus laatste klik

### Toekenning laatste klik

De laatste klikattributie is het gemeenschappelijkste attributiemodel dat door wordt gebruikt [!DNL Google Analytics]. In dit geval worden de [!DNL Google Analytics] cookie vertegenwoordigt de UTM-parameters voor de laatste of meest recente bron voorafgaand aan de conversiegebeurtenis. Dit is wat [opgenomen in de database](../../data-analyst/analysis/google-track-user-acq.md). De [!DNL Google Analytics] cookie overschrijft alleen de vorige UTM-parameters als de gebruiker op een nieuwe URL klikt die een nieuwe set UTM-parameters bevat.

Neem bijvoorbeeld een gebruiker die eerst een website bezoekt via [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *betaalde zoekopdracht*, dan keert terug via *organische zoekopdracht*, en komt eindelijk terug op de *rechtstreeks* of via een *e-mailkoppeling* **zonder UTM-parameters** vóór de conversiegebeurtenis. In dit voorbeeld wordt [!DNL Google Analytics] cookie zegt dat de bron van de gebruiker biologisch is , aangezien dit de laatste bron vóór de conversie is . De *pad* van de gebruiker vóór die laatste conversiegebeurtenis wordt genegeerd. Als de gebruiker in plaats daarvan via een e-mailkoppeling met UTM de website heeft bezocht, [!DNL Google Analytics] cookie zou zeggen dat de bron &quot;email&quot; is. Als het cookie bestaande UTM-parameters bevat en de gebruiker via direct de cookie in de cookie komt, wordt de [!DNL Google Analytics] cookie geeft altijd de UTM-parameters weer in plaats van &quot;direct&quot;.

>[!NOTE]
>
>Een specifieke gebruiker [!DNL Google Analytics] cookie parameters worden gewist wanneer de cookie [verloopt](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)of wanneer een gebruiker zijn of haar cookies in de browser wist.*)

### Kenmerk eerste klik

Met sommige gereedschappen voor betaalde toeschrijvingen kunt u de &quot;pancake-stapel&quot; van bronnen vastleggen in het pad van de gebruiker. In die situatie, in ons bovenstaande voorbeeld, zou de eerste klikattributie ons betaalde onderzoek vertellen. Alternatief, voert een minderheid van websites hun eigen koekjes uit die een pancake stapel vangen en de eerste bron in hun gegevensbestand opslaan.

## Hoe kan ik attributie analyseren?

[!DNL Google Analytics] heeft een aantal robuustere functionaliteit in hun webinterface waarmee u vier verschillende attribuutmodellen kunt uitvoeren: eerste klik, laatste klik, lineair (verdelen opbrengst gelijkelijk over alle bronnen in de weg), en gewogen (aangepaste attributie).

Nu je begrijpt wat het toewijzingsmodel is voor elke micro- of macroconversie, wordt de vraag wat je doet met alle conversies van een gebruiker.  Bekijk bijvoorbeeld de UTM&#39;s die zijn opgenomen op basis van de logica van de GA voor laatste klik:

* Gebruikersregisters volgens biologische
* Eerste aankoop van gebruiker onder betaalde zoekopdracht $5.00
* Tweede aankoop van gebruiker onder e-mail $50.00
* Derde aankoop van gebruiker onder biologische $10.00

Hier is waar u vraagt: Hoeveel inkomsten heb ik uit betaalde zoekopdrachten?  Uit e-mail?  Uit biologisch?  Je zou kunnen zeggen dat de antwoorden 5, 50 en 10 zijn (wat de laatste bron ook was), of je zou ook kunnen zeggen dat je alle inkomsten aan de eerste bron toewijst (dat wil zeggen, alle 65 gaan naar organisch). U kunt ook een gewogen analyse toepassen of het lineaire model toepassen (dat wil zeggen ongeveer 22 per model).

## Gerelateerde documentatie

* [Referentiebron voor bestelling volgen via [!DNL Google Analytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)
* [Verbind uw [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [ROI verhogen in uw reclamecampagnes](../analysis/roi-ad-camp.md)
* [5 beste praktijken voor het etiketteren van UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
