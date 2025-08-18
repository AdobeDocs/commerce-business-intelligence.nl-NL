---
title: Google Analytics- en UTM-kenmerk
description: Meer informatie over het Google Analytics-brontoewijzingsproces.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Google Analytics] en UTM-kenmerk

Het is kritiek aan [ bron van de spoorgebruikersaanwinst ](../../data-analyst/analysis/google-track-user-acq.md) om [ de best presterende reclamecampagnes ](../../data-analyst/analysis/most-value-source-channel.md) te identificeren. In dit onderwerp wordt het [!DNL Google Analytics] brontoewijzingsproces besproken. Met andere woorden, welk deel van de informatie wordt geregistreerd wanneer.

## Wat is attributie?

`Attribution` gaat over het opgeven van een verwijzingsbron van een bepaalde activiteit. Die activiteiten zijn typisch macro-omzettingen of micro-omzettingen, macro die dingen zoals **aankopen** zijn, micro die dingen zoals **registratie, e-mailaanmelding, blogcommentaar,** etc. zijn.

In het ideale geval wordt telkens wanneer een conversiegebeurtenis plaatsvindt, een verwijzingsbron vastgelegd. Maar hoe wordt de bron bepaald?

De realiteit is dat gebruikers vaak uit vele bronnen komen voordat ze een micro- of macroconversie bereiken of doorvoeren. Ze kunnen bijvoorbeeld naar de locatie komen via biologisch, dan vertrekken, dan via betaald zoeken, dan vertrekken en rechtstreeks naar de site zelf komen. Deze brontraceringsinformatie wordt vaak via UTM-parameters aan de site verstrekt, maar er zijn ook meer geavanceerde systemen. Voor uw doeleinden, concentreer zich op [ UTM ](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## Hoe kenmerkt [!DNL Google Analytics] verwijzingsbronnen via parameters UTM?

Wanneer de parameters UTM op URL worden gespecificeerd, worden deze ontleed en geplaatst in a [!DNL Google Analytics] [ koekje ](https://en.wikipedia.org/wiki/HTTP_cookie). Als een website [!DNL Google Analytics] niet heeft, heeft het geen zin om UTM&#39;s te hebben. [!DNL Google Analytics] heeft regels voor hoe het met een gebruiker behandelt die veelvoudige URLs met UTMs tijdens hun leven (meer op dat later) raakt. Ervan uitgaande dat de website is geconfigureerd om UTM-parameters vast te leggen in een externe database wanneer een micro- of macroconversie plaatsvindt, wordt alles wat zich op het moment van de conversie in het [!DNL Google Analytics] -cookie bevindt, gerepliceerd naar de database.

## Eerste klik versus laatste klik

### Toekenning laatste klik

De kenmerk Laatste klik is het meestgebruikte attributiemodel van [!DNL Google Analytics]. In dit geval, vertegenwoordigt het [!DNL Google Analytics] koekje de parameters UTM voor de meest recente bron vóór de omzettingsgebeurtenis, en dit wordt [ geregistreerd in het gegevensbestand ](../../data-analyst/analysis/google-track-user-acq.md). Het cookie [!DNL Google Analytics] overschrijft alleen de vorige UTM-parameters als de gebruiker op een nieuwe URL klikt die een nieuwe set UTM-parameters bevat.

Bijvoorbeeld, overweeg een gebruiker die eerst een website via [!DNL Google Analytics] *betaalde onderzoek* bezoekt, dan terugkeert via *biologisch onderzoek*, en komt tenslotte terug naar de *website direct* of via een *e-mailverbinding* **zonder parameters UTM** vóór de omzettingsgebeurtenis. In dit voorbeeld wordt in het cookie van [!DNL Google Analytics] gezegd dat de bron van de gebruiker biologisch is, aangezien dit de laatste bron vóór de conversie vertegenwoordigt. De *weg* van de gebruiker alvorens die definitieve omzettingsgebeurtenis wordt genegeerd. Als de gebruiker de website bezocht via een e-mailkoppeling met UTM, zou de cookie van [!DNL Google Analytics] zeggen dat de bron &quot;email&quot; is. Als het cookie bestaande UTM-parameters bevat en de gebruiker rechtstreeks in het cookie komt, worden in het cookie van [!DNL Google Analytics] de UTM-parameters weergegeven in plaats van &quot;direct&quot;.

>[!NOTE]
>
>De specifieke gebruikers [!DNL Google Analytics] koekjesparameters worden van een specifieke gebruiker gewist wanneer het koekje [&#128279;](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage) verloopt, of wanneer een gebruiker hun koekjes in browser ontruimt.*

### Kenmerk eerste klik

Met sommige gereedschappen voor betaalde toewijzingen kunt u de &quot;pancake-stapel&quot; van bronnen vastleggen in het pad van een gebruiker. In die situatie, in het bovenstaande voorbeeld, zou eerst klikken attributie ons betaalde onderzoek vertellen. Alternatief, voeren sommige websites hun eigen koekjes uit die een pancake stapel vangen en de eerste bron in hun gegevensbestand opslaan.

## Hoe kan ik attributie analyseren?

[!DNL Google Analytics] bevat een aantal robuuste functies in de webinterface waarmee u vier verschillende attributiemodellen kunt uitvoeren:

1. eerste klik
1. laatste klik
1. lineair (verdeel de opbrengst gelijkelijk over alle bronnen in de weg)
1. gewogen (aangepaste attributie)

Nu je begrijpt wat het toewijzingsmodel is voor elke micro- of macro-conversie, wordt de vraag: &quot;Wat doe je met alle conversies van een gebruiker?&quot;.  Bekijk bijvoorbeeld de UTM&#39;s die zijn opgenomen op basis van de logica van de GA laatste klik:

* Gebruikersregisters volgens organisch
* Eerste aankoop van gebruiker onder betaalde zoekopdracht $5.00
* Tweede aankoop van gebruiker onder e-mail $50.00
* Derde aankoop van gebruiker onder biologische $10.00

Hier vraag je: &quot;Hoeveel inkomsten heb ik van betaalde zoekopdrachten? Uit e-mail?  Uit biologisch?&quot;. U zou kunnen zeggen dat de antwoorden 5, 50, en 10 (wat de laatste bron ook was) zijn, of u zou ook kunnen zeggen dat u alle opbrengst aan de eerste bron (alle 65 gaat naar organisch) zou kunnen toeschrijven. U kunt ook een gewogen analyse toepassen of het lineaire model toepassen (dat wil zeggen ongeveer 22 per model).

## Gerelateerde documentatie

* [De verwijzingsbron van de orde van het spoor via  [!DNL Google Analytics]  E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)
* [Verbind uw  [!DNL Google Adwords]  rekening](../importing-data/integrations/google-adwords.md)
* [ROI verhogen in uw reclamecampagnes](../analysis/roi-ad-camp.md)
* [Vijf beste praktijken voor het etiketteren UTM in  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
