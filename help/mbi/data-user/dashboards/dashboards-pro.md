---
title: Out-of-the-Box Dashboards
description: Leer over dashboards uit-van-de-doos om inzicht in uw zaken te verstrekken.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# Out-of-the-box dashboards

[!DNL Adobe Commerce Intelligence] omvat out-of-the-box dashboards om inzicht in uw zaken te verstrekken. Met dashboards kunt u de gezondheid van essentiële metriek controleren zoals opbrengst van de gebruikersleven, aantal herhaalde aankopen, hoogste producten die over een bepaalde periode, en meer worden gekocht. Deze pre-gevormde dashboards werden gecreeerd om u te helpen geïnformeerde bedrijfsbesluiten nemen.

>[!NOTE]
>
>De toegang tot deze dashboards hangt van uw accounttype en uw toegangsniveau af. Neem contact op met [ondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Beschikbaarheid van rapporten

Voor de `Customers` en `Executive Summary` dashboards, zijn sommige rapporten slechts beschikbaar afhankelijk van de controleconfiguratie van uw opslag. Specifiek, als je winkel uitchecken door gasten toestaat of uitchecken door gasten niet toestaat.

## Klanten (uitchecken door gasten toegestaan)

Het dashboard Klanten (uitchecken door gasten toegestaan) biedt informatie over uw klantenbasis, zoals hun koopgedrag. Dit dashboard kan u helpen klantenbehoud verbeteren en bepalen welke klanten in de hoogste opbrengst brengen.

### Rapporten

| Naam | Beschrijving |
|---|---|
| `Orders by New Customers (Past 30 Days)` | In de afgelopen 30 dagen bestellingen van klanten die nog nooit eerder een bestelling hebben geplaatst. |
| `Orders by Existing Customers (Past 30 Days)` | In de afgelopen 30 dagen bestellingen van klanten die eerder ten minste één bestelling hebben geplaatst. |
| `Total Unique Customers (Past 30 Days)` | Aantal unieke klanten die in de afgelopen 30 dagen orders plaatsen. |
| `Orders by New vs Existing Customers` | Aantal orders door klanten zonder eerdere orders versus klanten met ten minste één eerdere order. |
| `Subsequent Order Probability (All Time)` | De waarschijnlijkheid dat klanten die een bestelling hebben geplaatst een andere plaatsen. |
| `% of Customers with Multiple Orders (All Time)` | Percentage van alle klanten die meerdere bestellingen hebben geplaatst. |
| `Median Time Between Orders (All Time)` | De mediane hoeveelheid tijd die elke klant nodig heeft tussen het plaatsen van een bestelling en de volgende bestelling. |
| `Subsequent Order Probability` | De waarschijnlijkheid dat de klanten die een orde hebben geplaatst een andere orde plaatsen, uitgesplitst door orderaantal. Dat wil zeggen: het percentage klanten met één bestelling die een seconde plaatsen, het percentage met twee die een derde plaatsen, enzovoort. |
| `Time Between Orders` | De gemiddelde en mediane tijd die klanten nemen tussen orders, uitgesplitst naar orderaantal (d.w.z. de tijd tussen bestellingen één en twee, twee en drie, etc.). |
| `Number of Customers - Lifetime Orders` | Voor een bepaald aantal orden die in het leven van een klant worden geplaatst, het aantal klanten die dat vele orden en het percentage van de volledige klantenbasis hebben geplaatst dat aantal vertegenwoordigt. |
| `One-Time Customers who Bought 3-6 Months Ago` | Klanten die tussen drie en zes maanden geleden hun eerste en enige aankoop hebben gedaan. |
| `Avg LTV by First Order` | Vergelijkt de cumulatieve gemiddelde opbrengst van het klantenleven over cohorts. Cohorts worden gedefinieerd door de maand waarin een klant voor het eerst een aankoop heeft gedaan. Bijvoorbeeld een `Jan 2020` cohort toont cumulatief gemiddelde LTV voor klanten wier eerste aankoop in januari 2020 plaatsvond. |
| `Customer's First 30 Day vs Lifetime Revenue` | Vergelijking van de gemiddelde inkomsten van klanten in de 30 dagen na hun eerste aankoop ten opzichte van in hun hele leven. Elke zeepbel komt overeen met een verzendgebied en de grootte van elke zeepbel geeft het aantal klanten aan dat gebied heeft aangeschaft. |

## Klanten (uitchecken door gasten is niet toegestaan)

Het dashboard Klanten (uitchecken door gasten is niet toegestaan) biedt informatie over uw klantenbestand, zoals hun aankoopgedrag en conversies van accountregistraties naar orderplaatsen. Dit dashboard kan u helpen klantenbehoud verbeteren en bepalen welke klanten in de hoogste opbrengst brengen.

### Rapporten

| Naam | Beschrijving |
|---|---|
| `Account Registration (Past 30 Days)` | Het aantal personen dat zich de afgelopen 30 dagen voor een account bij je winkel heeft geregistreerd. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | Het aantal personen dat zich de afgelopen 30 dagen voor een account bij uw winkel heeft geregistreerd en dat ook minstens één bestelling heeft geplaatst. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Percentage van rekeningen die in de afgelopen 30 dagen zijn geregistreerd die een bestelling hebben geplaatst. |
| `% Conversion from Registration to First Order` | Percentage geregistreerde rekeningen die een bestelling hebben gedaan, per maand van registratie. |
| `Orders by New vs Existing Customers` | Aantal orders door klanten zonder eerdere orders versus klanten met ten minste één eerdere order. |
| `Subsequent Order Probability (All Time)` | De waarschijnlijkheid dat klanten die een bestelling hebben geplaatst een andere plaatsen. |
| `% of Customers with Multiple Orders (All Time)` | Percentage van alle klanten die meerdere bestellingen hebben geplaatst. |
| `Median Time Between Orders (All Time)` | De mediane hoeveelheid tijd die elke klant nodig heeft tussen het plaatsen van een bestelling en de volgende bestelling. |
| `Subsequent Order Probability` | De waarschijnlijkheid dat klanten die een bestelling hebben geplaatst een andere plaatsen, uitgesplitst naar bestelnummer. Dat wil zeggen, procent van de klanten met één bestelling die een seconde plaatsen, een procent met twee die een derde plaatsen, enzovoort. |
| `Time Between Orders` | De gemiddelde en mediane tijd die klanten nemen tussen orders, uitgesplitst naar orderaantal (d.w.z. de tijd tussen bestellingen één en twee, twee en drie, etc.). |
| `Number of Customers - Lifetime Orders` | Voor een bepaald aantal orden die in het leven van een klant worden geplaatst, het aantal klanten die dat vele orden en het percentage van de volledige klantenbasis hebben geplaatst dat aantal vertegenwoordigt. |
| `One-Time Customers who Bought 3-6 Months Ago` | Klanten die tussen drie en zes maanden geleden hun eerste en enige aankoop hebben gedaan. |
| `Avg LTV by First Order` | Vergelijkt de cumulatieve gemiddelde opbrengst van het klantenleven over cohorts. Cohorts worden gedefinieerd door de maand waarin een klant voor het eerst een aankoop heeft gedaan. Zo toont een cohort van 2020 bijvoorbeeld een cumulatief gemiddelde LTV voor klanten wier eerste aankoop in januari 2020 plaatsvond. |
| `Customer's First 30 Day vs Lifetime Revenue` | Vergelijking van de gemiddelde inkomsten van klanten in de 30 dagen na hun eerste aankoop ten opzichte van in hun hele leven. Elke zeepbel komt overeen met een verzendgebied en de grootte van elke zeepbel geeft het aantal klanten aan dat gebied heeft aangeschaft. |

## Executive Summary (uitchecken door gasten toegestaan)

Het dashboard Executive Summary (uitchecken van gasten toegestaan) geeft u een beknopt beeld van hoe het bedrijf in termen van bestellingen en inkomsten doet. Dit dashboard is ontworpen voor managers om een algemeen inzicht in bedrijfsprestaties te krijgen, maar kan ook voor anderen inzichtelijk zijn.

### Rapporten

| Naam | Beschrijving |
|---|---|
| `Revenue (Current Month)` | De opbrengst die door uw opslag voor de huidige maand is geproduceerd. In dit geval wordt de opbrengst gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `Revenue (Past 6 Months by Day)` | Totale dagelijkse inkomsten, berekend op basis van de gemiddelde dagelijkse inkomsten van de afgelopen zeven dagen. In dit geval wordt de opbrengst gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `% Change in Revenue (MoM MTD)` | Vergelijking van de inkomsten in de huidige maand (tot nu toe) met hetzelfde deel van de vorige maand. |
| `Revenue from New vs Existing Customers (Current Month)` | Ontvangsten voor de huidige maand (tot dusver) toegerekend aan nieuwe (eerste) klanten versus bestaande klanten (het plaatsen van tweede of latere bestelling). |
| `Average Order Value (Current Month)` | Gemiddelde dagelijkse waarde van de in de lopende maand geplaatste orders (tot dusver). De bestelwaarde wordt gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `Orders (Current Month)` | Het aantal bestellingen dat voor de huidige maand in uw winkel is geplaatst (tot nu toe). |
| `% Change in Orders (MoM MTD)` | Vergelijking van het aantal orders voor de huidige maand (tot dusver) met hetzelfde gedeelte van de voorgaande maand. |
| `Orders by New Customers (Current Month)` | Orders voor de huidige maand van klanten die nog geen bestelling hebben geplaatst. |
| `Orders by Existing Customers (Current Month)` | Orders voor de huidige maand van klanten die eerder minstens één bestelling hebben geplaatst. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Aantal orders door klanten zonder eerdere orders vs. door klanten met ten minste één eerdere order, voor elke week van het lopende jaar (tot dusver). |

## Samenvatting (uitchecken door gast is niet toegestaan)

Het dashboard Executive Summary (geen uitcheckprocedure voor gasten toegestaan) geeft u een beknopt beeld van hoe het bedrijf in termen van bestellingen, inkomsten, en rekeningsregistraties doet. Dit dashboard is ontworpen voor managers om een algemeen inzicht in bedrijfsprestaties te krijgen, maar kan ook voor anderen inzichtelijk zijn.

### Rapporten

| Naam | Beschrijving |
|---|---|
| `Revenue (Current Month)` | De inkomsten die deze maand door uw opslag zijn gegenereerd. In dit geval wordt de opbrengst gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `Revenue (Past 6 Months by Day)` | Totale dagelijkse inkomsten, berekend op basis van de gemiddelde dagelijkse inkomsten van de afgelopen zeven dagen. In dit geval wordt de opbrengst gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `% Change in Revenue (MoM MTD)` | Vergelijking van de inkomsten tot nu toe deze maand met hetzelfde deel van de vorige maand. |
| `Revenue from New vs Existing Customers (Current Month)` | Ontvangsten voor de huidige maand (tot dusver) toegerekend aan nieuwe (eerste) klanten versus bestaande klanten (het plaatsen van tweede of latere bestelling). |
| `Average Order Value (Current Month)` | Gemiddelde dagelijkse waarde van de in de lopende maand geplaatste orders (tot dusver). De bestelwaarde wordt gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `Orders (Current Month)` | Het aantal bestellingen dat voor de huidige maand in uw winkel is geplaatst (tot nu toe). |
| `% Change in Orders (MoM MTD)` | Vergelijking van het aantal orders voor de huidige maand (tot dusver) met hetzelfde gedeelte van de voorgaande maand. |
| `Account Registrations (Current Month)` | Het aantal pas ingeschreven accounts tot nu toe deze maand. |
| `% Conversion from Registration to First Order (Current Month)` | Het percentage accounts dat deze maand is geregistreerd en dat een bestelling heeft geplaatst. |
| `% Conversion from Registration to First Order (Current Year by Week)` | Het percentage van de rekeningen die dit jaar tot nu toe elke week zijn geregistreerd en die een bestelling hebben geplaatst. |

## Orders

Het dashboard voor bestellingen biedt inzicht in het transactievolume van orders, de status ervan, de gebruikte couponcodes, de gegenereerde inkomsten en de gebruikte betalingsmethoden. U kunt bijvoorbeeld het afhandelingsproces volgen en controleren of er geen problemen zijn of knelpunten optreden.

>[!NOTE]
>
>De rapporten op dit dashboard zijn beschikbaar voor rekeningen die met één van beide type van configuratie (gastcontrole, geen gastcontrole) worden verbonden.

### Rapporten

| Naam | Beschrijving |
|---|---|
| `Orders (Past 30 Days)` | Het aantal bestellingen dat de afgelopen 30 dagen bij je winkel is geplaatst. |
| `Revenue (Past 30 Days)` | De inkomsten die uw winkel de afgelopen 30 dagen heeft gegenereerd. Opbrengsten worden gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `Average Order Value (Past 30 Days)` | Gemiddelde waarde van in de afgelopen 30 dagen uitgevoerde orders. De bestelwaarde wordt gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `Orders` | Het aantal bestellingen dat elke maand in uw winkel wordt geplaatst. |
| `Revenue by Payment Method` | De inkomsten die door uw winkel zijn gegenereerd, worden uitgesplitst naar betalingsmethode. Opbrengsten worden gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `AOV by New vs Existing Customers` | Gemiddelde maandwaarde van bestellingen die in uw winkel zijn gedaan, gedeeld door bestellingen die klanten zonder eerdere bestellingen hebben gedaan, versus klanten met ten minste één eerdere bestelling. De bestelwaarde wordt gedefinieerd als de uiteindelijke prijs die een klant op een bestelling betaalt. |
| `% Orders by Status (Past 30 Days)` | Percentage van bestellingen van elke dag in de afgelopen 30 dagen dat zich momenteel in elke orderstatus bevindt. |
| `Incomplete Orders (Created more than 1 Day Ago)` | Een lijst met alle orders die meer dan een dag geleden zijn geplaatst en die nog steeds onvolledig zijn (niet geannuleerd of voltooid). |
| `Orders Per Hour (Past 7 Days)` | Volgorde van volume per dag en per uur. |
| `Revenue Details (Past 30 Days)` | Uitsplitsing van de dagelijkse inkomsten over de afgelopen 30 dagen in alle componenten van de totale opbrengstwaarde. |
| `Order Details by Coupon Code (Past 30 Days)` | Voor elke couponcode die je winkel aanbiedt, kun je aangeven hoe die couponcode is gebruikt en wat de afgelopen 30 dagen de aanwinst is. |
| `% Orders with Coupon (Past 30 Days)` | Het percentage in de afgelopen 30 dagen geplaatste opdrachten waarbij een coupon werd gebruikt in vergelijking met orders die dat niet deden. |

## Producten

Het dashboard Producten toont algemene productprestaties in termen van bestelde producten, hun Bruto Waarde van de Handelswaren (GMV), en hoogste producten die worden gekocht en terugbetaald. Het kan u helpen aankopen en terugkeren in evenwicht te brengen, en productsucces en populariteit te bepalen. Je winkel moet [geconfigureerd voor het bijhouden van restituties](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) voor die grafieken die moeten worden ingevuld.

>[!NOTE]
>
>De rapporten op dit dashboard zijn beschikbaar voor rekeningen die met één van beide type van configuratie (gastcontrole, geen gastcontrole) worden verbonden.

### Rapporten

| Naam | Beschrijving |
|---|---|
| `GMV (Past 30 Days)` | De bruto-handelswaarde van alle producten die in de afgelopen dertig dagen zijn verkocht. GMV wordt gedefinieerd als de bestelde hoeveelheid vermenigvuldigd met de basisprijs voor elk product. |
| `% GMV (Past 30 Days) Refunded` | Percentage GMV voor producten die in die laatste 30 dagen zijn aangekocht en die tot een restitutie hebben geleid. |
| `Product Quantity Ordered (Past 30 Days)` | Totale hoeveelheid in de afgelopen 30 dagen bestelde objecten. |
| `% Purchased Products (Past 30 Days) Refunded` | Percentage van de objecten die in de laatste 30 dagen zijn aangeschaft en die hebben geresulteerd in restitutie. |
| `Gross Merchandise Value` | De brutowaarde van alle verkochte producten per maand. GMV wordt gedefinieerd als de bestelde hoeveelheid vermenigvuldigd met de basisprijs voor elk product. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | Voor elk product wordt een vergelijking gemaakt tussen het totale aantal bestellingen in de afgelopen 30 dagen en de restitutievoet voor het product. De grootte van elke bel staat voor de restitutievoet. |
| `Product Performance Details (Past 30 Days)` | Gedetailleerde informatie over de verkoop en de restituties die in de afgelopen 30 dagen zijn toegekend, per productgroep en per productnaam. |
| `Top Purchased Products by GMV (Past 30 Days)` | Producten die in de afgelopen 30 dagen werden verkocht en de meeste inkomsten opleverden (top 10). |
| `Top Refunded Products by GMV (Past 30 Days)` | Producten die in de afgelopen 30 dagen zijn aangekocht en waarbij de meeste GMV door restituties verloren is gegaan (top 10). |
| `Top Purchased Products by Quantity (Past 30 Days)` | Producten die in de afgelopen 30 dagen in de meeste aantallen zijn verkocht (top 10). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Producten die in de afgelopen 30 dagen zijn aangekocht en waarbij de grootste hoeveelheid is terugbetaald (top 10). |
