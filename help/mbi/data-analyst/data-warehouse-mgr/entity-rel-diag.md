---
title: Relatiediagrammen voor entiteiten
description: Leer over een paar ER diagrammen om u te helpen de verhouding tussen een handvol gemeenschappelijke Commerce gegevensbestandlijsten visualiseren.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Relatiediagram voor entiteit

Wat is een **[!UICONTROL entity relationship (ER) diagram]** ? Een [!UICONTROL ER] -diagram is een visualisatie van tabellen in een database en hoe deze zich op elkaar verhouden. Dit onderwerp bevat een paar [!UICONTROL ER] diagrammen om u te helpen de verhouding tussen een paar gemeenschappelijke de gegevensbestandlijsten van Adobe Commerce visualiseren.

>[!NOTE]
>
>Door dit onderwerp, ziet u de woorden **toetreden**, **verhouding**, en **weg**. Deze woorden worden allen gebruikt om te beschrijven hoe twee lijsten worden verbonden.

## Core Commerce [!UICONTROL ER] Diagram

![ 4_DB_Chart ](../../assets/4_DB_Chart.png)

Dit `ER` diagram vertegenwoordigt de relaties tussen de kerntabellen in een Commerce-database. Door veelvoudige verhoudingen tegelijkertijd te bekijken, kunt u zien hoe de gegevens over vele lijsten zouden betrekking hebben.

De onderstaande secties bevatten `ER` diagrammen die specifiek zijn voor twee tabellen tegelijk. Als u een diagram en de bijbehorende beschrijving wilt weergeven, klikt u op de koptekst voor die sectie.

## `customer\_entity & sales\_flat\_order`

![ Één Klant Vele Orden ](../../assets/2_OneCustomerManyOrders.png)

Eén klant kan veel bestellingen plaatsen. De relatie tussen deze twee tabellen is `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` is niet gelijk aan `sales\_flat\_order.entity\_id` . Het eerste kan worden beschouwd als een `customer\_id` en het tweede als een `order\_id.`

Binnen [!DNL Commerce Intelligence], als de weg tussen deze twee lijsten niet bestaat, kunt u [ de weg ](../data-warehouse-mgr/create-paths-calc-columns.md) binnen de Data Warehouse tabel tot stand brengen. Wanneer u klaar bent om het pad te maken, wordt het als volgt gedefinieerd:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![ 1_OneOrderManyItems ](../../assets/1_OneOrderManyItems.png)

Eén bestelling kan veel items bevatten. De relatie tussen deze twee tabellen is `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id` .

Binnen [!DNL Commerce Intelligence], als de weg tussen deze twee lijsten niet bestaat, kunt u [ de weg ](../data-warehouse-mgr/create-paths-calc-columns.md) in de Data Warehouse tabel tot stand brengen. Wanneer u klaar bent om het pad te maken, definieert u het pad zoals hieronder wordt getoond.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![ 3_OneProductManyTimes ](../../assets/3_OneProductManyTimes.png)

Eén product kan vele objecten aanschaffen. De relatie tussen deze twee tabellen is `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product` .

Binnen [!DNL Commerce Intelligence], als de weg tussen deze twee lijsten niet bestaat, kunt u [ de weg ](../data-warehouse-mgr/create-paths-calc-columns.md) binnen de Data Warehouse tabel tot stand brengen. Wanneer u klaar bent om het pad te maken, definieert u het pad zoals hieronder wordt getoond.

![](../../assets/SFOI___CPE_path.png)
