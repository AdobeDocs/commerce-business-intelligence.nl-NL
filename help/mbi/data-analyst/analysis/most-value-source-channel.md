---
title: Het identificeren van Uw Waardigste Marketingbronnen en Kanalen
description: Meer informatie over bepaalde rapporten die u kunt gebruiken om uw meest waardevolle marketingkanalen te ontdekken.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Succesvolle marketingbronnen identificeren

Je hebt je publiek onderzocht, je hebt je campagne gemaakt, je hebt geïnvesteerd in een paar marketingkanalen. Nu er enige tijd voorbij is, hoe presteren die kanalen? Welk kanaal heeft de meest nieuwe gebruikers gebracht? Welke bron heeft het meest aan uw totale opbrengst bijgedragen?

Met [!DNL Adobe Commerce Intelligence] kunt u uw omzet en gebruikers eenvoudig segmenteren via een verwijzingsbron, ongeacht of dit overeenkomt met [[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en) of aangepaste gegevensvelden. Dankzij deze segmentatie kunt u uw best presterende kanalen vinden en uw marketingbudget beter investeren.

In dit onderwerp worden enkele rapporten besproken die u kunt gebruiken om uw waardevolle marketingkanalen te ontdekken:

* [Nieuwe gebruikers op bronnen](#newusersbysource)
* [Gemiddelde levensopbrengst per gebruikersbron](#avglifetimerev)
* [Gemiddelde bestelwaarde per gebruikersbron](#avgorderval)
* [Ontvangsten per registratiedatum van de gebruiker en naar bronnen](#revbyregdateandsource)
* [Volgorde herhalen op gebruikersbron](#repeatordersbysource)

## Vereisten {#prereqs}

Om de analyses in dit onderwerp te bouwen, hebt u toegang tot marketing verwerving/verwijzingsbrongegevens nodig. Als u het niet reeds volgt, moet u [&#x200B; orde verwijzingsbrongegevens van  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) in [!DNL Adobe Commerce Intelligence] brengen alvorens u kunt verdergaan. Bovendien kunt u door apparaatgegevens aan uw analyses toe te voegen, zien welke technologie uw referenties gebruiken.

## Nieuwe gebruikers op bron {#newusersbysource}

Het beoordelen van de prestaties van verwijzingsbronnen is zeer belangrijk bij het bepalen van uw meest waardevolle kanalen. Dit rapport geeft het aantal nieuwe geregistreerde gebruikers in de loop der tijd weer, op basis van de aankoopbron, zodat u de prestaties van verwijzingsbronnen kunt bijhouden bij het aanschaffen van nieuwe geregistreerde gebruikers.

Om dit rapport in [&#x200B; Report Builder &#x200B;](../../tutorials/using-visual-report-builder.md) tot stand te brengen, voeg **Nieuwe gebruikers** metrisch toe (of gelijkwaardige metrisch die het aantal nieuwe gebruikers in tijd) aan het rapport telt. Voer vervolgens de volgende handelingen uit:

1. Stel de [!UICONTROL Time Period] in op de registratieperiode die u wilt analyseren.
1. Stel de [!UICONTROL Interval] in op maandelijks.
1. Stel [!UICONTROL Group By] in op verwervingsbron (of verwijzingsbron) en selecteer de bronnen die u wilt opnemen.
1. In dit voorbeeld wordt `stacked columns` [!UICONTROL chart type] gebruikt.

Hier is een visuele analyse:

![&#x200B; Creërend een Nieuwe gebruikers door bronrapport.](../../assets/New_Users_by_source.gif)

## Gemiddelde levensopbrengst per gebruikersbron {#avglifetimerev}

Het is belangrijk om de kanalen te vinden die nieuwe gebruikers introduceren, maar hoe waardevol zijn deze verwijzingen over het algemeen? Dit rapport toont de gemiddelde levensinkomsten van gebruikers uit specifieke aankoopbronnen in de loop van de tijd. Met andere woorden, staat dit u toe om te zien of de gebruikers die van een bepaalde bron worden verworven meer met u tijdens hun leven dan een groep gebruikers uitgeven die van een verschillende bron worden verworven.

Om dit rapport in Report Builder tot stand te brengen, voeg **Gemiddelde levenopbrengst** metrisch aan het rapport toe. Voer vervolgens de volgende handelingen uit:

1. Stel de [!UICONTROL Time Period] in op de tijdsperiode die u wilt analyseren.
1. Stel de [!UICONTROL Interval] in op maandelijks.
   [!UICONTROL Group By] aan verwervingsbron (of verwijzingsbron) en selecteer de bronnen die u wilt opnemen.
1. In dit voorbeeld wordt het type `line chart` gebruikt.

Hier is een visuele analyse:

![&#x200B; Creërend een Gemiddelde levenopbrengst door gebruikersbron &#x200B;](../../assets/Lifetime_revenue_by_user_source.gif).

In dit voorbeeld wordt alleen gekeken naar levenslange inkomsten, maar u kunt deze analyse ook repliceren om naar de [!UICONTROL Number of orders] - of [!UICONTROL Distinct buyers] -bron te kijken.

## Gemiddelde bestelwaarde per gebruikersbron {#avgorderval}

Om een beter idee te krijgen van hoeveel geld gebruikers van een specifieke aanschafbron uitgeven, kunt u een rapport bouwen dat hun Gemiddelde ordewaarde bekijkt. Hierdoor kunt u bijhouden of gebruikers die van een bepaalde bron zijn opgehaald, meer per bestelling uitgeven dan gebruikers van een andere bron.

Om dit rapport in Report Builder tot stand te brengen, voeg metrisch de **Gemiddelde ordewaarde** toe en doe dan het volgende:

1. Stel de [!UICONTROL Time Period] in op de registratieperiode die u wilt analyseren.
1. Stel de [!UICONTROL Time Interval] in op maandelijks.
1. Stel [!UICONTROL Group By] in op verwervingsbron (of verwijzingsbron) en selecteer de bronnen die u wilt opnemen.
1. Dit voorbeeld gebruikt het **gestapelde kolommen** grafiektype.

Hier is een visuele analyse:

![&#x200B; Creërend een Gemiddelde ordewaarde door gebruiker bronrapport.](../../assets/Average_order_value_by_source.gif)

## Totale inkomsten per registratiedatum en bron van de gebruiker {#revbyregdateandsource}

De analyse van de levenopbrengst die vroeger werd behandeld laat u de gemiddelde levenopbrengst van gebruikers bekijken die uit verschillende bronnen worden verworven, maar wat met totale levensinkomsten? Dit rapport staat u toe om te identificeren hoeveel algemene opbrengstgebruikers die tijdens een specifieke tijd en van een specifieke bron registreren produceren.

Als u dit rapport wilt maken in de Report Builder, voegt u de metrische waarde `Revenue by user registration date` toe. Als u niet [&#x200B; dit metrisch &#x200B;](../../data-user/reports/ess-manage-data-metrics.md) reeds hebt gecreeerd, kunt u dit doen door `Revenue` metrisch te herhalen en `time stamp` te veranderen in Gebruiker `creation date`. Voer de volgende handelingen uit nadat u de metrische waarde hebt toegevoegd:

1. Stel de [!UICONTROL Time Period] in op de registratieperiode die u wilt analyseren.
1. Stel de [!UICONTROL Time Interval] in op maandelijks.
1. Stel [!UICONTROL Group By] in op verwervingsbron (of verwijzingsbron) en selecteer de bronnen die u wilt opnemen.
1. In dit voorbeeld wordt het diagramtype `stacked columns` gebruikt.

Hier is een visuele analyse:

![&#x200B; Creërend een Totale opbrengst door de datum van de gebruikersregistratie &amp; bronrapport.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Volgorde herhalen op gebruikersbron {#repeatordersbysource}

Het gemiddelde rapport van de ordewaarde toont u, gemiddeld, hoeveel gebruikers die van een bepaalde bron worden verworven uitgeven wanneer het plaatsen van een orde. Dit rapport geeft echter niet aan of dezelfde gebruikers herhaalde klanten zijn. Maar met de Herhalingsorden door gebruikersbronnen, kunt u zien of maken de gebruikers van een bepaalde bron meer of minder herhaalde aankopen.

Om dit rapport in [&#x200B; Report Builder &#x200B;](../../tutorials/using-visual-report-builder.md) tot stand te brengen, voeg het **Aantal orden** metrisch toe en doe dan het volgende:

1. Stel de [!UICONTROL Time Period] in op de registratieperiode die u wilt analyseren.
1. Stel de [!UICONTROL Time Interval] in op maandelijks.
1. Voeg een [!UICONTROL filter] toe, zodat alleen gebruikers met herhaalde volgorden worden opgenomen:

   Volgnummer van gebruiker groter dan 1

1. Stel [!UICONTROL Group By] in op verwervingsbron (of verwijzingsbron) en selecteer de bronnen die u wilt opnemen.
1. In dit voorbeeld wordt het diagramtype `stacked columns` gebruikt.

Hier is een visuele analyse:

![&#x200B; Creërend een Herhalingsorden door gebruiker bronrapport.](../../assets/Repeat_orders_by_user_source.gif)


## Omloop omhoog {#wrapup}

In dit onderwerp werden slechts enkele analyses genoemd die je kunt gebruiken om de waarde van je aankoop- en marketingkanalen te analyseren, maar dit is slechts het topje van de ijsberg.

## Verwante {#related}

* [Referentiebron voor volgorde bijhouden via  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Het verbinden van uw  [!DNL Google Adwords]  rekening](../importing-data/integrations/google-adwords.md)
* [De bouw  [!DNL Google ECommerce]  dimensies met orden en klantengegevens](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Aanbevolen procedures voor UTM-codering in  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
