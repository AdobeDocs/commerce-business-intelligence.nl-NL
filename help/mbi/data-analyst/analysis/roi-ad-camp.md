---
title: Het rendement van uw reclamecampagnes verhogen
description: Meer informatie over enkele verschillende methoden om de prestaties van uw campagne te evalueren.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Advertising-campagnes en ROI

[!DNL Adobe Commerce Intelligence] staat u toe om [ gemakkelijk te trouwen de gegevens van de reclamekosten en opbrengst ](../../data-analyst/importing-data/integrations/google-adwords.md) van uw gegevensbestand. Dit helpt u identificeren welke campagnes het hoogste rendement op investering (ROI) hebben. In dit onderwerp worden enkele verschillende methoden voor het evalueren van de prestaties van uw campagne besproken.

## Vereisten

* Je gegevens over advertentiekosten importeren:
   * [ verbind uw  [!DNL Google AdWords]  met  [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): Dit synchroniseert uw [!DNL Adwords] besteedt in [!DNL Commerce Intelligence]
   * [ uploadt andere reclame kostengegevens ](../importing-data/connecting-data/import-offline-ad-data.md): Dit wordt geadviseerd voor kanalen zonder een directe schakelaar aan [!DNL Commerce Intelligence]
   * Als u kostengegevens uit veelvoudige bronnen invoert, kunt u [&#128279;](../../best-practices/consolidating-your-tables.md) de gegevens in [!DNL Commerce Intelligence] consolideren. Eenvoudig [ voorlegt een steunkaartje ](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Kanaalgegevens van verwervingskanalen bijhouden](../analysis/google-track-user-acq.md)

## Aankoopcampagnes voor gebruikers

Campagnes die gericht zijn op gebruikersverwerving kunnen vanuit vele perspectieven worden gemeten, zoals:

1. Het aantal nieuwe gebruikers dat van campagnes is aangeschaft
1. De omrekeningskoers van registratie tot aankoop van campagnes
1. Het rendement van campagnes op basis van de gemiddelde levensduur van de gebruiker (LTV)

Analyseert (1) en (2) hierboven worden verkend in een afzonderlijk leerprogramma op [ identificerend uw hoogste marketing kanalen ](../analysis/most-value-source-channel.md). Hier, onderzoekt u analyse (3) om campagne ROI in tijd te meten. Hiermee wordt beantwoord of gebruikers die zijn aangeschaft tijdens een bepaalde campagne voldoende inkomsten hebben gegenereerd om de aanschafkosten te dekken.

>[!NOTE]
>
>In dit voorbeeld wordt ervan uitgegaan dat alle campagnekosten uitsluitend werden gebruikt om nieuwe gebruikers aan te schaffen. In werkelijkheid worden uw campagnekosten ook gedeeld met het aanschaffen van ongeconverteerde bezoeken, herhaalde kopers en dergelijke. Door ervan uit te gaan dat alle kosten worden gebruikt om nieuwe geregistreerde gebruikers aan te schaffen, wordt het meest ongunstige scenario (hoogste kosten per overname) in het resulterende rendement verwerkt. U kunt zeker zijn dat uw daadwerkelijke ROI hoger is dan uw berekening.
>
>Voorbeeld: Ervan uitgaande dat je $20 hebt uitgegeven aan een campagne die 10 nieuwe gebruikers en 10 herhaalde kopers genereerde, bedragen de werkelijke kosten per nieuwe gebruiker $1. Maar, in de veronderstelling dat alle kosten gingen om nieuwe gebruikers te verwerven, zijn de kosten per aankoop $2.

**1. Begin door een grafiek te creëren die uw Advertentiekosten door Campagnes segmenteert:**

1. Maak een [!UICONTROL Metric] die uw uitgaven in de loop van de tijd opsomt
1. Ga naar [!UICONTROL Data > Metrics]
1. Selecteer `Add New Metric` en selecteer de [!DNL `Adwords...`] -tabel die uw [!DNL AdWords] kostengegevens opneemt.
1. Geef uw metrische waarde in de metrische editor een naam (bijvoorbeeld [!UICONTROL AdWord Cost] )
1. Gebruikend dropdowns, voer a **Som** op de `adCost` kolom in de [!DNL Adwords...] lijst (Verandering) uit die door de `date` kolom wordt bevolen.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Klik op `Back to Metric List` bovenaan en ga naar een willekeurig dashboard.

1. Een rapport maken dat segmenten via campagnes doorgeven
1. Klik in een dashboard op [!UICONTROL Add Report > Create report]
1. Selecteer de metrische waarde die u net hebt gemaakt. [!UICONTROL Adword Cost]
1. Stel de waarden [!UICONTROL Time period] in op `All-time` en [!UICONTROL Interval] op `None`
1. Voeg onder het tabblad `Group by` `campaign` as [!UICONTROL grouping field] toe en klik op `Add All` in het vak.
1. In dit rapport worden uw kosten voor de hele tijd [!DNL AdWords] via campagnes getoond

**2. Creeer een rapport dat nieuwe gebruikers door campagnes telt:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create report]**
1. Selecteer `New users` die het aantal nieuwe geregistreerde gebruikers in tijd telt
1. Stel de waarden [!UICONTROL Time period] in op `All-time` en [!UICONTROL Interval] op `None`
1. Voeg onder het tabblad `Group by` `campaign` as `grouping field` toe en klik op **`Add All`** in het vak
1. In dit rapport worden uw geregistreerde gebruikers tijdens de hele periode via campagnes weergegeven

**3. Creeer een rapport dat gemiddelde gebruiker LTV door campagnes segmenteert:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create report]**
1. Selecteer de `Average lifetime revenue` -maatstaf die de inkomsten van een gemiddelde gebruiker berekent
1. Stel de waarden [!UICONTROL Time period] in op `All-time` en [!UICONTROL Interval] op `None`
1. Voeg onder het tabblad `Group by` `campaign` of `utm\_campaign` toe als [!UICONTROL grouping field] en klik op `Add All` in het vak
1. Dit rapport toont uw gemiddelde opbrengst van het gebruikersleven door campagnes

