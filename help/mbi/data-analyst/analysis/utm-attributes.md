---
title: Google Analytics- en UTM-kenmerk
description: Meer informatie over het toewijzingsproces van de bron Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] en UTM-kenmerk

Het is van essentieel belang om [verwervingsbron voor gebruiker bijhouden](../../data-analyst/analysis/google-track-user-acq.md) tot [de best presterende reclamecampagnes te identificeren](../../data-analyst/analysis/most-value-source-channel.md). In dit onderwerp wordt de [!DNL Google Analytics] brontoewijzingsproces. Met andere woorden, welk deel van de informatie wordt geregistreerd wanneer.

## Wat is attributie?

`Attribution` gaat over het opgeven van een verwijzingsbron van een bepaalde activiteit. Deze activiteiten zijn meestal macroconversies of microconversies, macro zijn dingen als **aankopen**, micro-objecten zoals **registratie, e-mailaanmelding, blogcommentaar,** enzovoort.

In het ideale geval wordt telkens wanneer een conversiegebeurtenis plaatsvindt, een verwijzingsbron vastgelegd. Maar hoe wordt de bron bepaald?

De realiteit is dat gebruikers vaak uit vele bronnen komen voordat ze een micro- of macroconversie bereiken of doorvoeren. Ze kunnen bijvoorbeeld naar de locatie komen via biologisch, dan vertrekken, dan via betaald zoeken, dan vertrekken en rechtstreeks naar de site zelf komen. Deze brontraceringsinformatie wordt vaak via UTM-parameters aan de site verstrekt, maar er zijn ook meer geavanceerde systemen. Voor uw doeleinden richt u zich op [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Hoe werkt [!DNL Google Analytics] verwijzingsbronnen via UTM-parameters attribuut?

Wanneer de UTM-parameters op de URL worden opgegeven, worden deze geparseerd en in een [!DNL Google Analytics] [koekje](https://en.wikipedia.org/wiki/HTTP_cookie). Als een website geen [!DNL Google Analytics]Het heeft geen zin om UTM&#39;s te hebben. [!DNL Google Analytics] heeft regels voor hoe het met een gebruiker behandelt die veelvoudige URLs met UTMs tijdens hun leven (meer op dat later) raakt. Ervan uitgaande dat de website is geconfigureerd om UTM-parameters vast te leggen in een externe database wanneer een micro- of macroconversie plaatsvindt, wat zich ook in de [!DNL Google Analytics] cookie op het moment van omzetting wordt gerepliceerd naar de database.

## Eerste klik versus laatste klik

### Toekenning laatste klik

De laatste klikattributie is het gemeenschappelijkste attributiemodel dat door wordt gebruikt [!DNL Google Analytics]. In dit geval worden de [!DNL Google Analytics] cookie vertegenwoordigt de UTM-parameters voor de meest recente bron vóór de conversiegebeurtenis. Dit is [opgenomen in de database](../../data-analyst/analysis/google-track-user-acq.md). De [!DNL Google Analytics] cookie overschrijft alleen de vorige UTM-parameters als de gebruiker op een nieuwe URL klikt die een nieuwe set UTM-parameters bevat.

Neem bijvoorbeeld een gebruiker die eerst een website bezoekt via [!DNL Google Analytics] *betaalde zoekopdracht*, dan keert terug via *organische zoekopdracht*, en komt eindelijk terug op de *rechtstreeks* of via een *e-mailkoppeling* **zonder UTM-parameters** vóór de conversiegebeurtenis. In dit voorbeeld wordt [!DNL Google Analytics] cookie zegt dat de bron van de gebruiker biologisch is , aangezien dit de laatste bron vóór de conversie is . De *pad* van de gebruiker voordat die laatste conversiegebeurtenis wordt genegeerd. Als de gebruiker in plaats daarvan via een e-mailkoppeling met UTM de website heeft bezocht, [!DNL Google Analytics] cookie zou zeggen dat de bron &quot;email&quot; is. Als het cookie bestaande UTM-parameters bevat en de gebruiker via direct de cookie in de cookie komt, wordt de [!DNL Google Analytics] cookie toont de UTM-parameters in plaats van &quot;direct&quot;.

>[!NOTE]
>
>Een specifieke gebruiker [!DNL Google Analytics] cookieparameters worden gewist wanneer het cookie [verloopt](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)of wanneer een gebruiker de cookies in de browser wist.*

### Kenmerk eerste klik

Met sommige gereedschappen voor betaalde toewijzingen kunt u de &quot;pancake-stapel&quot; van bronnen vastleggen in het pad van een gebruiker. In die situatie, in het bovenstaande voorbeeld, zou eerst klikken attributie ons betaalde onderzoek vertellen. Alternatief, voeren sommige websites hun eigen koekjes uit die een pancake stapel vangen en de eerste bron in hun gegevensbestand opslaan.

## Hoe kan ik attributie analyseren?

[!DNL Google Analytics] heeft een aantal robuuste functies in de webinterface waarmee u vier verschillende attribuutmodellen kunt uitvoeren:

1. eerste klik
1. laatste klik
1. lineair (verdeel de opbrengst gelijkelijk over alle bronnen in de weg)
1. gewogen (aangepaste attributie)

Nu je begrijpt wat het toewijzingsmodel is voor elke micro- of macro-conversie, wordt de vraag: &quot;Wat doe je met alle conversies van een gebruiker?&quot;.  Bekijk bijvoorbeeld de UTM&#39;s die zijn opgenomen op basis van de logica van de GA voor laatste klik:

* Gebruikersregisters volgens biologische
* Eerste aankoop van gebruiker onder betaalde zoekopdracht $5.00
* Tweede aankoop van gebruiker onder e-mail $50.00
* Derde aankoop van gebruiker onder biologische $10.00

Hier vraag je: &quot;Hoeveel inkomsten heb ik van betaalde zoekopdrachten? Uit e-mail?  Uit biologisch?&quot;. U zou kunnen zeggen dat de antwoorden 5, 50, en 10 (wat de laatste bron ook was) zijn, of u zou ook kunnen zeggen dat u alle opbrengst aan de eerste bron (alle 65 gaat naar organisch) zou kunnen toeschrijven. U kunt ook een gewogen analyse toepassen of het lineaire model toepassen (dat wil zeggen ongeveer 22 per model).

## Gerelateerde documentatie

* [Referentiebron voor bestelling volgen via [!DNL Google Analytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)
* [Verbind uw [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [ROI verhogen in uw reclamecampagnes](../analysis/roi-ad-camp.md)
* [Vijf aanbevolen procedures voor UTM-tags in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
