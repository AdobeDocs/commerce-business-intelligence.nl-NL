---
title: Het rendement van uw reclamecampagnes verhogen
description: Meer informatie over enkele verschillende methoden om de prestaties van uw campagne te evalueren.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Reclamecampagnes en investeringsrendement

[!DNL Adobe Commerce Intelligence] staat u toe gemakkelijk [Gegevens over advertentiekosten en inkomstengegevens combineren](../../data-analyst/importing-data/integrations/google-adwords.md) uit uw database. Dit helpt u identificeren welke campagnes het hoogste rendement op investering (ROI) hebben. In dit onderwerp worden enkele verschillende methoden voor het evalueren van de prestaties van uw campagne besproken.

## Vereisten

* Je gegevens over advertentiekosten importeren:
   * [Verbind uw [!DNL Google AdWords] tot [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): Dit synchroniseert uw [!DNL Adwords] uitgeven in [!DNL Commerce Intelligence]
   * [Andere gegevens over advertentiekosten uploaden](../importing-data/connecting-data/import-offline-ad-data.md): Dit wordt aanbevolen voor kanalen zonder directe aansluiting op [!DNL Commerce Intelligence]
   * Als u kostengegevens uit meerdere bronnen importeert, kunt u [consolideren](../../best-practices/consolidating-your-tables.md) de gegevens in [!DNL Commerce Intelligence]. Eenvoudig [een ondersteuningsticket indienen](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Kanaalgegevens van verwervingskanalen bijhouden](../analysis/google-track-user-acq.md)

## Aankoopcampagnes voor gebruikers

Campagnes die gericht zijn op gebruikersverwerving kunnen vanuit vele perspectieven worden gemeten, zoals:

1. Het aantal nieuwe gebruikers dat van campagnes is aangeschaft
1. De omrekeningskoers van registratie tot aankoop van campagnes
1. Het rendement van campagnes op basis van de gemiddelde levensduur van de gebruiker (LTV)

De bovenstaande analyses (1) en (2) worden in een aparte zelfstudie besproken op [uw belangrijkste marketingkanalen identificeren](../analysis/most-value-source-channel.md). Hier, onderzoekt u analyse (3) om campagne ROI in tijd te meten. Hiermee wordt beantwoord of gebruikers die zijn aangeschaft tijdens een bepaalde campagne voldoende inkomsten hebben gegenereerd om de aanschafkosten te dekken.

>[!NOTE]
>
>In dit voorbeeld wordt ervan uitgegaan dat alle campagnekosten uitsluitend werden gebruikt om nieuwe gebruikers aan te schaffen. In werkelijkheid worden uw campagnekosten ook gedeeld met het aanschaffen van ongeconverteerde bezoeken, herhaalde kopers en dergelijke. Door ervan uit te gaan dat alle kosten worden gebruikt om nieuwe geregistreerde gebruikers aan te schaffen, wordt het meest ongunstige scenario (hoogste kosten per overname) in het resulterende rendement verwerkt. U kunt zeker zijn dat uw daadwerkelijke ROI hoger is dan uw berekening.
>
>Voorbeeld: Ervan uitgaande dat je $20 hebt uitgegeven aan een campagne die 10 nieuwe gebruikers en 10 herhaalde kopers heeft gegenereerd, bedragen de werkelijke kosten per nieuwe gebruiker $1. Maar, in de veronderstelling dat alle kosten gingen om nieuwe gebruikers te verwerven, zijn de kosten per aankoop $2.

**1. Begin door een grafiek te creëren die uw Advertentiekosten door Campagnes segmenteert:**

1. Een [!UICONTROL Metric] dat de uitgaven in de loop der tijd
1. Ga naar [!UICONTROL Data > Metrics]
1. Selecteren `Add New Metric` en selecteert u de [!DNL `Adwords...`] tabel die uw [!DNL AdWords] kostengegevens.
1. Geef in de metrische editor uw metrische waarde een naam (bijvoorbeeld [!UICONTROL AdWord Cost])
1. Voer met behulp van de dropdowns een **Som** op de `adCost` in de [!DNL Adwords...] tabel (Wijzigen) die is geordend door de `date` kolom.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Klikken `Back to Metric List` bovenaan en ga naar een dashboard.

1. Een rapport maken dat segmenten via campagnes doorgeven
1. Klik in een dashboard op [!UICONTROL Add Report > Create report]
1. Selecteer [!UICONTROL Adword Cost] de zojuist gemaakte metrische waarde
1. Stel de [!UICONTROL Time period] tot `All-time`, en [!UICONTROL Interval] tot `None`
1. Onder de `Group by` tab, toevoegen `campaign` als [!UICONTROL grouping field]en klik op `Add All` in de doos.
1. Dit rapport laat uw hele tijd zien [!DNL AdWords] kosten via campagnes

**2. Creeer een rapport dat nieuwe gebruikers door campagnes telt:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create report]**
1. Selecteer `New users` metrisch die het aantal nieuwe geregistreerde gebruikers in tijd telt
1. Stel de [!UICONTROL Time period] tot `All-time`, en [!UICONTROL Interval] tot `None`
1. Onder de `Group by` tab, toevoegen `campaign` als `grouping field`en klik op **`Add All`** in het vak
1. In dit rapport worden uw geregistreerde gebruikers tijdens de hele periode via campagnes weergegeven

