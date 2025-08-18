---
title: Het effect van de coupon analyseren
description: Leer hoe u de invloed van coupons op het aanschaffen en behouden van klanten analyseert.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Coupon-effect

Analyseren hoe klanten uw coupons gebruiken, kan uw bedrijf aanzienlijke insight bieden. Specifiek analyseren hoe u klanten aanschaft en behoudt via coupons. Dit onderwerp verkent analyses die u kunnen helpen de volgende soorten vragen beantwoorden:

* Hoeveel klanten verwerft u via coupons?
* Hebben klanten met een coupon meer kans om herhaaldelijk aankopen te doen dan klanten die niet via coupons zijn gekocht?
* Hoe verschillen de gemiddelde levensduuropbrengsten tussen klanten die coupon hebben gekregen en klanten die niet via coupons zijn aangekocht?
* Doen klanten die zijn aangeschaft met coupons, herhaaldelijk aankopen met coupons?

Beantwoord deze vragen door zich op [ te concentreren het vergelijken van coupon-verworven klanten aan niet-coupon verworven klanten ](#compare), [ het analyseren van eerste ordedetails van couponverwervingen ](#firstorder), en [ het bekijken van de attributen van klanten die coupons in hun eerste orde gebruiken.](#attributes)

Aan de slag!

## Klanten met coupon vergelijken met klanten zonder coupon {#compare}

Wanneer u analyses maakt die de verwerving en retentie van coupons onderzoeken, kunt u de volgende maatstaven gebruiken:

### Aantal nieuwe klanten

Deze maatstaf toont u het aantal klanten met coupon en klanten zonder coupon die in de loop der tijd zijn aangeschaft. Dit kan u helpen de verhouding van klantenverwervingen via coupons bepalen.

### Gemiddelde inkomsten tijdens de levensduur

Deze maatstaf toont u de gemiddelde levensopbrengst van coupon en niet-coupon verworven klanten. Dit kan helpen bepalen als de levenwaarde van een klant afhankelijk van hun verwervingstype varieert.

### Aantal herhalingsorders

Deze metrisch toont u het aantal herhalingsorden die door beide types van klantenverwervingen worden gemaakt. Dit kan helpen bepalen als meer follow-uporders worden geplaatst door verkregen klanten met of zonder coupon.

### Aantal en percentage herhaalde opdrachten met coupon

Dit toont het aantal herhaalde opdrachten met een coupon en het percentage herhaalde opdrachten met een coupon. Dit kan u helpen bepalen of klanten die coupon hebben verkregen, meer herhaalde opdrachten met een coupon willen uitvoeren dan klanten die geen coupon hebben verkregen, en of klanten die coupon hebben verkregen, in hun vervolgorders onevenredig gebruik maken van coupons.

Bekijk een aantal voorbeeldgegevens voor de aanschaf van coupons versus niet-couponaanschaf:

| **de acquisitie van de Klant** | **Aantal nieuwe klanten** | **Gemiddelde levensinkomsten** | **Aantal herhalingsorden** | **Aantal herhalingsorden met coupon** | **% van herhaalde opdrachten met coupon** |
|-----|-----|-----|-----|-----|-----|
| Coupon | 1.206 | $ 356,91 | 2.570 | 1.248 | 48,56% |
| Geen coupon | 11.561 | $ 498,30 | 20.145 | 3.251 | 16,14% |

{style="table-layout:auto"}

Kijk eens wat je hiervan kunt wegnemen:

### Aantal nieuwe klanten

In het bovenstaande voorbeeld is het aantal overnames zonder coupon veel groter dan het aantal overnames met coupon. Er zijn echter nog steeds 1.206 klanten die via een coupon zijn aangekocht en die anders geen klanten zijn geworden.

### Gemiddelde inkomsten tijdens de levensduur

In dit voorbeeld hebben overnames zonder coupon een hogere gemiddelde levensinkomsten dan couponovernames. Dit houdt in dat overnames zonder coupon meer terugkerende aankopen doen en/of hogere aankopen doen.

### Aantal herhalingsorders

Het aantal herhaalde opdrachten voor niet-couponaankopen is veel hoger dan voor couponaankopen. Dit wordt verwacht omdat er veel meer klanten zijn die geen coupon hebben gekocht.

### Aantal herhaalde opdrachten met coupon

Evenzo is het aantal herhaalde opdrachten met een coupon hoger voor aankopen zonder coupon.

## Percentage herhalingsopdrachten met coupon

Klanten die geen coupon hebben verkregen, hebben een veel lager percentage van herhaalde opdrachten met een coupon dan klanten die een coupon hebben verkregen. Voor klanten met coupon geldt dus dat bijna de helft van herhaalde opdrachten een coupon heeft. In dit voorbeeld doen klanten die coupon hebben gekocht vaak herhaalde aankopen met coupons.

## Details van eerste bestelling van couponaankopen analyseren {#firstorder}

Deze sectie richt zich slechts op **eerste orden van couponverwervingen, die door coupon worden gesegmenteerd.** Gebruik deze meetgegevens in uw analyse:

### Aantal orders/klanten

Deze maatstaf toont u het aantal eerste opdrachten voor elke coupon, of het aantal klanten dat deze coupon in hun eerste bestelling heeft gebruikt. Dit kan helpen bepalen als een bepaalde coupon meer aankopen voor het eerst aanmoedigt dan andere coupons.

### Bruto-inkomsten

Deze maatstaf onthult de opbrengst die u van een bepaalde coupon verkrijgt die in de eerste orde van een klant werd gebruikt. Deze opbrengst is een berekening van de verkochte posten voordat eventuele kortingen worden toegepast.

### Kortingen op coupons

In deze maatstaf ziet u het totale kortingsbedrag dat op de coupons wordt toegepast.

### Netto-inkomsten

Deze maatstaf onthult de opbrengst die u van een bepaalde coupon verkrijgt die in de eerste orde van een klant werd gebruikt. Deze opbrengst is een berekening van de posten die worden verkocht nadat alle kortingen zijn toegepast. Het is van belang op te merken dat de netto-inkomsten zonder de coupons mogelijk niet hebben plaatsgevonden.

### Gemiddelde orderwaarde

Deze maatstaf toont de gemiddelde orderwaarde voor een bepaalde coupon.

### Gemiddeld aantal orders gedurende de looptijd

Deze maatstaf helpt de loyaliteit en het gemiddelde aantal orders te evalueren die door klanten worden geproduceerd die een bepaalde coupon gebruiken.

### Gemiddelde inkomsten tijdens de levensduur

Deze metrische hulp evalueert de loyaliteit en gemiddelde opbrengst die door klanten wordt geproduceerd die een bepaalde coupon gebruiken. Bij de beoordeling of klanten die coupons gebruiken, een hogere waarde hebben dan andere, moet u rekening houden met het aantal orders waarin elke coupon is gebruikt om ervoor te zorgen dat u een aanzienlijke steekproefgrootte hebt.

Kijk nu naar een voorbeeld met drie verschillende coupons die worden gebruikt voor de eerste bestelling van klanten:

| **Coupon** | **Eerste tijdorden (FTO)** | **Bruto opbrengst van FTO** | **Kortingen die op FTO** worden toegepast | **Netto opbrengst van FTO** | **Gemiddelde ordewaarde voor FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% van $100 of meer** | 56 | $ 8.531,04 | $ 2.132,76 | $ 6.398,28 | $ 152,34 |
| **$10 off** | 87 | $ 3.707,07 | $ 426,10 | $ 3.280,97 | $ 42,61 |
| **20% weg** | 145 | $ 10.975,05 | $ 2.195,01 | $ 8.780,04 | $ 75,69 |

{style="table-layout:auto"}

Wat kan hieruit worden afgeleid? Ten eerste had de coupon &quot;20% korting&quot; het meeste aantal eerste opdrachten. Het aantal aan elke coupon gekoppelde orders kan echter variëren op basis van verschillende factoren, zoals:

* het bedrag van de advertentie voor elke coupon.
* de duur van de periode waarvoor de coupons werden aangeboden.
* het tijdstip van de dag/week/maand/jaar waarop de coupons werden aangeboden.
* het seizoen waarin de coupons werden aangeboden , afhankelijk van de activiteit .

  **Voorbeeld:** de &quot;20% korting&quot;coupon werd aangeboden tijdens de zomermaanden, maar de zaken verkopen winterkleding.
* de beperkingen op de coupons.

  **Voorbeeld:** de &quot;10% korting&quot;coupon wordt slechts aangeboden aan klanten die een winterjas in de zelfde orde kopen.

De **bruto opbrengst** voor de &quot;25% van $100 of meer&quot;coupon is veel hoger dan de bruto opbrengst voor &quot;$10 van&quot;coupon. Nochtans, heeft &quot;$10 van&quot;coupon een veel groter **aantal orden**. Het analyseren van de **gemiddelde ordewaarde** verstrekt insight in deze verschillen. Hoewel de coupon &quot;25% korting op $100 of meer&quot; minder orders bevatte, is de gemiddelde orderwaarde meer dan driemaal die van de coupon &quot;$10 korting&quot;. Zo wordt een grotere bruto-opbrengst toegeschreven aan de coupon &quot;25% korting op $100 of meer&quot;.

De **kortingen** en **netto opbrengst** voor &quot;25% van $100 of meer&quot;en &quot;20% van&quot;coupons zijn dicht in waarde. Hoewel de gemiddelde orderwaarde voor &quot;25% korting op $100 of meer&quot; bijna tweemaal de gemiddelde orderwaarde voor &quot;20% korting&quot; is, heeft de laatste coupon iets minder dan driemaal het aantal orders.

## Attributen van klanten die coupons gebruiken in hun eerste bestelling {#attributes}

Nu u de bestellingen zelf hebt bekeken, bekijkt u de klanten die coupons gebruiken in hun eerste bestellingen:

| **de eerste orde van de Klant coupon** | **Aantal klanten** | **Gemiddeld levenslevensaantal orden** | **Gemiddelde levensinkomsten** |
|-----|-----|-----|-----|
| **25% van $100 of meer** | 56 | 2,8 | $ 554,54 |
| **$10 off** | 87 | 1,9 | $ 115,50 |
| **20% weg** | 145 | 1,3 | $ 103,75 |

{style="table-layout:auto"}

U ziet dat het aantal eerste opdrachten hetzelfde is als het aantal klanten voor elke coupon. Dit is logisch omdat elke klant slechts één eerste bestelling kan hebben.

Het grootste aantal klanten werd aangekocht via de coupon &quot;20% korting&quot;. Nochtans, hebben deze klanten het laagste **gemiddelde levenaantal orden** en **gemiddelde levenopbrengst**; over het algemeen, maken de meeste coupon-verworven klanten geen herhalingsorden. Voorts verwierven de klanten door &quot;25% van $100 of meer&quot;couponaandrijving hoger **gemiddeld levenaantal orden** en beurtelings, hogere **gemiddelde levenopbrengst**. Over het algemeen komen gebruikers die via deze coupon zijn aangeschaft, gewoonlijk terug en doen ze meer herhaalde aankopen.

## Omloop omhoog {#wrapup}

Er zijn veel analyses die u kunt maken om beter te begrijpen hoe uw klanten coupons gebruiken. Heb je ooit gedacht aan het analyseren van hoe je klanten je coupons gebruiken of de tijd die het kost om coupons te gebruiken? En hoe zit het met het vinden van het optimale kortingsbedrag - welk bedrag stimuleert herhaalde kopers, hogere gemiddelde orderwaarde en hogere levensduuropbrengsten? Voor hulp met deze soorten vragen, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
