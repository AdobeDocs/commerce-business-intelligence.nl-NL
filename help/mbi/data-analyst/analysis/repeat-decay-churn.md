---
title: Herhalingswaarschijnlijkheidsverlies en -kromme analyseren
description: Leer en begrijp hoe tijd verloopt tussen bestellingen en wanneer klanten naar verwachting zullen afkoelen.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Verval en kurn van waarschijnlijkheid herhalen

Als een deel van uw opbrengst uit herhaalde aankopen komt, bent u zich waarschijnlijk bewust van de enorme waarde van een loyale klantenbasis. Daarom is het van essentieel belang te begrijpen hoe tijd verstrijkt tussen bestellingen en wanneer van klanten wordt verwacht dat zij zullen afglijden.

Dit onderwerp verkent de analyses die u kunnen helpen de volgende vragen beantwoorden:

* Wat is de waarschijnlijkheid dat een klant een andere aankoop zal doen?
* Hoe varieert de waarschijnlijkheid van de herhaalde bestelling in de tijd sinds de laatste aankoop van de klant?
* Wanneer moet een klant als gekost worden beschouwd? En wanneer moet een reactiveringscampagne dan van start gaan?

## Aanbevolen meetwaarden

Bij het analyseren van recidiefwaarschijnlijkheidsverlies en -kromme kunt u het volgende gebruiken ([of gebouw](../../data-user/reports/ess-manage-data-metrics.md)) deze cijfers:

### Waarschijnlijk eerste herhalingsvolgorde

Deze maatregel wordt gedefinieerd als het totale aantal herhalingsorders, als percentage van het totale aantal bestellingen. Anders gezegd, dit is de kans dat een order wordt gevolgd door een andere volgorde. Als deze waarschijnlijkheid groter is dan 50%, betekent dit dat meer dan de helft van alle orders wordt gevolgd door een volgende order.

### Herhaal de waarschijnlijkheid van de volgorde van maanden sinds de bestelling

Deze maatregel toont de waarschijnlijkheid aan dat een gebruiker opnieuw bestelt gezien het aantal maanden dat sinds zijn laatste orde is verstreken. De formule die wordt gebruikt om dit metrisch te produceren vereenvoudigt aan:

![Herhalingskansingsformule](../../assets/Repeat_probability_formula.png)

Afhankelijk van uw bedrijfsmodel kan de waarschijnlijkheid van de herhalingsbestelling onmiddellijk afnemen nadat een klant een bestelling plaatst en in de daaropvolgende maanden verder afneemt, of kan de waarschijnlijkheid seizoensgebonden variaties en pieken aantonen.

In beide gevallen, begrijpt welk percentage van uw klanten naar verwachting herhaalde aankopen zullen doen en hoe deze tendensen in tijd u toestaat om uw klanten met kritieke intervallen te richten om de waarschijnlijkheid van een herhaalde aankoop te maximaliseren. Dus wanneer de waarschijnlijkheid van een herhaalde aankoop afneemt, kunt u een tijd kiezen om een klant te identificeren als &#39;afgekoeld&#39; en uw inspanningen te verschuiven van &#39;vasthouden&#39; naar &#39;reactiveren&#39;.

## Het voorbeeld van vandaag

Kijk eens naar de waarschijnlijkheidsdaling voor een typisch eCommerce-bedrijf.

![Met de waarschijnlijkheid van een eerste herhalingsvolgorde wordt de volgorde in maanden sinds de order herhaald.](../../assets/Order_probability_reports.png)

### Waarschijnlijk eerste herhalingsvolgorde

In dit voorbeeld is de waarschijnlijkheid van de eerste herhalingsvolgorde - of de waarschijnlijkheid dat een volgorde wordt gevolgd door een andere volgorde - 60%. Dit betekent dat 60% van alle bestellingen die bij dit bedrijf worden geplaatst, worden gevolgd door een volgende bestelling.

### Herhaal de waarschijnlijkheid van de volgorde van maanden sinds de bestelling

Dit rapport toont de waarschijnlijkheid dat een klant opnieuw bestelt aangezien een aantal maanden sinds hun laatste orde is verstreken. Hoewel er geen enkele definitie is voor de churn-drempel in dit rapport, raden we aan om de churn te definiëren als het punt waar het kansverlies de waarde overschrijdt die de helft is van de waarschijnlijkheid van de eerste herhaling.