**3. Creeer een rapport dat gemiddelde gebruiker LTV door campagnes segmenteert:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create report]**
1. Selecteer `Average lifetime revenue` Metrisch die de inkomsten van een gemiddelde gebruiker tijdens zijn leven berekent
1. Stel de [!UICONTROL Time period] tot `All-time`, en [!UICONTROL Interval] tot `None`
1. Onder de `Group by` tab, toevoegen `campaign` of `utm\_campaign` als [!UICONTROL grouping field]en klik op `Add All` in het vak
1. Dit rapport toont uw gemiddelde opbrengst van het gebruikersleven door campagnes

**Tot slot moet u het ROI van de campagne berekenen door deze drie analyses samen te brengen in één verslag:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create new report]**
1. Voeg toe als invoer en gebruik de drie bovenstaande maatstaven. Elke letter wordt toegewezen (bijvoorbeeld\[`A`\], \[`B`\] en \[`C`\])
1. [!UICONTROL Cost]: Voeg de kosten van de metrische Advertentiewoorden toe - dit is variabele \[A\]. Dit brengt kosten door campagnes terug.
1. [!UICONTROL Users]: Voeg de metrische nieuwe gebruikers toe - dit is variabele \[B\]. Hierdoor wordt het aantal gebruikers via campagnes geretourneerd.
1. [!UICONTROL LTV]: Voeg de gemiddelde omzet van Levensduur metrisch toe - dit is veranderlijke \[`C`\]. Dit retourneert LTV via campagnes.

