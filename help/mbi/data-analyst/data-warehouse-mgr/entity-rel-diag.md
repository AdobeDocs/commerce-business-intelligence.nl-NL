---
title: Relatiediagrammen voor entiteiten
description: Leer over een paar ER diagrammen om u te helpen de verhouding tussen een handvol gemeenschappelijke Commerce gegevensbestandlijsten visualiseren.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Relatiediagram voor entiteit

Wat is een **[!UICONTROL entity relationship (ER) diagram]** ? Een [!UICONTROL ER] -diagram is een visualisatie van tabellen in een database en hoe deze zich op elkaar verhouden. Dit onderwerp bevat een paar [!UICONTROL ER] diagrammen om u te helpen de verhouding tussen een paar gemeenschappelijke de gegevensbestandlijsten van Adobe Commerce visualiseren.

>[!NOTE]
>
>Door dit onderwerp, ziet u de woorden **toetreden**, **verhouding**, en **weg**. Deze woorden worden allen gebruikt om te beschrijven hoe twee lijsten worden verbonden.

## Core Commerce [!UICONTROL ER] Diagram

![&#x200B; 4_DB_Chart &#x200B;](../../assets/4_DB_Chart.png)

Dit `ER` diagram vertegenwoordigt de relaties tussen de kerntabellen in een Commerce-database. Door veelvoudige verhoudingen tegelijkertijd te bekijken, kunt u zien hoe de gegevens over vele lijsten zouden betrekking hebben.

De onderstaande secties bevatten `ER` diagrammen die specifiek zijn voor twee tabellen tegelijk. Als u een diagram en de bijbehorende beschrijving wilt weergeven, klikt u op de koptekst voor die sectie.

## `customer\_entity & sales\_flat\_order`

![&#x200B; Één Klant Vele Orden &#x200B;](../../assets/2_OneCustomerManyOrders.png)

Eén klant kan veel bestellingen plaatsen. De relatie tussen deze twee tabellen is `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` is niet gelijk aan `sales\_flat\_order.entity\_id` . Het eerste kan worden beschouwd als een `customer\_id` en het tweede als een `order\_id.`

Binnen [!DNL Commerce Intelligence], als de weg tussen deze twee lijsten niet bestaat, kunt u [&#x200B; de weg &#x200B;](../data-warehouse-mgr/create-paths-calc-columns.md) binnen het lusje van Data Warehouse tot stand brengen. Wanneer u klaar bent om het pad te maken, wordt het als volgt gedefinieerd:

![&#x200B; het relatiediagram dat van de Entiteit weg van sales_flat_order aan customer_entity &#x200B;](../../assets/SFO___CE_path.png) toont

## `sales\_flat\_order & sales\_flat\_order\_item`

![&#x200B; 1_OneOrderManyItems &#x200B;](../../assets/1_OneOrderManyItems.png)

Eén bestelling kan veel items bevatten. De relatie tussen deze twee tabellen is `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id` .

Binnen [!DNL Commerce Intelligence], als de weg tussen deze twee lijsten niet bestaat, kunt u [&#x200B; de weg &#x200B;](../data-warehouse-mgr/create-paths-calc-columns.md) in het lusje van Data Warehouse tot stand brengen. Wanneer u klaar bent om het pad te maken, definieert u het pad zoals hieronder wordt getoond.

![&#x200B; het relatiediagram dat van de Entiteit weg van sales_flat_order_item aan sales_flat_order &#x200B;](../../assets/SFOI___SFO_path.png) toont

## `catalog\_product\_entity & sales\_flat\_order\_item`

![&#x200B; 3_OneProductManyTimes &#x200B;](../../assets/3_OneProductManyTimes.png)

Eén product kan vele objecten aanschaffen. De relatie tussen deze twee tabellen is `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product` .

Binnen [!DNL Commerce Intelligence], als de weg tussen deze twee lijsten niet bestaat, kunt u [&#x200B; de weg &#x200B;](../data-warehouse-mgr/create-paths-calc-columns.md) binnen het lusje van Data Warehouse tot stand brengen. Wanneer u klaar bent om het pad te maken, definieert u het pad zoals hieronder wordt getoond.

![&#x200B; het relatiediagram dat van de Entiteit weg van sales_flat_order_item aan catalog_product_entiteit &#x200B;](../../assets/SFOI___CPE_path.png) toont
