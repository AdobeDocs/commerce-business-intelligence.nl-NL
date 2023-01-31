---
title: Verwacht[!DNL Google ECommerce]data
description: Leer welke soorten gegevens met de Handel van Google worden gedeeld.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Verwacht[!DNL Google ECommerce] data

Na uw [!DNL Google ECommerce] account is verbonden met [!DNL MBI]worden gegevens geïmporteerd in een tabel met de naam `ecommerce`. Deze lijst zal een gegevensrij voor elke transactie registreren. Dit omvat de volgende orde-vlakke gegevenskolommen:

| Kolomnaam | Beschrijving |
|-----|-----|
| `\_id` | Deze kolom is de primaire sleutel. |
| `accountId` | Deze kolom bevat de account-id die aan uw [!DNL Google Analytics] eCommerce-account. |
| `profileName` | Deze kolom bevat uw [!DNL Google Analytics] profielnaam. |
| `profileId` | Deze kolom bevat uw [!DNL Google Analytics] profiel-id. |
| `socialNetwork` | Deze kolom bevat de naam van het sociale netwerk (bijvoorbeeld [!DNL Facebook], of [!DNL YouTube]) |
| `campaign` | Deze kolom bevat de naam van de campagne (bijvoorbeeld [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Deze kolom bevat de naam van het medium (bijvoorbeeld [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Deze kolom bevat de bronnaam. (bijvoorbeeld [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Deze kolom bevat de trefwoordbeschrijving (bijvoorbeeld [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Deze kolom bevat de volgorde-id. Dit wordt gebruikt om de verwijzingsgegevens terug naar uw ordegegevens weer te geven. |
| `updated\_at` | Deze kolom bevat de laatste keer dat de gegevensrij is bijgewerkt. |

{style=&quot;table-layout:auto&quot;}
