---
title: Algemene Commerce-tabellen
description: Leer over enkele gemeenschappelijkere lijsten die  [!DNL Commerce Intelligence]  klanten gebruiken.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Algemene Commerce-tabellen

Wanneer u een [!DNL Adobe Commerce] -instantie voor het eerst verbindt met [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md) , worden in [!DNL Commerce Intelligence] automatisch gegevens uit sommige van uw handelstabellen (doorgaans 4-6 tabellen) overgenomen om de eerste set dashboards en rapporten te configureren. Hoewel dit een groot uitgangspunt aanbiedt, produceren de meeste opslaginstanties tientallen als niet honderden extra lijsten die kritiek inzicht in de prestaties van uw zaken kunnen verstrekken.

Hieronder vindt u een lijst met een aantal van de meer algemene tabellen die klanten van [!DNL Commerce Intelligence] gebruiken. Nadat u [ uw instantie van Commerce met Commerce Intelligence ](../../data-analyst/importing-data/integrations/magento.md) verbindt, kunt u de [ Manager van de Data Warehouse ](../../data-analyst/data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden te volgen.

| Tabelnaam | Beschrijving |
|---|---|
| `catalog_category_entity` | Elke rij in de tabel `catalog_category_entity` beschrijft een specifieke categorie. Met de bijbehorende `catalog_category_entity_varchar` tabel en de `catalog_category_product` toewijzingstabel kunt u voor elk product informatie over categorieën verkrijgen. |
| `catalog_category_product` | Elke rij in de tabel `catalog_category_product` bevat een combinatie van een product en een categorie. Daarom kan een bepaald product op deze lijst veelvoudige tijden met verschillende categorieën bestaan, en een bepaalde categorie kan op deze lijst bestaan veelvoudige tijden verbonden aan verschillende producten. Deze tabel indexeert de tabel `catalog_category_entity` (die details op categorieniveau bevat) en de tabel `catalog_product_entity` (die details op productniveau bevat). |
| `catalog_product_entity` | Elke rij in de tabel `catalog_product_entity` vertegenwoordigt een specifiek product. Dit geldt ook wanneer dat product is gemaakt in uw Commerce-account en de SKU van uw account. |
| `customer_entity` | Elke rij in de tabel [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) vertegenwoordigt een geregistreerde gebruiker op uw website. Belangrijke details op klantniveau, zoals de registratiedatum en het e-mailadres, worden in deze tabel weergegeven. |
| `quote` | Elke rij in de tabel [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) vertegenwoordigt een winkelwagentje dat tijdens het uitrekenen is gemaakt, ongeacht of die winkelwagentje uiteindelijk is omgezet in een bestelling. Vanwege de mogelijke grootte van deze tabel, raadt de Adobe u regelmatig aan om records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes zijn die ouder zijn dan 60 dagen. |
| `quote_item` | Elke rij in de tabel [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) vertegenwoordigt een item dat aan een winkelwagentje is toegevoegd, ongeacht of het winkelwagentje uiteindelijk is omgezet in een bestelling. Vanwege de mogelijke grootte van deze tabel, raadt de Adobe u regelmatig aan om records te verwijderen als aan bepaalde criteria wordt voldaan, bijvoorbeeld als er niet-omgezette winkelwagentjes zijn die ouder zijn dan 60 dagen. |
| `sales_order` | Elke rij in de tabel [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) vertegenwoordigt een volgorde die op uw site is geplaatst. Deze tabel bevat informatie op orderniveau, zoals de datum van de order, de klant die de order heeft geplaatst, het ordertotaal en het gebruik van kortingen- en couponcodes. |
| `sales_order_address` | Elke rij in de tabel `sales_order_address` bevat informatie over verzending en facturering voor een specifieke bestelling. In de tabel `sales_order` verwijzen de tekens `billing_address_id` en `shipping_address_id` voor een bepaalde volgorde naar een specifieke rij (bepaald door `entity_id` ) in de tabel `sales_order_address` . |
| `sales_order_item` | Elke rij in de tabel [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identificeert een specifiek item in een specifieke volgorde. Elke rij bevat gegevens zoals het product, de aangeschafte hoeveelheid en de volgorde waarin het item is gekoppeld. |

{style="table-layout:auto"}

## Gerelateerde documentatie

[Relatiediagrammen voor entiteiten](../data-warehouse-mgr/entity-rel-diag.md)
