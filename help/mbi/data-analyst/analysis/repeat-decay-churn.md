---
title: Herhalingswaarschijnlijkheidsverlies en -kromme analyseren
description: Leer en begrijp hoe tijd verloopt tussen bestellingen en wanneer klanten naar verwachting zullen afkoelen.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Verval en kurn van waarschijnlijkheid herhalen

Als een deel van uw opbrengst uit herhaalde aankopen komt, bent u zich waarschijnlijk bewust van de enorme waarde van een loyale klantenbasis. Daarom is het van essentieel belang te begrijpen hoe tijd verstrijkt tussen bestellingen en wanneer van klanten wordt verwacht dat zij zullen afglijden.

Dit onderwerp verkent de analyses die u kunnen helpen de volgende vragen beantwoorden:

* Wat is de kans dat een klant een andere aankoop doet?
* Hoe varieert de waarschijnlijkheid van de herhaalde bestelling in de tijd sinds de laatste aankoop van de klant?
* Wanneer moet een klant als gekost worden beschouwd? En wanneer moet een reactiveringscampagne dan van start gaan?

## Aanbevolen meetwaarden

Wanneer het analyseren van herhalingswaarschijnlijkheidsdaling en kurn, denk na gebruikend ([ of bouwend ](../../data-user/reports/ess-manage-data-metrics.md)) deze metriek:

### Waarschijnlijk eerste herhalingsvolgorde

Deze maatregel wordt gedefinieerd als het totale aantal herhalingsorders, als percentage van het totale aantal bestellingen. Anders gezegd, dit is de kans dat een order wordt gevolgd door een andere volgorde. Wanneer deze waarschijnlijkheid meer dan 50 percenten is, impliceert het dat meer dan de helft van alle orden door een verdere orde wordt gevolgd.

### Herhaal de waarschijnlijkheid van de volgorde van maanden sinds de bestelling

Deze maatregel toont de waarschijnlijkheid aan dat een gebruiker opnieuw bestelt gezien het aantal maanden dat sinds zijn laatste orde is verstreken. De formule die wordt gebruikt om dit metrisch te produceren vereenvoudigt aan:

![ Herhaal kansingsformule ](../../assets/Repeat_probability_formula.png)

Afhankelijk van uw bedrijfsmodel kan de waarschijnlijkheid van de herhalingsbestelling onmiddellijk afnemen nadat een klant een bestelling plaatst en in de daaropvolgende maanden verder afneemt, of kan de waarschijnlijkheid seizoensgebonden variaties en pieken aantonen.

Met een goed begrip van het percentage klanten dat herhaalde aankopen moet doen (en van de manier waarop dit zich in de loop van de tijd ontwikkelt) kunt u uw klanten op gezette tijden als doel instellen om de kans op een herhaalde aankoop zo groot mogelijk te maken. Dus wanneer de waarschijnlijkheid van een herhaalde aankoop afneemt, kunt u een tijd kiezen om een klant te identificeren als afgekoeld en van het vasthouden naar het reactiveren over te schakelen.

## Het voorbeeld van vandaag

Kijk naar de herhalingswaarschijnlijkheidsdaling voor een typisch e-commerce bedrijf.

![ de Aanvankelijke waarschijnlijkheid van de herhalingsorde herhaalt orde bepaalde maanden sinds orde.](../../assets/Order_probability_reports.png)

### Waarschijnlijk eerste herhalingsvolgorde

In dit voorbeeld is de waarschijnlijkheid van de eerste herhalingsbestelling - of de waarschijnlijkheid dat een klant een herhaalde aankoop maakt - 60 procent. Dit betekent dat 60 percent van alle orden die met deze zaken worden geplaatst door een verdere orde worden gevolgd.

### Herhaal de waarschijnlijkheid van de volgorde van maanden sinds de bestelling

Dit rapport toont de waarschijnlijkheid van een klant die opnieuw opdracht geeft aangezien sommige maanden sinds hun laatste orde zijn verstreken. Hoewel er geen enkele definitie van de churn-drempel bestaat op basis van dit rapport, beveelt de Adobe aan om de churn te definiëren als het punt waar het kansverlies de waarde overschrijdt die de helft is van de waarschijnlijkheid van de eerste herhaling.

