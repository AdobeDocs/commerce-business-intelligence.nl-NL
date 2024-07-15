---
title: Verwachte [!DNL Google ECommerce] gegevens
description: Leer welke soorten gegevens met de Handel van Google worden gedeeld.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# [!DNL Google ECommerce] gegevens verwacht

Nadat uw [!DNL Google ECommerce] -account is verbonden met [!DNL Commerce Intelligence] , begint het systeem met het importeren van gegevens naar een tabel met de naam `ecommerce` . Deze lijst registreert een gegevensrij voor elke transactie. Dit omvat de volgende orde-vlakke gegevenskolommen:

| Kolomnaam | Beschrijving |
|-----|-----|
| `\_id` | Deze kolom is de primaire sleutel. |
| `accountId` | Deze kolom bevat de account-id die is gekoppeld aan uw [!DNL Google Analytics] eCommerce-account. |
| `profileName` | Deze kolom bevat uw [!DNL Google Analytics] -profielnaam. |
| `profileId` | Deze kolom bevat uw [!DNL Google Analytics] profiel-id. |
| `socialNetwork` | Deze kolom bevat de naam van het sociale netwerk (bijvoorbeeld [!DNL Facebook] of [!DNL YouTube] ) |
| `campaign` | Deze kolom bevat de campagnenaam (bijvoorbeeld, [`utm\_campaign` ](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Deze kolom bevat de gemiddelde naam (bijvoorbeeld, [`utm\_medium` ](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Deze kolom bevat de bronnaam. (bijvoorbeeld, [`utm\_source` ](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Deze kolom bevat de sleutelwoordbeschrijving (bijvoorbeeld, [`utm\_term` ](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Deze kolom bevat de volgorde-id. Dit wordt gebruikt om zich bij de verwijzingsgegevens terug naar uw ordegegevens aan te sluiten. |
| `updated\_at` | Deze kolom bevat de laatste keer dat de gegevensrij is bijgewerkt. |

{style="table-layout:auto"}
