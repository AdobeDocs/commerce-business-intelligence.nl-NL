---
title: Het gebruik van coupons analyseren
description: Leer hoe u het gebruik van coupons kunt analyseren bij het aanschaffen en behouden van klanten.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Coupongebruik

Vraag je je ooit af hoe het aanbieden van coupons je je bedrijf beïnvloedt? Wilt u weten welke coupons de prestaties helpen of schaden? In dit artikel bekijken we analyses die u een goed beeld geven van het gebruik van de coupon van uw klanten door de volgende vragen te beantwoorden:

* Hoeveel klanten gebruiken coupons?
* Hoeveel coupons worden gebruikt?
* Wat zijn uw inkomsten voor en na het toepassen van coupons?
* Wat is de gemiddelde orderwaarde voor en na het toepassen van coupons?
* Welk soort klanten trekt u met coupons aan?

Laten we beginnen!

## Aanbevolen meetwaarden {#metrics}

Gebruik ([of gebouw](../../data-user/reports/ess-manage-data-metrics.md)) deze cijfers:

### Aantal orders

Deze maatstaf toont het aantal orders met en zonder coupons in de loop der tijd. Dit toont aan of en hoe vaak klanten uw coupons gebruiken, en hoe dit in tijd verandert.

### Bruto-inkomsten

Deze maatstaf toont de bruto-inkomsten die u verkrijgt uit orders die een bepaalde coupon bevatten. De bruto-inkomsten zijn een berekening van de volledige prijs van de verkochte posten, voordat eventuele kortingen worden toegepast. Dit kan helpen bepalen welke coupons met de hoogste en laagste bruto-inkomsten worden geassocieerd.

### Kortingen op coupons

Deze maatstaf kan u het totale kortingsbedrag tonen dat van de coupons wordt toegepast. Het is van belang op te merken dat deze orders mogelijk niet zonder de coupons hebben plaatsgevonden.

### Netto-inkomsten

Deze maatstaf toont de netto-inkomsten die u verkrijgt uit orders die een bepaalde coupon bevatten. De netto-inkomsten zijn een berekening van de prijs van de posten die worden verkocht nadat alle kortingen zijn toegepast. Dit kan helpen bepalen welke coupons aan de hoogste en laagste netto opbrengst worden geassocieerd.

### Percentage verdisconteerd

Dit toont het aandeel van de bruto-inkomsten dat door kortingen wordt gecompenseerd. Voor coupons met een percentagekorting is deze waarde al bekend (bijvoorbeeld 10% korting). Desondanks verschaft deze maatregel inzicht en een vergelijkingsmethode voor coupons die een korting op de vaste dollar zijn.

### Gemiddelde nettoorderwaarde

Deze maatstaf toont de gemiddelde orderwaarde wanneer een coupon wordt toegepast. U kunt analyseren of orders met coupons altijd een lagere orderwaarde hebben dan orders zonder coupons.

### Gemiddelde orderkorting

Dit geeft de gemiddelde dollarwaarde aan die wordt verdisconteerd bij elke order waarbij coupons worden toegepast. Dit geeft het verschil weer tussen de gemiddelde nettoorderwaarde en de gemiddelde brutoorderwaarde.

### Afzonderlijke kopers

Deze maatstaf geeft het aantal afzonderlijke kopers weer die een bepaalde coupon gebruiken.

### Gemiddelde inkomsten tijdens de levensduur

Deze metrische hulp evalueert de loyaliteit en gemiddelde opbrengst die door klanten wordt geproduceerd die een bepaalde coupon gebruiken. Wanneer u beoordeelt of klanten die coupons gebruiken, een hogere waarde hebben dan andere, moet u rekening houden met het aantal afzonderlijke kopers in elke categorie om ervoor te zorgen dat u een aanzienlijke steekproefgrootte hebt.

## Voorbeeld {#example}

Nu we weten naar welke maatstaven we moeten kijken, laten we een voorbeeld nemen met drie verschillende coupons: 10% korting, 20 dollar korting van 100 dollar of meer en 10 dollar korting.

| **Coupon** | **Aantal bestellingen** | **Bruto-inkomsten** | **Brutodisconto uit coupons** | **Netto-inkomsten** | **Percentage verdisconteerd** |
|-----|-----|-----|-----|-----|-----|
| **10% korting** | 79 | $ 19.757,02 | $ 1.975,70 | $ 17.781,32 | 10,00% |
| **$ 20 korting op $100+** | 101 | $ 13.928,91 | $ 2.020,00 | $ 11.908,91 | 14,50% |
| **$10 korting** | 201 | $ 14.542,35 | $ 2.010,00 | $ 12.532,35 | 13,82% |

{style=&quot;table-layout:auto&quot;}


| **Coupon** | **Gem. nettoorderwaarde** | **Gem. orderkorting** | **Afzonderlijke kopers** | **Gem. levenslange inkomsten** |
|-----|-----|-----|-----|-----|
| **10% korting** | $ 225,08 | $ 25,01 | 79 | $ 361,50 |
| **$ 20 korting op $100+** | $ 117,91 | $ 20,00 | 95 | $ 218,76 |
| **$10 korting** | $ 62,35 | $ 10,00 | 199 | $ 84,27 |

