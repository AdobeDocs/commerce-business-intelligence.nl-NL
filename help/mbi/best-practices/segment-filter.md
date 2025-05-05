---
title: Aanbevolen Dimensionen van Gegevens voor Segmentatie en Filtreren
description: Leer over beste praktijken voor segmentatie en het filtreren.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Segmentatie en filteren

Goede segmentatie is wat een oppervlakkige statistiek omzet in een zakelijke maatstaf die beslissingen drijft.

Wilt u weten wie uw meest waardevolle klanten zijn? Wat zijn uw waardevolste marketingkanalen? Welke producten bewegen sneller en waarom? Om aan om het even welk van deze antwoorden te krijgen, moet u beginnen door uw gegevens te segmenteren.

Dit onderwerp behandelt kritieke segmenten die vaak aan klanten worden geadviseerd. Het gaat ook in detail op welke vragen die deze segmenten u kunnen helpen beantwoorden. Technisch, zijn de segmenten gegevenskolommen in uw gegevensbestand. In [!DNL Adobe Commerce Intelligence] worden ze dimensies genoemd.

![](../../mbi/assets/mbi-critical-segments.png)


## Gebruikerssegmenten

Gebruikerssegmenten helpen u te begrijpen wie uw gebruikers zijn en hoe zij zich gedragen.

* **Leeftijd/Jaar van de Macht**: Hoe oud zijn uw gebruikers? Hoe oud zijn uw meest actieve gebruikers? Doorgaans is het zinvol de waarden in bereiken op te nemen voor een effectievere analyse.
* **Geslacht**: Doen de verschillende genders met uw website verschillend?
* **Adres**: Waar komen uw gebruikers uit? Moet u uw marketinginspanningen richten op een bepaalde regio? Hebben uw recente reclamecampagnes zoals verwacht in uw doelregio&#39;s uitgevoerd?
* **bron van de de acquisitie van de Klant** \: Weet u welk marketing kanaal uw gebruikers uit komen? Hebben ze op een advertentie geklikt of via zoekactie naar je gezocht? [ segmenterend uw gegevens door bron van de gebruikersaanwinst ](../data-analyst/analysis/google-track-user-acq.md) is de eerste stap in het optimaliseren van uw nieuwe klantenaanwinst. Stap twee is meer geld uit te geven in wat werkt en wat niet werkt te doden.
* **het apparaat van de Registratie**: Hebben de gebruikers geregistreerd via uw mobiele app of uw website? iOS of Android™? Is uw mobiele gebruikersbasis groot genoeg om meer bronnen toe te wijzen voor de ontwikkeling van uw mobiele product? Als u dit nog niet volgt, zie dit onderwerp [ over het volgen van gebruikersapparaat ](../data-analyst/analysis/track-usr-dev-browser.md).
* **die door** wordt bedoeld: Wie zijn uw belangrijkste beïnvloedingsfactoren? Hoeveel gebruikers werden rechtstreeks door anderen doorverwezen?
* **Industrie**: Als u zaken B2B bent, waarin de industrieën uw gebruikers werken? Welke handelsorganisaties zijn de moeite waard om zich bij te sluiten?
* **reacties van het Onderzoek**: Als u klantenonderzoeken uitvoert, gebruik de reacties als segmenten voor een dieper niveau van het profileren. U kunt vragen stellen die een aanvulling vormen op wat u al weet over uw gebruikers of uw instructies bevestigen.
* **Eerste ordebedrag en productcategorie**: Is er een correlatie tussen de eerste orde van een gebruiker en toekomstige aankooppatronen?

## Orders/gebeurtenissensegmenten

De orde en gebeurtenissegmenten helpen bij het analyseren van gebruikersgedrag en betrokkenheid in tijd.

