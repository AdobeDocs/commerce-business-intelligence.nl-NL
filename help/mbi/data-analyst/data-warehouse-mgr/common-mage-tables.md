---
title: Gemeenschappelijke handelstabellen
description: Meer informatie over enkele meer algemene tabellen die [!DNL Commerce Intelligence] klanten gebruiken.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Gemeenschappelijke handelstabellen

Wanneer u voor het eerst een verbinding maakt [!DNL Adobe Commerce] instantie aan [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] herhaalt automatisch gegevens van sommige van uw handelstabellen (typisch 4-6 lijsten) om de aanvankelijke reeks dashboards en rapporten te vormen. Hoewel dit een groot uitgangspunt aanbiedt, produceren de meeste opslaginstanties tientallen als niet honderden extra lijsten die kritiek inzicht in de prestaties van uw zaken kunnen verstrekken.

Hieronder vindt u een lijst met enkele van de meer algemene tabellen die [!DNL Commerce Intelligence] klanten gebruiken. Na u [Verbind uw instantie van de Handel met de Intelligentie van de Handel](../../data-analyst/importing-data/integrations/magento.md), kunt u de [Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden bij te houden.

| Tabelnaam | Beschrijving |
|---|---|
| `catalog_category_entity` | Elke rij in de `catalog_category_entity` in de tabel wordt een specifieke categorie beschreven. Met de bijbehorende `catalog_category_entity_varchar` en de `catalog_category_product` Als u een tabel toewijst, kunt u voor elk product informatie over categorieën verkrijgen. |
| `catalog_category_product` | Elke rij in de `catalog_category_product` in de tabel wordt een combinatie van een product en een categorie weergegeven. Daarom kan een bepaald product op deze lijst veelvoudige tijden met verschillende categorieën bestaan, en een bepaalde categorie kan op deze lijst bestaan veelvoudige tijden verbonden aan verschillende producten. In deze tabel wordt de index van `catalog_category_entity` tabel (met gegevens op categorieniveau) en de `catalog_product_entity` tabel (die details op productniveau bevat). |
| `catalog_product_entity` | Elke rij in de `catalog_product_entity` tabel geeft een specifiek product aan. Dit omvat wanneer dat product in uw rekening van de Handel en zijn SKU werd gecreeerd. |
| `customer_entity` | Elke rij in de [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) tabel vertegenwoordigt een geregistreerde gebruiker op uw website. Belangrijke details op klantniveau, zoals de registratiedatum en het e-mailadres, worden in deze tabel weergegeven. |
| `quote` | Elke rij in de [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) de lijst vertegenwoordigt een karretje dat in het controleproces werd gecreeerd, of dat karretje uiteindelijk in een orde werd omgezet. Vanwege de mogelijke grootte van deze tabel, raadt de Adobe u regelmatig aan om records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes zijn die ouder zijn dan 60 dagen. |
| `quote_item` | Elke rij in de [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) in de tabel staat een item dat aan een winkelwagentje is toegevoegd, ongeacht of het karretje uiteindelijk in een bestelling is omgezet. Vanwege de mogelijke grootte van deze tabel, raadt de Adobe u regelmatig aan om records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes zijn die ouder zijn dan 60 dagen. |
| `sales_order` | Elke rij in de [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) tabel staat voor een volgorde die op uw site is geplaatst. Deze tabel bevat informatie op orderniveau, zoals de datum van de order, de klant die de order heeft geplaatst, het ordertotaal en het gebruik van kortingen- en couponcodes. |
| `sales_order_address` | Elke rij op de `sales_order_address` tabel bevat verzend- en factureringsgegevens voor een specifieke bestelling. Op de `sales_order` de `billing_address_id` en de `shipping_address_id` voor een bepaalde opdracht verwijzen naar een specifieke rij (aangeduid door `entity_id`) over de `sales_order_address` tabel. |
| `sales_order_item` | Elke rij in de [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) de lijst identificeert een specifiek punt van een specifieke orde. Elke rij bevat gegevens zoals het product, de aangeschafte hoeveelheid en de volgorde waarin het item is gekoppeld. |

{style="table-layout:auto"}

## Gerelateerde documentatie

[Relatiediagrammen voor entiteiten](../data-warehouse-mgr/entity-rel-diag.md)
