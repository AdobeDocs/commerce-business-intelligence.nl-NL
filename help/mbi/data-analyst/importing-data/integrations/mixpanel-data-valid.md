---
title: Gegevensvalidatie in Mixpanel
description: Leer hoe u kunt bevestigen dat u alle gegevens hebt gesynchroniseerd die rechtstreeks beschikbaar zijn in het deelvenster Mixen.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Gegevensvalidatie in [!DNL Mixpanel]

Wanneer [!DNL Adobe Commerce Intelligence] maakt eerst verbinding met uw [!DNL Mixpanel] gegevens, kan uw accountmanager of analist u vragen gegevens te exporteren van [!DNL Mixpanel] voor validatiedoeleinden. Zo kunt u bevestigen dat u alle gegevens hebt gesynchroniseerd die direct binnen beschikbaar zijn [!DNL Mixpanel].

## Gegevensuitvoerproces: `Events`

1. Bezoek uw `Segmentation` sectie en weergave `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Selecteren `Past 96 Hours` voor het tijdbereik

   ![](../../../assets/past-96-hours.png)

1. De rol aan het laag-juiste gedeelte van het rapport en voert a uit `.csv` bestand:

   ![](../../../assets/export-csv-mixpanel.png)

1. Verzend de `.csv` bestand naar de accountmanager of -analist waarmee u werkt aan dit validatieproces.
