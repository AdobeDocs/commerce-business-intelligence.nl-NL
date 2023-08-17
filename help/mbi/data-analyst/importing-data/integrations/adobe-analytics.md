---
title: Connect Adobe Analytics
description: Leer om de de reisnadruk van de klant van begin tot eind samen te brengen van [!DNL Adobe Analytics] en de eCommerce-focus waarop u vertrouwt [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Verbinden [!DNL Adobe Analytics]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

De [!DNL Adobe Analytics] integratie voor [!DNL Adobe Commerce Intelligence] laat u toe om de nadruk van de klantenreis van begin tot eind samen te brengen van [!DNL Adobe Analytics] en de eCommerce-focus waarop u vertrouwt [!DNL Commerce Intelligence]. Dit geeft je een volledig beeld van de algehele prestaties van je winkel.

Meer in het bijzonder [!DNL Adobe Analytics] integratie voor [!DNL Commerce Intelligence] verstrekt functionaliteit voor verkopers beginnen hun te combineren [!DNL Adobe Commerce] en [!DNL Adobe Analytics] gegevenssets.

- Een verbinding maken op basis van uw bestaande [!DNL Adobe Analytics] account [!DNL Commerce Intelligence].

- Selecteer maximaal 25 metriek en afmetingen van één rapportreeks aan replicatie in uw Data Warehouse.

- Alle standaard gebruiken [!DNL Commerce Intelligence] functionaliteit om te transformeren, zich aan te sluiten bij, en rapport over gerepliceerde [!DNL Adobe Analytics] gegevens.

## Verbindingsvoorwaarden

De volgende informatie is nodig om verbinding te maken:

- [!DNL Adobe Analytics] aanmeldingsgegevens

- `Name` en/of `ID` van [!DNL Adobe Analytics] rapportsuite om gegevens te repliceren van

- Lijst met metriek en dimensies die moeten worden gerepliceerd [!DNL Commerce Intelligence]

## De [!DNL Adobe Analytics] Integratie voor [!DNL Commerce Intelligence]

1. Ga naar de `Integrations` pagina onder **[!DNL Manage Data** > **Integrations]**.

1. Klik op **[!UICONTROL Add an Integration]**.

1. Klik op de knop **[!UICONTROL Adobe Analytics]** pictogram voor toegang tot de pagina waarmee u toestemming kunt geven voor [!DNL Adobe Analytics] accountverbinding.

1. Klik op **[!UICONTROL Authorize with Adobe Analytics]**.

1. Voer uw [!DNL Adobe Analytics] referenties. Nadat de autorisatie is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence].

1. Een lijst met beschikbare rapportsuites wordt weergegeven. Selecteer de rapportsuite waaruit u de gegevens wilt importeren en klik op **[!UICONTROL Continue]**.

1. Het selectiescherm voor maateenheden en afmetingen wordt weergegeven. Selecteer minstens één metrische en minstens één afmeting, tot een gecombineerd totaal van 25 metriek en afmetingen. Zoek op naam of rol om uw componenten te vinden, dan checkboxes te selecteren. Klik op **[!UICONTROL Continue]**.

1. De geselecteerde rapportsuite wordt in een tabel weergegeven. Klikken **[!UICONTROL Save]** om uw selectie te bevestigen.

1. De [!DNL Commerce Intelligence] [Ondersteuningsteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) dat uw integratie is geautoriseerd en dat deze het eerste verbindingsproces voor u uitvoert.

Nadat het eerste verbindingsproces is uitgevoerd, is uw tabel beschikbaar op de pagina Data Warehouse onder de `All Tables` tab. Selecteer de kolommen die u wilt repliceren en de gegevens worden weergegeven na de volgende volledige update.
