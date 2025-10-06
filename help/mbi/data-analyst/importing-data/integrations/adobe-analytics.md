---
title: Connect Adobe Analytics
description: Leer om de nadruk van de klantenreis van begin tot eind van  [!DNL Adobe Analytics]  en de eCommerce samen te brengen u zich van  [!DNL Commerce Intelligence] baseert.
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Verbinden [!DNL Adobe Analytics]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![ het embleem van Adobe Analytics ](../../../assets/adobe-analytic-slogo.png)

Dankzij de [!DNL Adobe Analytics] integratie voor [!DNL Adobe Commerce Intelligence] kunt u de volledige aandacht van de klant voor de reis van [!DNL Adobe Analytics] en de eCommerce-focus die u van [!DNL Commerce Intelligence] vertrouwt, samenbrengen. Dit geeft je een volledig beeld van de algehele prestaties van je winkel.

Meer specifiek, verstrekt de [!DNL Adobe Analytics] integratie voor [!DNL Commerce Intelligence] functionaliteit voor verkopers beginnen hun [!DNL Adobe Commerce] en [!DNL Adobe Analytics] gegevensreeksen te combineren.

- Maak een verbinding van uw bestaande [!DNL Adobe Analytics] -account met [!DNL Commerce Intelligence] .

- Selecteer maximaal 25 metriek en afmetingen uit één rapportsuite om in uw Data Warehouse te repliceren.

- Gebruik alle standaardfuncties van [!DNL Commerce Intelligence] om gerepliceerde [!DNL Adobe Analytics] -gegevens te transformeren, samen te voegen en rapporteren.

## Verbindingsvoorwaarden

De volgende informatie is nodig om verbinding te maken:

- [!DNL Adobe Analytics] aanmeldingsgegevens

- `Name` en/of `ID` van [!DNL Adobe Analytics] rapportsuite om gegevens van te repliceren

- Lijst met metriek en dimensies die moeten worden gerepliceerd in [!DNL Commerce Intelligence]

## De [!DNL Adobe Analytics] integratie voor [!DNL Commerce Intelligence] verbinden

1. Ga naar de pagina `Integrations` onder **[!DNL Manage Data** > **Integrations]** .

1. Klik op **[!UICONTROL Add an Integration]**.

1. Klik op het pictogram **[!UICONTROL Adobe Analytics]** om de pagina te openen waarmee u de verbinding met uw [!DNL Adobe Analytics] -account kunt autoriseren.

1. Klik op **[!UICONTROL Authorize with Adobe Analytics]**.

1. Voer uw [!DNL Adobe Analytics] referenties in. Nadat de autorisatie is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence] .

1. Een lijst met beschikbare rapportsuites wordt weergegeven. Selecteer de rapportsuite waaruit u de gegevens wilt importeren en klik op **[!UICONTROL Continue]** .

1. Het selectiescherm voor maateenheden en afmetingen wordt weergegeven. Selecteer minstens één metrische en minstens één afmeting, tot een gecombineerd totaal van 25 metriek en afmetingen. Zoek op naam of rol om uw componenten te vinden, dan checkboxes te selecteren. Klik op **[!UICONTROL Continue]**.

1. De geselecteerde rapportsuite wordt in een tabel weergegeven. Klik op **[!UICONTROL Save]** om uw selectie te bevestigen.

1. Informeer het [!DNL Commerce Intelligence] [ team van de Steun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) dat uw integratie wordt gemachtigd, en zij stellen het aanvankelijke verbindingsproces voor u in werking.

Nadat het eerste verbindingsproces is gestart, is uw tabel beschikbaar op de Data Warehouse-pagina onder het tabblad `All Tables` . Selecteer de kolommen die u wilt repliceren en de gegevens worden weergegeven na de volgende volledige update.
