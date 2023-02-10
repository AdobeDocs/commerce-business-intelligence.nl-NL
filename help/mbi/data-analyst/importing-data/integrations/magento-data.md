---
title: Verwachte handelsgegevens
description: Onderzoek de belangrijkste gegevenslijsten die de gebruikers van de Handel in MBI invoeren
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Verwachte handelsgegevens

Nadat u [heeft de winkel Commerce aangesloten](../../../data-analyst/importing-data/integrations/magento.md), kunt u de Manager van de Data Warehouse gebruiken om relevante gegevensgebieden van uw gegevensbestand van de Handel voor analyse gemakkelijk te volgen.

In dit artikel onderzoeken wij de belangrijkste gegevenslijsten die de gebruikers van de Handel in invoeren [!DNL MBI].

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| `Customers` | De `customer\_entity` en verwante tabellen bevatten informatie over de *geregistreerde klant* in uw database, zoals hun e-mailadres en registratiedatum. Met deze informatie, kunt u beginnen segmenterend door klant-vlakke attributen en cohorts. |
| `Orders` | De `sales\_flat\_order` in de tabel worden alle orders vastgelegd, inclusief de `created\_at` tijdstempel dat de order is geplaatst en `base\_grand\_total` veld waarin de inkomsten worden samengevat. Deze gebieden zullen de basis voor uw orde-vlakke metriek zijn. Indien de beschikking is gegeven door een *geregistreerde klant* de `customer\_id` veld wordt gekoppeld aan  `customer\_entity` tabel voor analyse van het aankoopgedrag van klanten. |
| `Order items` | De `sales\_flat\_order\_item` in de tabel wordt elk item vastgelegd dat tot een bestelling behoort. Dit omvat ook de `price` en `qty\_ordered` en de `order\_id` veld dat verbinding maakt met het `sales\_flat\_order` tabel. Deze tabel vormt de basis voor metriek zoals `Item sold`en kunt u segmenteren op `product` en `product type`. |
| `Products` | De `catalog\_product\_entity` de lijst slaat informatie over product-vlakke attributen, zoals categorie, grootte, en kleur op. |
| `Categories` | Uw producten behoren tot een of meerdere verschillende `product categories`, afhankelijk van de manier waarop de Handel is ingesteld. De `catalog\_category\_entity` in de tabel wordt de hiërarchie van deze categorieën (bijvoorbeeld Venster > Tops > T-Shirts) en de `catalog\_category\_product` de lijst registreert de verbindingen tussen uw producten en die categorieën. |

{style=&quot;table-layout:auto&quot;}

## Verwante

* [Verbinding maken [!DNL Adobe Commerce]](../integrations/magento.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
