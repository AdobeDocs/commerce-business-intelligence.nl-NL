---
title: Connect-Googles Analytics gedraaid
description: Leer hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en meer.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Verbinden [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is de meest gebruikte webanalysedienst op internet. Implementatie [!DNL Google Analytics] op uw website kunt u bijhouden hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en nog veel meer. [!DNL Google Analytics Warehoused] is een afzonderlijke integratie van uw bestaande [!DNL Google Analytics] integratie. Het maakt een betere analyse mogelijk omdat het [!DNL Google Analytics] gegevens in uw Data Warehouse, die anders is dan de live feed van de bestaande [!DNL Google Analytics] integratie. Deze gegevens analyseren in [!DNL Commerce Intelligence], en andere gegevens, verbetert de algehele gezondheid en bruikbaarheid van uw site.

## Verschil tussen GA gehuisvest en Live integratie

De belangrijkste differentiator is dat één integratie wordt opgeslagen ([!DNL Google Analytics Warehoused]) en de andere is niet ([!DNL Google Analytics Live]). In het geval van [!DNL Google Analytics Warehoused]kunt u uw [!DNL Google Analytics] gegevens en biedt u de mogelijkheid [!DNL Google Analytics] en andere gegevensbronnen om inzichtelijke rapportage te maken.

Kijk naar [!DNL Google Analytics] advertentiecampagnes voor een voorbeeld van wat vanuit een manipulatiestandpunt kan worden gedaan. Stel dat u voor het vierde kwartaal meerdere advertentiecampagnes met verschillende namen hebt gehad. De campagnes waren het resultaat van een specifiek marketinginitiatief. Met opgeslagen gegevens, kunt u een kolom tot stand brengen die de campagnemenamen in kwestie vindt en de vierde kwartaalinitiatiefnaam van terugkeert `Operation Dumbo`.

Met het combinatieaspect [!DNL Google Analytics] gegevens die met het oog op de uitvoering van analyses aan andere gegevens moeten worden toegevoegd. Neem bijvoorbeeld `Total Time On Site By Ad Campaign` gegevens van [!DNL Google Analytics] en doe mee met `Total Spent Per Campaign` gegevens van [!DNL Facebook Ads] om een volledig beeld te krijgen van hoeveel betrokkenheid u kost.

Met de [!DNL Google Analytics Live] integratie daarentegen , elke [!DNL Google Analytics] grafiek is als een kleine silo die niet in uw Data Warehouse wordt opgeslagen.

## Verbinding maken [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] is een `Premium` Integratie. [Contact opnemen met ondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) als u er belang bij hebt deze integratie aan uw abonnement toe te voegen.

1. Ga naar de `Connections` pagina onder **[!UICONTROL Admin** > **Integrations]**.
1. Klikken **[!UICONTROL Add an Integration]** aan de rechterkant.
1. Klik op de knop [!DNL Google Analytics Warehoused] pictogram. Hierdoor wordt het [!DNL Google Analytics] pagina met referenties.
1. Voer uw [!DNL Google Analytics] referenties. Nadat het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence].
1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence]. Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u het dialoogvenster Meerdere verbindingen [!DNL Google Analytics] in de onderstaande sectie Profielen.

## Meerdere verbindingen maken [!DNL Google Analytics] profielen

U hebt mogelijk meerdere websites verbonden met één [!DNL Google Analytics] eigen rekening [!DNL Google Analytics] profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence]. Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

Om een bepaalde website te identificeren [!DNL Google Analytics] Profiel-id:

1. Aanmelden [!DNL Google Analytics]
1. Ga naar de specifieke website [!DNL Google Analytics] dashboard
1. Kijk naar de URL. De profiel-id komt overeen met de volgende acht nummers `p` aan het einde van de regel

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Verbinding verbreken [!DNL Google Analytics Warehoused] van [!DNL Commerce Intelligence] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [accountinstellingen](https://myaccount.google.com/intro) pagina.
1. Onder de `Security` en klik op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klikken **[!UICONTROL revoke access]** naast [!DNL Commerce Intelligence].

## Gerelateerde documentatie

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Verbinding maken [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Websiteactiviteiten en conversietarieven van klanten analyseren](../../analysis/web-act-cust-conversion.md)
* [Verzamelingsgegevens van gebruikers bijhouden met [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
