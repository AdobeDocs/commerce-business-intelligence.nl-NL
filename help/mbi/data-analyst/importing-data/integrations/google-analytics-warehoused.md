---
title: Connect Google Analytics gehuisvest
description: Leer hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en meer.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Verbinden [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is de meest gebruikte webanalysedienst op internet. Implementatie [!DNL Google Analytics] op uw website kunt u bijhouden hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en nog veel meer. [!DNL Google Analytics Warehoused] is een afzonderlijke integratie van onze bestaande [!DNL Google Analytics] integratie. Het zal een betere analyse mogelijk maken omdat het [!DNL Google Analytics] gegevens in uw Data Warehouse, die anders is dan de live feed van de bestaande [!DNL Google Analytics] integratie. Deze gegevens analyseren in [!DNL MBI], naast andere gegevens, zal de algemene gezondheid en bruikbaarheid van uw site verbeteren.

## Verschil tussen GA gehuisvest en Levende Integratie

De belangrijkste differentiator is dat één integratie wordt opgeslagen ([!DNL Google Analytics Warehoused]) en de andere is niet ([!DNL Google Analytics Live]). In het geval van [!DNL Google Analytics Warehoused]kunt u uw [!DNL Google Analytics] gegevens en biedt u de mogelijkheid om [!DNL Google Analytics] en andere gegevensbronnen om inzichtelijke rapportage te maken.

Laten we eens kijken naar [!DNL Google Analytics] advertentiecampagnes voor een voorbeeld van wat vanuit een manipulatiestandpunt kan worden gedaan. Stel dat u meerdere advertentiecampagnes voor Q4 met verschillende namen had. De campagnes waren het resultaat van een specifiek marketinginitiatief. Met gekapte gegevens, kunnen wij een nieuwe kolom tot stand brengen die de campagnemenamen in kwestie vindt en Q4 initiatiefnaam van terugkeert `Operation Dumbo`.

Met het combinatieaspect [!DNL Google Analytics] gegevens die met het oog op de uitvoering van analyses aan andere gegevens moeten worden toegevoegd. Neem bijvoorbeeld `Total Time On Site By Ad Campaign` gegevens van [!DNL Google Analytics] en doe mee `Total Spent Per Campaign` gegevens van [!DNL Facebook Ads] om een volledig beeld te krijgen van hoeveel betrokkenheid u kost.

Met de [!DNL Google Analytics Live] integratie daarentegen , elke [!DNL Google Analytics] diagram is als een kleine silo die niet is opgeslagen in uw [!DNL MBI] data-entrepot.

## Verbinding maken [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] is een `Premium` Integratie. [Contact opnemen met ondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) als u er belang bij hebt deze integratie aan uw abonnement toe te voegen.

1. Ga naar de `Connections` pagina onder **[!UICONTROL Admin** > **Integrations]**.
1. Klikken **[!UICONTROL Add a Add Integration]**, die zich aan de rechterkant van het scherm bevindt.
1. Klik op de knop [!DNL Google Analytics Warehoused] pictogram. Hierdoor wordt de [!DNL Google Analytics] aanmeldingspagina.
1. Voer uw [!DNL Google Analytics] referenties. Als het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL MBI].
1. Er wordt een lijst met profiel-id&#39;s weergegeven. Controleer de profielen waarmee u verbinding wilt maken [!DNL MBI]. Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u het dialoogvenster Meerdere verbindingen [!DNL Google Analytics] in de onderstaande sectie Profielen.

## Meerdere verbindingen maken [!DNL Google Analytics] profielen

U hebt mogelijk meerdere websites verbonden met één [!DNL Google Analytics] eigen rekening [!DNL Google Analytics] profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL MBI]. Controleer gewoon de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

Om een bepaalde website te identificeren [!DNL Google Analytics] Profiel-id:

1. Aanmelden [!DNL Google Analytics]
1. Ga naar de specifieke website [!DNL Google Analytics] dashboard
1. Kijk naar de URL. De profiel-id komt overeen met de volgende 8 nummers `p` aan het einde van de regel

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Verbinding verbreken [!DNL Google Analytics Warehoused] van [!DNL MBI] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [accountinstellingen](https://www.google.com/accounts/) pagina.
1. Onder de `Security` en klik op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klikken **[!UICONTROL revoke access]** naast [!DNL MBI].

## Gerelateerde documentatie

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Verbinding maken [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Websiteactiviteiten en conversietarieven van klanten analyseren](../../analysis/web-act-cust-conversion.md)
* [Verzamelingsgegevens van gebruikers bijhouden met [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