**tot slot, bereken campagne ROI door deze drie analyses in één rapport samen te brengen:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create new report]**
1. Voeg toe als invoer en gebruik de drie bovenstaande maatstaven. Aan elk is een letter toegewezen (bijvoorbeeld \[`A`\], \[`B`\] en \[`C`\])
1. [!UICONTROL Cost]: voeg de kosten voor de metrische Advertentiewoorden toe. Dit is een variabele \[A\]. Dit brengt kosten door campagnes terug.
1. [!UICONTROL Users]: voeg de metrische nieuwe gebruikers toe - dit is variabele \[B\]. Hierdoor wordt het aantal gebruikers via campagnes geretourneerd.
1. [!UICONTROL LTV]: voeg de metrische gemiddelde opbrengst van de Levensduur toe - dit is veranderlijke \ [`C` \]. Dit retourneert LTV via campagnes.

1. Klik op het pictogram Verbergen naast het woord Grafiek zodat u zich op de tabel kunt concentreren
1. Gebruik `Add Formula` nu om deze cijfers als volgt te combineren:
1. [!UICONTROL ROI]: Voer de formule `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])` in als \[`A`\] `Ad Cost by Campaigns` vertegenwoordigt, \[`B`\] `New users by campaigns` vertegenwoordigt en \[`C`\] `LTV by campaigns`. Dit geeft de verhouding tussen (gemiddelde LTV van gebruikers - gemiddelde kostprijs per aankoop) / (gemiddelde kostprijs per aankoop)
1. [!UICONTROL Avg Return per User]: Ga de formule **\ in \ [`C` \] - (\ [`A` \]/\ [`B` \])**. Dit geeft de gemiddelde marge voor een gebruiker terug door (gemiddelde LTV-gebruiker) te berekenen - (gemiddelde kosten per aankoop).
1. [!UICONTROL CPA]: voer de formule in **`\[A\]/\[B\]`** . Dit retourneert de werkelijke kosten van de campagne per aankoop.
1. Andere mogelijke meetgegevens die van [!DNL AdWords] gegevens kunnen worden opgenomen, zijn sommen `Impressions` en `adClicks` (van [!DNL AdWords] data), samen met het totaal `number of orders` dat via een bepaalde campagne is gemaakt.
1. Het kan ook interessant zijn om het rendement van investeringen te berekenen op basis van LTV 30 dagen en 90 dagen nadat een gebruiker zich heeft geregistreerd of een eerste aankoop doet.

1. Voel vrij om uw metriek en formules te klikken en te slepen om de kolommen van uw rapport te herschikken
1. Geef uw rapport een naam en zorg ervoor dat u het opslaat als een tabel.

## Productcampagnes

Gebruikt u productspecifieke advertenties? Als dat het geval is, kunt u de ROI op die campagnes meten door de opbrengsten/kosten voor specifieke producten te berekenen.