1. Klik op het pictogram Verbergen naast het woord Grafiek zodat u zich op de tabel kunt concentreren
1. Nu gebruiken `Add Formula` om deze cijfers als volgt te combineren:
1. [!UICONTROL ROI]: Voer de formule in `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, als \[`A`\] staat voor `Ad Cost by Campaigns`, \[`B`\] staat voor `New users by campaigns`, en \[`C`\] `LTV by campaigns`. Dit geeft de verhouding tussen (gemiddelde LTV van gebruikers - gemiddelde kostprijs per aankoop) / (gemiddelde kostprijs per aankoop)
1. [!UICONTROL Avg Return per User]: Voer de formule in **\[`C`\]-(\[`A`\]/\[`B`\])**. Dit geeft de gemiddelde marge voor een gebruiker terug door (gemiddelde LTV-gebruiker) te berekenen - (gemiddelde kosten per aankoop).
1. [!UICONTROL CPA]: Voer de formule in **`\[A\]/\[B\]`**. Dit retourneert de werkelijke kosten van de campagne per aankoop.
1. Andere mogelijke meetgegevens die moeten worden opgenomen van [!DNL AdWords] gegevens omvatten sommen  `Impressions` en `adClicks` (van [!DNL AdWords] gegevens), samen met het totaal `number of orders` via een bepaalde campagne.
1. Het kan ook interessant zijn om het rendement van investeringen te berekenen op basis van LTV 30 dagen en 90 dagen nadat een gebruiker zich heeft geregistreerd of een eerste aankoop doet.

1. Voel vrij om uw metriek en formules te klikken en te slepen om de kolommen van uw rapport te herschikken
1. Geef uw rapport een naam en zorg ervoor dat u het opslaat als een tabel.

## Productcampagnes

Gebruikt u productspecifieke advertenties? Als dat het geval is, kunt u de ROI op die campagnes meten door de opbrengsten/kosten voor specifieke producten te berekenen.

>[!NOTE]
>
>In dit voorbeeld wordt ervan uitgegaan dat alle campagnekosten uitsluitend werden gebruikt om aankopen van specifieke producten te genereren. Door ervan uit te gaan dat alle kosten werden besteed aan het genereren van aankopen, maakt het resulterende rendement van investeringen het worstcasescenario (hoogste kosten per aankoop). U kunt zeker zijn dat uw daadwerkelijke ROI hoger is dan deze berekening. Voorbeeld: Ervan uitgaande dat u $20 hebt uitgegeven aan een campagne die tien nieuwe gebruikers en tien aankopen heeft gegenereerd, bedragen uw werkelijke kosten per aankoop $1. Onder de veronderstelling dat alle kosten gingen om nieuwe gebruikers te verwerven, zijn de kosten per aankoop $2.

Voordat u begint, [een ondersteuningsticket indienen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om de volgende afmetingen aan uw lijst van lijnpunten ( te verbinden`sales\_flat\_order\_item, order\_item`):

* De bron van de orde (als u slechts verwijzingsbron op het gebruikersniveau bijhoudt, dan zich bij de bron van de gebruiker aansluit)
* De campagne van de orde (als u slechts verwijzingsbron op het gebruikersniveau bijhoudt, dan zich bij de campagne van de gebruiker aansluit)
* Het middel van de orde (als u slechts verwijzingsbron op het gebruikersniveau bijhoudt, dan zich bij het middel van de gebruiker aansluit)

**1. Begin nu door een grafiek te creëren die opbrengst per campagne voor specifiek product(en) terugkeert:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create new report]**
1. Selecteer `Revenue by items` metrisch die opbrengst op het niveau van lijnpunten berekent
1. Stel de [!UICONTROL Time period] tot `All-time`, en [!UICONTROL Interval] tot `None`
1. Onder de `Filter by` tab, toevoegen `product name 'IN'` Product `A`, Product `B`, Product `C`, ...&quot; en neemt alle productnamen op waarop uw campagne betrekking heeft, gescheiden door een komma (bijvoorbeeld `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Onder de `Group by` tab, toevoegen `order's campaign` of `order's utm\_campaign` als `grouping` en klik op **[!UICONTROL Add All]** in het vak
1. In dit verslag worden de inkomsten voor specifieke producten via campagnes weergegeven

**2. Om ROI te berekenen, combineert u opnieuw metriek in één rapport:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create new report]**
1. Voeg de `Revenue by items` metrisch, die het filter en de groep door richtingen van de campagne voor specifiek(e) product(en) rapport hierboven volgen en klikken **[!UICONTROL Hide]** onder de scalaire waarde van metrisch
1. Voeg nu de [!DNL AdWords Cost] metrisch, die de filter en de groep door richtingen van `Ad cost by campaigns` rapport dat u hebt verkend in `User acquisition campaigns` deel hierboven; klik vervolgens op **[!UICONTROL Hide]** onder de scalaire waarde van metrisch
1. Voeg formules toe met deze meetwaarden:
1. [!UICONTROL ROI]: Voer de formule in `\[A\]/\[B\]`, als `\[A\]` vertegenwoordigt `Revenue per campaign for specific product(s)` en `\[B\]` vertegenwoordigt `Ad cost by campaigns`. Hiermee wordt de verhouding tussen (inkomsten voor specifieke producten) / (Campagnekosten) geretourneerd
1. [!UICONTROL Return]: Voer de formule in `\[A\]-\[B\]`. Dit geeft de gemiddelde marge voor een gebruiker door te berekenen (gemiddelde LTV-gebruiker) - (gemiddelde kostprijs per aankoop)
1. (Optioneel) [!UICONTROL Revenue]: De verbergen van `Revenue by items` Metrisch om de opbrengsten voor specifieke producten per campagne te zien
1. (Optioneel) [!UICONTROL Cost]: De verbergen van `AdWords Cost` metrisch om de kosten van campagnes te zien

1. Geef uw rapport een naam en zorg ervoor het als lijst bewaart

**3. Herhaal stap 1 en 2 voor elk van uw geadverteerde producten of productgroep(en).**

## Gerelateerde documentatie

* [Referentiebron voor bestelling volgen via [!DNL Google Analytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../analysis/track-usr-dev-browser.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)
* [Verbind uw [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Hoe werkt [!DNL Google Analytics] UTM-toewijzingswerk?](../analysis/utm-attributes.md)
* [Vijf aanbevolen procedures voor UTM-tags in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