{style=&quot;table-layout:auto&quot;}

## Wat kunnen we hiervan weghalen?

Ongeveer 80 orders zijn geplaatst met de coupon &quot;10% korting&quot;, 100 opdrachten met de coupon &quot;$20 van $100 of meer&quot; en 200 opdrachten met de coupon &quot;$10 korting&quot;. De **aantal bestellingen** voor elke coupon kunnen verschillende factoren worden gebruikt, zoals:

* de duur van de periode waarvoor de coupons werden aangeboden.
* het tijdstip van de dag/week/maand/jaar waarop de coupons werden aangeboden.
* het seizoen waarin de coupons werden aangeboden , afhankelijk van de activiteit . Bijvoorbeeld:
* De coupon &quot;10% korting&quot; werd tijdens de zomermaanden aangeboden, maar de onderneming verkoopt winterkleding.

* de beperkingen op de coupons. Bijvoorbeeld:
* Het coupon &quot;$10 korting&quot; wordt alleen aan nieuwe klanten aangeboden.
* De coupon &quot;10% korting&quot; wordt alleen aangeboden aan klanten die in dezelfde volgorde een winterjas kopen.

* het gebruikelijke aankoopgedrag van de klant.

Terwijl de **brutokortingen** voor alle drie de coupons is het aantal orders voor elke coupon aanzienlijk verschillend ( ongeveer $2.000 ) . Het analyseren van kortingen op een per ordebasis helpt de redenen voor deze contrasterende aantallen verklaren. De coupon met de waarde &quot;10% korting&quot; heeft het minste aantal opdrachten, maar heeft een **gemiddelde orderkorting** van ongeveer $25. Hoewel deze coupon een laag aantal orders heeft, leidt haar hoge gemiddelde discontowaarde tot een brutodiscontobedrag van ongeveer $2.000.

**Bruto- en netto-inkomsten** Geef een algemeen overzicht van de totale waarde van de aan elke coupon gekoppelde orders. Dit totaalbeeld geeft echter geen inzicht in de verschillende gedragingen met betrekking tot elke coupon. Als u eenmaal per bestelling kijkt, ziet u dat de coupon &quot;10% korting&quot; erg hoog is **gemiddelde nettoorder** waarde, die op zijn beurt weer leidt tot de hoge **netto-inkomsten**.

Anderzijds heeft de coupon &quot;10% korting&quot; een zeer hoge gemiddelde discontowaarde ($25,01), maar de laagste **gedisconteerd percentage**. Dit is logisch als je rekening houdt met de gemiddelde nettoorderwaarde van $225,08. De coupon &quot;10% korting&quot; heeft een kleine procentuele korting op een grote gemiddelde nettoorderwaarde, dus de gemiddelde orderkorting is een groot bedrag.

Laten we eens kijken naar de **afzonderlijke kopers** en **gemiddelde levensduurinkomsten** voor elke coupon. De coupon &quot;10% korting&quot; heeft hetzelfde aantal orders als afzonderlijke kopers. Dit kan het gevolg zijn van het feit dat elke klant beperkt is tot één coupon. Anderzijds hebben de coupons &quot;$20 van $100 of meer&quot; en &quot;$10 korting&quot; minder duidelijke kopers dan het aantal orders, wat betekent dat sommige klanten deze coupons meerdere keren hebben gebruikt.

Voor gemiddelde levensinkomsten kunt u zien dat de gemiddelde levensinkomsten voor elke coupon groter zijn dan de respectieve **gemiddelde nettoorder** waarde. Dit houdt in dat ofwel klanten herhaalde aankopen hebben gedaan, en/of dat hun orderwaarde veel hoger was dan de gemiddelde nettoorderwaarde.

## Wat kan ik nog meer analyseren? {#otheranalyses}

De analyses die we in dit artikel hebben genoemd, kunnen u waardevolle inzichten geven in hoe uw klanten uw coupons gebruiken, maar er zijn vele andere analyses die u in staat stellen een beetje dieper te graven.

**U kunt de acquisities van uw klanten aan de hand van coupons analyseren.**

Welke coupons moedigen klanten aan om orders te plaatsen? Zijn deze coupons aantrekkelijk voor eenmalige kopers of stimuleren ze klantenloyaliteit (met andere woorden, klanten die herhaalde aankopen doen)?

**U kunt de tijd analyseren die het voor uw klanten duurt om uw coupons te gebruiken.**

Worden uw coupons gebruikt op de dag dat ze worden vrijgegeven of loopt een week of twee voorbij voordat de meerderheid van uw klanten deze gebruikt?

**U kon het optimale discontobedrag ontdekken dat klantenloyaliteit en algemene waarde verhoogt.**

Welk kortingsbedrag zal herhaalde kopers, hogere gemiddelde orderwaarde, en hogere levensinkomsten aanmoedigen?

Als u deze vragen beantwoordt, krijgt u inzicht in uw klanten, hun gedrag en de coupons die uw bedrijf de meeste waarde bieden.