>[!NOTE]
>
>In dit voorbeeld wordt ervan uitgegaan dat alle campagnekosten uitsluitend werden gebruikt om aankopen van specifieke producten te genereren. Door ervan uit te gaan dat alle kosten werden besteed aan het genereren van aankopen, maakt het resulterende rendement van investeringen het worstcasescenario (hoogste kosten per aankoop). U kunt zeker zijn dat uw daadwerkelijke ROI hoger is dan deze berekening. Voorbeeld: Ervan uitgaande dat u $20 hebt uitgegeven aan een campagne die 10 nieuwe gebruikers en 10 aankopen genereerde, zijn uw werkelijke kosten per aankoop $1. Onder de veronderstelling dat alle kosten gingen om nieuwe gebruikers te verwerven, zijn de kosten per aankoop $2.

Alvorens u begint, [ voorlegt een steunkaartje ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om zich bij de volgende dimensies aan uw lijst van lijnpunten (`sales\_flat\_order\_item, order\_item`) aan te sluiten:

* De bron van de orde (als u slechts verwijzingsbron op het gebruikersniveau bijhoudt, dan zich bij de bron van de gebruiker aansluit)
* De campagne van de orde (als u slechts verwijzingsbron op het gebruikersniveau bijhoudt, dan zich aansluit bij gebruikerscampagne)
* Het middel van de orde (als u slechts verwijzingsbron op het gebruikersniveau bijhoudt, dan zich bij het middel van de gebruiker aansluit)

**1. Begin nu door een grafiek te creëren die opbrengst per campagne voor specifiek product(en) terugkeert:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create new report]**
1. Selecteer `Revenue by items` metrisch die opbrengst op het niveau van lijnpunten berekent
1. Stel de waarden [!UICONTROL Time period] in op `All-time` en [!UICONTROL Interval] op `None`
1. Voeg onder het tabblad `Filter by` `product name 'IN'` Product `A` , Product `B` , Product `C` ...&quot; toe en voeg alle productnamen toe die voor uw campagne zijn bedoeld, gescheiden door een komma (bijvoorbeeld `product name 'IN' yellow t-shirt` , `red t-shirt, blue t-shirt` )
1. Voeg onder de tab `Group by` `order's campaign` of `order's utm\_campaign` toe als `grouping` veld en klik op **[!UICONTROL Add All]** in het vak
1. In dit verslag worden de inkomsten voor specifieke producten via campagnes weergegeven

**2. Om ROI te berekenen, combineert u opnieuw metriek in één rapport:**

1. Klik in een dashboard op **[!UICONTROL Add Report > Create new report]**
1. Voeg de `Revenue by items` -metrische waarde toe, waarbij u het filter en de groep op aanwijzingen van de campagne voor het/de specifieke product(en)-rapport hierboven volgt en op **[!UICONTROL Hide]** onder de scalaire waarde van de meting klikt
1. Voeg nu de metrische waarde [!DNL AdWords Cost] toe, die het filter en de groep op richtingen van het `Ad cost by campaigns` rapport volgt u in de `User acquisition campaigns` sectie hierboven verkende; dan klik **[!UICONTROL Hide]** onder de scalaire waarde van metrisch
1. Voeg formules toe met deze meetwaarden:
1. [!UICONTROL ROI]: voer de formule `\[A\]/\[B\]` in als `\[A\]` `Revenue per campaign for specific product(s)` en `\[B\]` `Ad cost by campaigns` vertegenwoordigt. Hiermee wordt de verhouding tussen (inkomsten voor specifieke producten) en (campagnekosten) gegeven
1. [!UICONTROL Return]: voer de formule in `\[A\]-\[B\]` . Dit geeft de gemiddelde marge voor een gebruiker door te berekenen (gemiddelde LTV-gebruiker) - (gemiddelde kostprijs per aankoop)
1. (Optioneel) [!UICONTROL Revenue]: maak de `Revenue by items` -meting zichtbaar om de inkomsten voor specifieke producten per campagne weer te geven
1. (Optioneel) [!UICONTROL Cost]: maak de `AdWords Cost` -metrische informatie zichtbaar om de kosten voor campagnes te zien

1. Geef uw rapport een naam en zorg ervoor het als lijst bewaart

**3. Herhaal stap 1 en 2 hierboven voor elk van uw geadverteerde producten of productgroep(en).**

## Gerelateerde documentatie

* [De verwijzingsbron van de orde van het spoor via  [!DNL Google Analytics]  E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](../analysis/track-usr-dev-browser.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../analysis/most-value-source-channel.md)
* [Verbind uw  [!DNL Google Adwords]  rekening](../importing-data/integrations/google-adwords.md)
* [Hoe werkt  [!DNL Google Analytics]  UTM attributie?](../analysis/utm-attributes.md)
* [Vijf beste praktijken voor het etiketteren UTM in  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
