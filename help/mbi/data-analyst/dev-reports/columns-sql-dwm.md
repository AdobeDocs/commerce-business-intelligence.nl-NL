---
title: Verschillen tussen SQL en de Manager van de Data Warehouse
description: Leer de verschillen tussen SQL en de Manager van de Data Warehouse.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Verschillen tussen [!DNL SQL] en [!DNL Data Warehouse Manager]

Er zijn twee belangrijke verschillen tussen kolommen die zijn gemaakt in het dialoogvenster [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) en die zijn gemaakt met de [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). De ene is afhankelijk van updatecycli en de andere is hoe kolommen worden opgeslagen in uw account.

## Kolommen in de [!DNL SQL Report Builder]

Kolommen zijn niet afhankelijk van updatecycli. U hoeft dus niet langer te wachten tot de kolommen zijn voltooid voordat u de kolom kunt doorlopen. Als u een fout maakt, hebt u slechts enkele toetsaanslagen nodig om deze te corrigeren. Er wordt niet meer gewacht tot twee updates zijn voltooid voordat u weer aan de slag kunt.

>[!IMPORTANT]
>
>De kolommen die u maakt met de [!DNL SQL] de editor wordt niet opgeslagen naar de Data Warehouse. U hebt altijd toegang tot de vraag die de kolom bevat, maar als u de kolom in meer dan één rapport wilt gebruiken, moet u het in de vraag voor elk rapport opnieuw creëren. Dit betekent dat kolommen zijn gemaakt met de [!DNL SQL] editor kan niet worden gebruikt in de traditionele [!DNL Report Builder].

## Kolommen in het Manager van de Data Warehouse

Kolommen zijn afhankelijk van updatecycli, dus een volledige cyclus moet zijn voltooid voordat ze kunnen worden bewerkt. Deze kolommen worden bewaard aan de Manager van de Data Warehouse en kunnen in traditionele worden gebruikt [!DNL Report Builder] of [!DNL SQL Report Builder].
