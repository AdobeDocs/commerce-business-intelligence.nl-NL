---
title: Gegevensvalidatie in Mixpanel
description: Leer hoe u kunt bevestigen dat u alle gegevens hebt gesynchroniseerd die rechtstreeks beschikbaar zijn in het deelvenster Mixen.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Gegevensvalidatie in [!DNL Mixpanel]

Wanneer [!DNL Adobe Commerce Intelligence] voor het eerst verbinding maakt met uw [!DNL Mixpanel] -gegevens, kan uw accountmanager of analist u vragen om voor validatiedoeleinden gegevens te exporteren van [!DNL Mixpanel] . Zo kunt u bevestigen dat u alle gegevens hebt gesynchroniseerd die direct binnen [!DNL Mixpanel] beschikbaar zijn.

## Gegevensuitvoerproces: `Events`

1. Ga naar de `Segmentation` -sectie en bekijk `Your Top Events` .

   ![&#x200B; Mixpanel dashboard die uw hoogste gebeurtenissen tonen &#x200B;](../../../assets/your-top-events.png)

1. `Past 96 Hours` selecteren voor het tijdbereik

   ![&#x200B; de bereikselecteur van de het tijdwaaier van het Mixpanel die voorbij 96 uuroptie toont &#x200B;](../../../assets/past-96-hours.png)

1. Blader naar het gedeelte rechtsonder in het rapport en exporteer een `.csv` -bestand:

   ![&#x200B; de uitvoer van het Mixpanel naar optie CSV in menu &#x200B;](../../../assets/export-csv-mixpanel.png)

1. Verzend het `.csv` -bestand naar de accountmanager of analist waarmee u werkt aan dit validatieproces.
