---
title: Repliceren van Google Analytics-kanalen met behulp van aankoopbronnen
description: Leer hoe je Google Analytics-kanalen repliceert met behulp van acquisitiebronnen.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] het gebruiken van de Bronnen van de Aankoop

## Wat zijn kanalen? {#channels}

Het creëren van douanesegmenten om te zien hoe het verschillende verkeer presteert en trends waarneemt is één van de krachtigste toepassingen voor [!DNL Google Analytics]. Eén klasse van segmenten die standaard in [!DNL Google Analytics] zijn `Channels`. Kanalen zijn een groepering van algemene manieren waarop mensen naar uw site komen.  [!DNL Google Analytics] sorteert automatisch de vele manieren dat u een gebruiker - of het sociale media, betaal-per-klik, e-mail, of verwijzingsverbindingen zijn - en bundelt hen in een emmer, of Kanaal.

## Waarom zie ik mijn `channels` in Commerce Intelligence? {#nochannels}

`Channels` zijn eenvoudige, geaggregeerde emmers van gegevens. Om uw verwervingen in de emmers van het Kanaal te sorteren, [!DNL Google] stelt verschillende regels en definities in met behulp van specifieke parameters: een combinatie van verwervingen [Bron](https://support.google.com/analytics/answer/1033173?hl=en) (de oorsprong van uw verkeer) en aankoop [Normaal](https://support.google.com/analytics/answer/6099206?hl=en) (de algemene categorie van de bron).

Terwijl het hebben van deze emmers u kan helpen om te begrijpen waar uw verkeer uit komt, worden deze gegevens niet geëtiketteerd door kanaal maar door een combinatie Bron en Normaal. Omdat [!DNL Google] verzendt kanaalinformatie als twee afzonderlijke gegevenspunten, de kanaalgroepen verschijnen niet automatisch binnen [!DNL Commerce Intelligence].

## Wat zijn de standaardkanaalgroepen? Hoe worden ze gemaakt?

Standaard, [!DNL Google] stelt acht verschillende kanalen in. Hieronder vindt u de regels die bepalen hoe kanalen worden gemaakt.

| **Kanaal** | **Wat is het?** | **Hoe wordt het gemaakt?** |
|---|---|---|
| Direct | Iedereen die rechtstreeks op uw site komt. | Bron = `Direct`<br>AND Medium = `(not set); OR Medium = (none)` |
| Organic Search | Verkeer dat in onbetaalde zoekmachines op organische wijze is gerangschikt. | Normaal = `organic` |
| Verwijzing | Verkeer dat afkomstig is van een externe koppeling die geen Organic Search is of van websites die geen sociale netwerken zijn. | Normaal = `referral` |
| Betaalde zoekopdracht | Verkeer dat een UTM-trackingcode heeft waarvan het medium &quot;cpc&quot;, &quot;ppc&quot; of &quot;paidsearch&quot; is EN een advertentienetwerk is dat niet overeenkomt met &quot;Content&quot;. | Normaal = `^(cpc|ppc|paidsearch)$`<br>AND ADD Distribution Network ≠ `Content` |
| Sociaal | Verwijzingsverkeer dat uit om het even welk van ongeveer komt [400 sociale netwerken](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) en zijn niet gecodeerd als advertenties. | Verwijzing naar sociale bron = `Yes`<br>OR Normaal = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Verkeer van sessies die zijn gelabeld met een medium &quot;email&quot;. | UTM-trackingcode van medium = `email` |
| Weergave | Verkeer dat een UTM-trackingcode heeft waarbij het medium weergave of cpm is. Bevat ook AdWords-interactie, waarbij het advertentiedistributienetwerk overeenkomt met &quot;Content&quot; | Normaal = `^(display|cpm|banner)$`<br>OR Ad Distribution Network = `Content`<br>AND Ad Format ≠ `Text` |
| Overige | Sessies van andere reclamekanalen (met uitzondering van paid Search) die zijn gelabeld met een medium van &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot; en &quot;gelieerde&quot;. | Normaal = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Hoe kan ik deze kanaalgroeperingen in mijn Data Warehouse opnieuw maken? {#recreate}

Nu u weet dat kanalen slechts combinaties van bronnen en media zijn, is het een gemakkelijk proces in drie stappen om deze groeperingen in uw Data Warehouse opnieuw te maken.

1. **Schakel uw[!DNL Google ECommerce]integratie**

   [Indien ingeschakeld](../importing-data/integrations/google-ecommerce.md), zorg ervoor dat u [synchroniseren](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#sync) de **medium** en **source** in uw Data Warehouse. Nadat dit is voltooid, zullen de gegevens van de middelmatige en bronverwerving in uw Data Warehouse worden gebracht.

1. **Een toewijzing van Google-kanaalgroepen uploaden**

   Adobe Commerce maakt een tabel met de standaardgroepen die zijn toegewezen als een bestand dat u kunt [downloaden](../../assets/ga-channel-mapping.csv).

   Als u een [!DNL Google Analytics] pro en creeerde uw eigen kanalen, wilt u uw specifieke regels aan de toewijzingstabel toevoegen alvorens het dossier in te uploaden [!DNL Commerce Intelligence].

   Breng het als een [Bestand uploaden](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Een relatie tot stand brengen tussen[!DNL Google ECommerce]en Toewijzingen Bestand uploaden**

   Om een relatie tot stand te brengen tussen[!DNL Google ECommerce] en de toewijzingstabel, [een steunaanvraag indienen](../../guide-overview.md#Submitting-a-Support-Ticket) aan uw team van de Analyst van Gegevens en verwijzing dit onderwerp. De analist maakt een nieuwe berekende kolom met de naam **Kanaal** in de tabel ECommerce. **Na een volledige updatecyclus**, kan deze kolom worden gebruikt in een `Filter` of `Group by`.

U hebt nu [!DNL Google Analytics Channel] groeperingen in uw Data Warehouse, wat betekent dat u uw gegevens vanuit een nieuw perspectief kunt analyseren:

![Het segmenteren van het Aantal orden metrisch door Kanaal](../../assets/GA_Channel_Gif.gif)

In dit voorbeeld bent u eenvoudig begonnen met het segmenteren van de **Aantal bestellingen** metrisch op **Kanaal**. Test uw nieuwe kolom en bekijk welke trends u kunt identificeren in uw [!DNL Google Analytics Channel] data!

## Gerelateerde documentatie

* [De Report Builder gebruiken](../../tutorials/using-visual-report-builder.md)
* [Verwacht[!DNL Google ECommerce]data](../importing-data/integrations/google-ecommerce-data.md)
* [Gebouw[!DNL Google ECommerce]afmetingen met bestelling en klantgegevens](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Wat zijn uw waardevolste aanschafbronnen en kanalen?](../analysis/most-value-source-channel.md)