Aangezien de waarschijnlijkheid van de eerste herhaling voor dit voorbeeld 60% is, is de vervaldatum de tijd waarop de waarschijnlijkheid van de herhalingsvolgorde daalt tot minder dan 60%/2 = 30%, of ongeveer 6 maanden. Van de 60% van de bestellingen die met een andere bestelling worden opgevolgd, werd de helft binnen de eerste zes maanden geplaatst.

Een andere manier, als een klant een vervolgorder zou plaatsen, zullen zij eerder dit binnen zes maanden na hun laatste orde dan na het 6 maandteken hebben gedaan. Als een klant na zes maanden niet opnieuw heeft aangeschaft, moet een reactiveringscampagne worden gestart om deze klant weer aan te trekken.

Afhankelijk van uw bedrijfsmodel, kunt u een verschillende drempel, zoals het punt willen kiezen waar de waarschijnlijkheid van de herhaalde orde onder 50% of 10% daalt. Als uw interne kennis een ander aantal suggereert, dan zou u het op alle mogelijke manieren moeten gebruiken!

Uiteindelijk is het de bedoeling om de drempel te selecteren waar het zinvol is om van retentie naar reactivering over te schakelen. Bewaarinspanningen kunnen e-mails omvatten om bestaande klanten opnieuw te betrekken bij voorgestelde vervolgaankopen om deze aan te bieden, terwijl voor reactivering e-mails naar vervallen klanten met coupons en deals nodig kunnen zijn.

## Welke vragen moet ik in overweging nemen?

Om u te helpen de waarschijnlijkheid van herhalingsbestellingen begrijpen zoals deze op uw bedrijf van toepassing is, stellen wij voor deze vragen in overweging te nemen wanneer u uw eigen gegevens onderzoekt:

* Wordt de waarschijnlijkheid van de eerste herhalingsvolgorde verwacht? Zo nee, waarom denkt u dat het hoger of lager moet zijn?
* Zijn er grote dalingen in de waarschijnlijkheid van herhaling gedurende bepaalde maanden sinds laatste orde? Zo ja, worden deze veranderingen verwacht?
* Wat is de huidige churn-drempel?
* Lijnt de huidige churn-drempel uit op een van de waarden in de waarschijnlijkheid van de herhalingsvolgorde voor maanden sinds laatste orderrapport?
* Geeft uw huidige drempelwaarde uw inspanningen voor advertenties weer en overschakelt van retentie naar reactivering?
* Heeft het zin dat uw bedrijf de drempel wijzigt in de maand waarin het waarschijnlijkheidsverlies de waarde overschrijdt die de helft is van het waarschijnlijkheidscijfer bij eerste herhaling?

## Wat moet ik nog meer analyseren?

Nadat u de bovenstaande analyse hebt gemaakt en een drempelwaarde voor het aantal kolommen hebt bepaald, kunt u meer analyses maken om gemeenschappelijke trends in vertrouwde gebruikers te identificeren. Zijn klanten die in dezelfde periode hebben gekocht of hebben ze soortgelijke producten in hun laatste bestelling gekocht? Zodra een kanondrempel wordt geplaatst, kunt u verder in specifieke eigenschappen van deze gekochte klanten duiken.

Als u meer dan één product aanbiedt, vraagt u zich waarschijnlijk af hoe klanten die een specifiek product aanschaffen zich in de loop der tijd anders gedragen dan andere klanten. Wilt u meer weten? Bekijk deze zelfstudie om het levenslange aankoopgedrag van klanten te verkennen op basis van specifieke producten die ze hebben aangeschaft.

Deze beste praktijken worden verstrekt door [!DNL MBI] Data Analysis Services (DAS). We kijken ernaar uit om al uw specifieke zakelijke vragen te beantwoorden! [Contact opnemen met ondersteuning](../../guide-overview.md) voor meer informatie.

### Verwante

* [Analyseren van de invloed van coupons op het verwerven en behouden van klanten](../analysis/coupon-impact.md)
* [Het terugkoopgedrag van klanten analyseren](../analysis/repurchase-behavior.md)
