---
title: Repliceren van Google Analytics-kanalen met behulp van acquisitiebronnen
description: Leer hoe u Google Analytics-kanalen kunt repliceren met behulp van aankoopbronnen.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: cb7dd221f3e83be0c7ee01a6af479e5d1bad108c
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# [!DNL Google Analytics] Aankoopbronnen gebruiken

## Wat zijn kanalen? {#channels}

Het creëren van douanesegmenten om te zien hoe het verschillende verkeer presteert en trends waarneemt is één van de krachtigste toepassingen voor [!DNL Google Analytics]. Een klasse segmenten die standaard in [!DNL Google Analytics] bestaan, is `Channels` . Kanalen zijn een groepering van algemene manieren waarop mensen naar uw site komen.  [!DNL Google Analytics] sorteert automatisch de vele manieren die u een gebruiker aanschaft - of het sociale media, betaal-per-klik, e-mail, of verwijzingsverbindingen zijn - en bundelt hen in een emmer, of Kanaal.

## Waarom zie ik mijn `channels` niet in Commerce Intelligence? {#nochannels}

`Channels` zijn eenvoudige, geaggregeerde emmers van gegevens. Om uw verwervingen in de emmers van het Kanaal te sorteren, [!DNL Google] plaatst verschillende regels en definities gebruikend specifieke parameters: een combinatie van verwerving [ Source ](https://support.google.com/analytics/answer/1033173?hl=en) (de oorsprong van uw verkeer) en verwerving [ Medium ](https://support.google.com/analytics/answer/6099206?hl=en) (de algemene categorie van de bron).

Terwijl het hebben van deze emmers u kan helpen om te begrijpen waar uw verkeer uit komt, worden deze gegevens niet geëtiketteerd door kanaal maar door een combinatie van Source en Medium. Omdat [!DNL Google] kanaalinformatie als twee afzonderlijke gegevenspunten verzendt, worden kanaalgroepen niet automatisch weergegeven in [!DNL Commerce Intelligence] .

## Wat zijn de standaardkanaalgroepen? Hoe worden ze gemaakt?

[!DNL Google] stelt standaard acht verschillende kanalen in. De regels die bepalen hoe kanalen worden gecreeerd zijn hieronder.

| **Kanaal** | **wat is het?** | **hoe wordt het gecreeerd?** |
|---|---|---|
| Direct | Iedereen die rechtstreeks op uw site komt. | Source = `Direct`<br> AND Medium = `(not set); OR Medium = (none)` |
| Organic Search | Verkeer dat in onbetaalde zoekmachines op een organische positie is geplaatst. | Medium = `organic` |
| Verwijzing | Verkeer dat afkomstig is van een externe koppeling die geen Organic Search is of van websites die geen sociale netwerken zijn. | Medium = `referral` |
| Betaalde zoekopdracht | Verkeer dat een UTM-trackingcode heeft waarvan het medium &quot;cpc&quot;, &quot;ppc&quot; of &quot;paidsearch&quot; is EN een advertentienetwerk is dat niet overeenkomt met &quot;Content&quot;. | Medium = `^(cpc|ppc|paidsearch)$`<br> AND Ad Distribution Network ≠ `Content` |
| Sociaal | Het verkeer van de verwijzing dat uit om het even welk ongeveer [ 400 sociale netwerken ](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) komt en niet geëtiketteerd als advertenties. | Sociale Source-verwijzing = `Yes`<br> OR Medium = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Verkeer van sessies die zijn gelabeld met een medium &quot;email&quot;. | UTM-trackingcode van Medium = `email` |
| Weergave | Verkeer dat een UTM-trackingcode heeft waarvan het medium ofwel weergave of cpm is. Omvat ook interactie AdWords waar het advertentienetwerk &quot;Inhoud&quot;aanpast | Medium = `^(display|cpm|banner)$`<br> OR Ad Distribution Network = `Content`<br> AND Ad Format ≠ `Text` |
| Overige | Sessies van andere reclamekanalen (met uitzondering van Betaalde zoekopdracht) die zijn gelabeld met een medium van &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot; en &quot;filiaal&quot;. | Medium = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Hoe kan ik deze kanaalgroepen opnieuw maken in mijn Data Warehouse? {#recreate}

Nu u weet dat kanalen slechts combinaties van bronnen en media zijn, is het een eenvoudig proces in drie stappen om deze groepen opnieuw te maken in uw Data Warehouse.

1. **laat uw [!DNL Google ECommerce] integratie** toe

   [ wanneer toegelaten ](../importing-data/integrations/google-ecommerce.md), zorg ervoor aan [ synchronisatie ](tour-dwm.md#syncing) het **middel** en **bron** gebieden in uw Data Warehouse. Nadat deze bewerking is voltooid, worden gegevens over aankopen via medium en bron naar uw Data Warehouse overgebracht.

1. **upload een afbeelding van het kanaalgroeperingen van Google**

   Adobe Commerce leidt tot een lijst met de standaardgroepen die als dossier in kaart worden gebracht dat u [ kunt downloaden ](../../assets/ga-channel-mapping.csv).

   Als u een [!DNL Google Analytics] pro bent en uw eigen kanalen hebt gemaakt, wilt u uw specifieke regels toevoegen aan de toewijzingstabel voordat u het bestand uploadt naar [!DNL Commerce Intelligence] .

   Breng het in uw Data Warehouse als a [ Dossier uploaden ](../importing-data/connecting-data/using-file-uploader.md).

   ![ interface die van de Manager van Data Warehouse primaire zeer belangrijke montages ](../../assets/Setting_Primary_Keys.png) toont

1. **Vestig een verband tussen [!DNL Google ECommerce] en het Uploaden van het Dossier van Toewijzingen**

   Om een verband tussen [!DNL Google ECommerce] en de mappinglijst te vestigen, [ voorlegt een steunverzoek ](../../guide-overview.md#Submitting-a-Support-Ticket) aan uw team van de Analyst van Gegevens en van verwijzingen dit onderwerp. De analist leidt tot een nieuwe berekende kolom genoemd **Kanaal** in de lijst van de Handel EC. **na een volledige updatecyclus**, zal deze kolom klaar zijn om in a `Filter` of `Group by` te gebruiken.

U hebt nu [!DNL Google Analytics Channel] groepen in uw Data Warehouse, wat betekent dat u uw gegevens vanuit een nieuw perspectief kunt analyseren:

![ die het Aantal van Orden segmenteren metrisch door Kanaal ](../../assets/GA_Channel_Gif.gif)

In dit voorbeeld, begon u eenvoudig met het segmenteren van het **Aantal Orden** metrisch door **Kanaal**. Test uw nieuwe kolom en bekijk welke trends u kunt identificeren in uw [!DNL Google Analytics Channel] gegevens!

## Gerelateerde documentatie

* [De Report Builder gebruiken](../../tutorials/using-visual-report-builder.md)
* [Verwachte [!DNL Google ECommerce] gegevens](../importing-data/integrations/google-ecommerce-data.md)
* [De bouw [!DNL Google ECommerce] dimensies met orde en klantengegevens](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Wat zijn uw waardevolste aanschafbronnen en kanalen?](../analysis/most-value-source-channel.md)