* **[!UICONTROL Billing / Shipping Address]**: Waar komen de meeste bestellingen vandaan? Is er een verschil tussen facturerings en verzendadressen?
* **[!UICONTROL Status]**: Hoeveel van uw bestellingen zijn niet voltooid? Wat is de verhouding tussen lopende orders in de afgelopen zeven dagen?
* **[!UICONTROL Customer acquisition source]**: Voorbij het volgen van gegevens van de gebruikersverwerving op een gebruikersniveau, kunt u het op een orde of gebeurtenisniveau [&#128279;](../data-analyst/analysis/google-track-user-acq.md) ook  volgen. Een gebruiker die zich via één bron heeft geregistreerd, heeft mogelijk toegang tot uw site via andere bronnen.
* **[!UICONTROL Device]**: neemt het aantal mobiele bestellingen toe? Hoeveel van uw opbrengst wordt geproduceerd via mobiele aankopen? (Als u dit nog niet volgt, zie dit onderwerp [ over het volgen van de gegevens van het ordeapparaat ](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: Welke van uw afhandelingscentra genereert de meeste inkomsten? Als u het verschil tussen bestellingstijd en verzendtijd analyseert, welk afhandelingscentrum reageert het meest?
* **[!UICONTROL Delivery Carrier]**: Welke is de populairste vervoerder? Welke drager heeft het minste aantal teruggekeerde punten?
* **[!UICONTROL Discount / Coupon Codes]**: genereren uw promoties eigenlijk extra zaken? Hoeveel extra objecten hebben uw klanten gekocht naast het te koop aangeboden object? Hoe beïnvloeden coupons uw gemiddelde orderwaarde? Wat is je gemiddelde marge voor gedisconteerde versus niet-gedisconteerde objecten?
* **[!UICONTROL Satisfaction / Rating]**: Hoe tevreden zijn uw klanten met hun bestellingen? Zijn uw klanten waarschijnlijk zaken naar u verwijzen?

## Productsegmenten

De segmenten van het product helpen u handelsveranderende besluiten nemen.

* **[!UICONTROL Merchant / Brand]**: Verkoop één specifiek merk sneller dan de rest? Welke merken presteren ondermaats?
* **[!UICONTROL Type / Category]**: genieten verschillende gebruikerssegmenten van verschillende typen producten? Welke productcategorieën produceren de meest herhaalde zaken?
* **[!UICONTROL Discount / Coupon Codes]**: Leiden promoties nadelig uit voor de verkoop van producten zonder kortingen? Hoe beïnvloeden coupons de waargenomen waarde van uw producten?
* **[!UICONTROL Social Activity]**: Is er een correlatie tussen de zogenoemde &#39;buzz&#39; die op sociale media wordt gegenereerd en de hoeveelheid die voor een product wordt verkocht?
* **[!UICONTROL Size / Variant]**: Wat is de verhouding van inventaris die u van elke variant nodig hebt? Welke varianten kunnen tegen disconteringsvoeten worden verkocht?

Als u in handel geinteresseerd bent, controleer [ hoe te om productsegmenten te gebruiken om herhalingszaken ](../data-analyst/analysis/most-value-source-channel.md) te drijven.

## Klantprofielen maken

De deskundigen van de segmentatie kunnen zich voorbij eendimensionele plakken willen bewegen en beginnen het vestigen van echte klantenprofielen. Mensen tussen 13 en 24 jaar die zich bijvoorbeeld via een mobiel apparaat hebben geregistreerd, worden in een groep &quot;Jong en mobiel&quot; geplaatst. Hoe verhoudt het gedrag van deze groep zich tot de rest van uw gebruikersbasis?

Dit soort analyse doen marketeers van Fortune 1000 bedrijven de hele dag. Voor de komst van op cloud gebaseerde business intelligence platforms als [!DNL Commerce Intelligence] was het grotendeels onbereikbaar voor de rest van ons. Gelukkig is dat niet langer het geval.

## Nieuwe segmenten bijhouden

De eerste stap om uw metriek door de bovengenoemde afmetingen te segmenteren is ervoor te zorgen dat u deze gegevens in uw gegevensbestand volgt. Als de gegevens niet worden bijgehouden, neemt u contact op met uw technische team en zoekt u een manier om deze gegevens te volgen.

Nadat u bevestigt dat het gegeven in uw gegevensbestand wordt gevolgd, [ contacteer het steunteam ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om de afmetingen aan uw [!DNL Commerce Intelligence] metriek en grafieken te duwen. U kunt het *hulpmiddel van het Beheer van het Gebied* ook gebruiken om deze gebieden in [!DNL Commerce Intelligence] te volgen.

## Verwante

* [De database optimaliseren voor analyse](../best-practices/opt-db-analysis.md)
