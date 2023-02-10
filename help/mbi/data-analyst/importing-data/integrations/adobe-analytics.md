---
title: Connect Adobe Analytics
description: Leer om de de reisnadruk van de klant van begin tot eind samen te brengen van [!DNL Adobe Analytics] en de eCommerce-focus waarop u vertrouwt [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Verbinden [!DNL Adobe Analytics]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

De [!DNL Adobe Analytics] integratie voor [!DNL MBI] laat u toe om de nadruk van de klantenreis van begin tot eind samen te brengen van [!DNL Adobe Analytics] en de eCommerce-focus waarop u vertrouwt [!DNL MBI], voor een vollediger beeld van de algemene prestaties van je winkel.

Meer in het bijzonder [!DNL Adobe Analytics] integratie voor [!DNL MBI] verstrekt functionaliteit voor verkopers beginnen hun de gegevensreeksen van de Handel en van de Analyse te combineren.
- Een verbinding maken op basis van uw bestaande [!DNL Adobe Analytics] account [!DNL MBI].
- Selecteer maximaal 25 metriek en dimensies van één rapportsuite om in uw [!DNL MBI] data-entrepot.
- Alle standaard gebruiken [!DNL MBI] functionaliteit om te transformeren, zich aan te sluiten bij, en rapport over gerepliceerde [!DNL Adobe Analytics] gegevens.

## Verbindingsvoorwaarden

De volgende informatie is nodig om verbinding te maken:
- [!DNL Adobe Analytics] aanmeldingsgegevens
- `Name` en/of `ID` van [!DNL Adobe Analytics] rapportsuite om gegevens te repliceren van
- Lijst met metriek en dimensies die moeten worden gerepliceerd [!DNL MBI]

## De [!DNL Adobe Analytics] Integratie met MBI

1. Ga naar de `Integrations` pagina onder **[!DNL Manage Data** > **Integrations]**.
1. Klikken **[!UICONTROL Add an Integration]**, die zich aan de rechterkant van het scherm bevindt.
1. Klik op de knop **[!UICONTROL Adobe Analytics]** pictogram voor toegang tot de pagina waarmee u toestemming kunt geven voor [!DNL Adobe Analytics] accountverbinding.
1. Klikken **[!UICONTROL Authorize with Adobe Analytics]**.
1. Voer uw [!DNL Adobe Analytics] referenties. Nadat de autorisatie is voltooid, wordt u teruggeleid naar [!DNL MBI].
1. Een lijst met beschikbare rapportsuites wordt weergegeven. Selecteer de rapportsuite waaruit u de gegevens wilt importeren en klik op **[!UICONTROL Continue]**.
1. Het selectiescherm voor maateenheden en afmetingen wordt weergegeven. Selecteer minstens één metrische en minstens één afmeting, tot een gecombineerd totaal van 25 metriek en afmetingen. Zoek op naam of rol om uw componenten te vinden, dan checkboxes te selecteren. Klikken **[!UICONTROL Continue]**.
1. De geselecteerde rapportsuite wordt in een tabel weergegeven. Klikken **[!UICONTROL Save]** om uw selectie te bevestigen.
1. De [!DNL MBI] Ondersteuningsteam dat uw integratie is geautoriseerd en dat deze het initiële verbindingsproces voor u uitvoeren.

Nadat het eerste verbindingsproces is uitgevoerd, is uw tabel beschikbaar op de pagina Data Warehouse onder de `All Tables` tab. Selecteer de kolommen die u wilt repliceren en de gegevens worden weergegeven na de volgende volledige update.
