---
title: Commerce-gegevens verwacht
description: De belangrijkste gegevenstabellen die Commerce-gebruikers in Commerce Intelligence importeren, verkennen
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!DNL Adobe Commerce] gegevens verwacht

Nadat u [ uw  [!DNL Adobe Commerce]  opslag ](../../../data-analyst/importing-data/integrations/magento.md) hebt verbonden, kunt u de Manager van de Data Warehouse gebruiken om relevante gegevensgebieden van uw gegevensbestand van Commerce voor analyse gemakkelijk te volgen.

In dit onderwerp worden de belangrijkste gegevenstabellen besproken die Commerce-gebruikers in [!DNL Commerce Intelligence] importeren.

| **de naam van de Lijst** | **Beschrijving** |
|-----|-----|
| `Customers` | `customer\_entity` en verwante lijsten beschrijven de informatie verbonden aan elke *geregistreerde klant* in uw gegevensbestand, als hun e-mailadres en registratiedatum. Met deze informatie, kunt u beginnen segmenterend door klant-vlakke attributen en cohorts. |
| `Orders` | In de tabel `sales\_flat\_order` worden alle orders vastgelegd, inclusief de `created\_at` timestamp dat de order is geplaatst en het `base\_grand\_total` -veld waarin de inkomsten worden samengevat. Deze gebieden zijn de basis voor uw orde-vlakke metriek. Als de orde door a *geregistreerde klant* werd gemaakt, de `customer\_id` gebiedsverbindingen terug naar de `customer\_entity` lijst om analyse bij klant toe te staan die gedrag koopt. |
| `Order items` | In de tabel `sales\_flat\_order\_item` wordt elk item vastgelegd dat tot een bestelling behoort. Dit omvat de velden `price` en `qty\_ordered` en `order\_id` die verbinding maken met de tabel `sales\_flat\_order` . Deze tabel vormt de basis voor metriek zoals `Item sold` en maakt het mogelijk om te segmenteren op `product` en `product type` . |
| `Products` | In de tabel `catalog\_product\_entity` wordt informatie opgeslagen over kenmerken op productniveau, zoals categorie, grootte en kleur. |
| `Categories` | Uw producten horen bij een of meer verschillende `product categories` , afhankelijk van de manier waarop uw Commerce-build is ingesteld. In de tabel `catalog\_category\_entity` wordt de hiërarchie van deze categorieën opgeslagen (bijvoorbeeld Vastzetten > Tops > T-Shirts). In de tabel `catalog\_category\_product` worden de verbindingen tussen uw producten en deze categorieën vastgelegd. |

{style="table-layout:auto"}

## Verwante

* [Verbinding maken  [!DNL Adobe Commerce]](../integrations/magento.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
