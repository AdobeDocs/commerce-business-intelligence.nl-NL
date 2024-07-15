---
title: Connect-Googles Analytics gedraaid
description: Leer hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en meer.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Verbinden [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is de meest gebruikte service voor webanalyse op internet. Als u [!DNL Google Analytics] op uw website implementeert, kunt u bijhouden hoe bezoekers uw site gebruiken, welke inhoud aantrekkelijk is, waar bezoekers vertrekken en nog veel meer. [!DNL Google Analytics Warehoused] is een afzonderlijke integratie van uw bestaande [!DNL Google Analytics] -integratie. Hierdoor is een betere analyse mogelijk omdat de [!DNL Google Analytics] -gegevens in uw Data Warehouse staan. Dit verschilt van de live feed van de bestaande [!DNL Google Analytics] -integratie. Als u deze gegevens in [!DNL Commerce Intelligence] analyseert, worden de algemene gezondheid en bruikbaarheid van uw site verbeterd, samen met andere gegevens.

## Verschil tussen GA gehuisvest en Live integratie

Het belangrijkste differentiator is dat één integratie wordt opgeslagen ([!DNL Google Analytics Warehoused]), en andere is niet ([!DNL Google Analytics Live]). In het geval van [!DNL Google Analytics Warehoused] kunt u hiermee uw [!DNL Google Analytics] -gegevens bewerken en kunt u [!DNL Google Analytics] en andere gegevensbronnen combineren om een inzichtelijke rapportage te maken.

Bekijk [!DNL Google Analytics] advertentiecampagnes voor een voorbeeld van wat van een manipulatiestandpunt kan worden gedaan. Stel dat u voor het vierde kwartaal meerdere advertentiecampagnes met verschillende namen hebt gehad. De campagnes waren het resultaat van een specifiek marketinginitiatief. Met opgeslagen gegevens, kunt u een kolom tot stand brengen die de campagnemenamen in kwestie vindt en de vierde kwartaalinitiatiefnaam van `Operation Dumbo` terugkeert.

Met het combinatieaspect kunnen [!DNL Google Analytics] -gegevens worden gekoppeld aan andere gegevens om analyses uit te voeren. Neem bijvoorbeeld `Total Time On Site By Ad Campaign` gegevens van [!DNL Google Analytics] en voeg deze samen met `Total Spent Per Campaign` gegevens van [!DNL Facebook Ads] om een volledig beeld te krijgen van hoeveel betrokkenheid u kost.

Met de [!DNL Google Analytics Live] -integratie aan de andere kant is elke [!DNL Google Analytics] -grafiek een soort kleine silo die niet in uw Data Warehouse is opgeslagen.

## Verbinding maken [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] is een `Premium` Integratie. [ de steun van het Contact ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) als u een belang in het toevoegen van deze integratie aan uw abonnement hebt.

1. Ga naar de pagina `Connections` onder **[!UICONTROL Admin** > **Integrations]** .
1. Klik op **[!UICONTROL Add an Integration]** aan de rechterkant.
1. Klik op het pictogram [!DNL Google Analytics Warehoused] . Hierdoor wordt de aanmeldingspagina van [!DNL Google Analytics] geopend.
1. Voer uw [!DNL Google Analytics] referenties in. Nadat het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence] .
1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence] . Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de sectie Meerdere [!DNL Google Analytics] profielen verbinden hieronder.

## Meerdere [!DNL Google Analytics] -profielen verbinden

U kunt meerdere websites hebben die zijn verbonden met één [!DNL Google Analytics] -account, geïdentificeerd door hun eigen [!DNL Google Analytics] -profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence] . Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

De profiel-id [!DNL Google Analytics] van een bepaalde website identificeren:

1. Aanmelden bij [!DNL Google Analytics]
1. Naar het [!DNL Google Analytics] dashboard van de specifieke website gaan
1. Kijk naar de URL. De profiel-id komt overeen met de acht nummers na `p` aan het einde van de regel

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics Warehoused] loskoppelen van [!DNL Commerce Intelligence] {#disconnect}

1. Bezoek uw [!DNL Google Analytics] [ pagina van de rekeningsmontages ](https://myaccount.google.com/intro).
1. Klik onder de sectie `Security` op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klik op **[!UICONTROL revoke access]** naast [!DNL Commerce Intelligence] .

## Gerelateerde documentatie

* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Verbinding maken  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Websiteactiviteiten en conversietarieven van klanten analyseren](../../analysis/web-act-cust-conversion.md)
* [De gegevens van de gebruikersverwerving van het spoor gebruikend  [!DNL Google Analytics]  koekjes](../../analysis/google-track-user-acq.md)