Aangezien de waarschijnlijkheid van de eerste herhaling voor dit voorbeeld 60% is, is de vervaldatum de tijd waarop de waarschijnlijkheid van de herhalingsvolgorde daalt tot minder dan 60%/2 = 30%, of ongeveer 6 maanden. Van de 60% van de bestellingen die met een andere bestelling moesten worden gevolgd, werd de helft binnen de eerste zes maanden geplaatst.

Een andere manier, als een klant een vervolgorder zou plaatsen, zullen zij eerder dit binnen zes maanden na hun laatste orde dan na het zes maandteken hebben gedaan. Als een klant na zes maanden niet opnieuw heeft aangeschaft, moet een reactiveringscampagne worden gestart om deze klant terug te halen.

Afhankelijk van uw bedrijfsmodel, kunt u een verschillende drempel, zoals het punt willen kiezen waar de waarschijnlijkheid van de herhaalde orde onder 50% of 10% daalt. Als uw interne kennis een ander aantal suggereert, dan moet u het op alle mogelijke manieren gebruiken!

Uiteindelijk is het de bedoeling om de drempel te selecteren waar het zinvol is om van retentie naar reactivering over te schakelen. Bewaarinspanningen kunnen e-mails omvatten om bestaande klanten opnieuw te betrekken bij voorgestelde vervolgaankopen om deze aan te bieden, terwijl voor reactivering e-mails naar vervallen klanten met coupons en deals nodig kunnen zijn.

## Welke vragen moet ik in overweging nemen?

Om u te helpen de waarschijnlijkheid van herhalingsbestellingen begrijpen aangezien het op uw zaken van toepassing is, stelt de Adobe voor om deze vragen te overwegen wanneer u uw eigen gegevens onderzoekt:

* Wordt de waarschijnlijkheid van de eerste herhalingsvolgorde verwacht? Zo nee, waarom denkt u dat het hoger of lager moet zijn?
* Zijn er grote dalingen in de waarschijnlijkheid van herhaling gedurende bepaalde maanden sinds laatste orde? Zo ja, worden deze veranderingen verwacht?
* Wat is de huidige churn-drempel?
* Lijnt de huidige churn-drempel uit op een van de waarden in de waarschijnlijkheid van de herhalingsvolgorde voor maanden sinds laatste orderrapport?
* Geeft uw huidige drempelwaarde uw inspanningen voor advertenties weer en overschakelt van retentie naar reactivering?
* Heeft het zin dat uw bedrijf de drempel wijzigt in de maand waarin het waarschijnlijkheidsverlies de waarde overschrijdt die de helft is van het waarschijnlijkheidscijfer bij eerste herhaling?

## Wat moet ik nog meer analyseren?

Nadat u de bovenstaande analyse hebt gemaakt en een drempelwaarde voor het aantal kolommen hebt bepaald, kunt u meer analyses maken om gemeenschappelijke trends in vertrouwde gebruikers te identificeren. Zijn klanten die in dezelfde periode hebben gekocht of hebben ze soortgelijke producten in hun laatste bestelling gekocht? Zodra een kanondrempel wordt geplaatst, kunt u zich verder in specifieke eigenschappen van deze gekochte klanten duiken.

Als u meer dan één product aanbiedt, vraagt u zich waarschijnlijk af hoe klanten die een specifiek product aanschaffen zich in de loop der tijd anders gedragen dan andere klanten. Wilt u meer weten? Bekijk deze zelfstudie om het levenslange aankoopgedrag van klanten te verkennen op basis van specifieke producten die ze hebben aangeschaft.

Deze best practices worden geleverd door [!DNL Adobe Commerce Intelligence] Data Analysis Services (DAS). [ de steun van het Contact ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) voor meer info.

### Verwante

* [Analyseren van de invloed van coupons op het verwerven en behouden van klanten](../analysis/coupon-impact.md)
* [Het terugkoopgedrag van klanten analyseren](../analysis/repurchase-behavior.md)
