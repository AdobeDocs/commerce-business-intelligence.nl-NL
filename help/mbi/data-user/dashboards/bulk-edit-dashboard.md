---
title: Grafieken voor bulkbewerking in dashboards
description: Leer hoe te om de bulk-uitgevende eigenschap in  [!DNL Commerce Intelligence] te gebruiken.
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 1%

---

# Bulkbewerkingsgrafieken in dashboards

Met de functie voor het bewerken van grote hoeveelheden kunt u heel gemakkelijk namen en datums van grafieken in uw dashboards wijzigen. U wilt bijvoorbeeld dat alle grafieken op een specifiek dashboard naar één winkel verwijzen en dat deze op maandbasis worden gerapporteerd in plaats van op kwartaalbasis. Laat de functie `bulk-editing` het werk doen in plaats van alles handmatig te wijzigen. In dit onderwerp leert u hoe u kunt gebruiken:

* [De  [!DNL Find/Replace]  Eigenschap](#findreplace)

* [De  [!DNL Prepend Name]  Eigenschap](#prepend)

* [De  [!DNL Change Dates]  Eigenschap](#dates)

Dit gezegd hebbende, bedenk dit - *moeten deze veranderingen permanent zijn?* Als dat niet het geval is, kunt u het dashboard klonen en vervolgens de datums in het nieuwe dashboard wijzigen. Zo kunt u het oorspronkelijke dashboard behouden en toch de gewenste wijzigingen aanbrengen.

>[!NOTE]
>
>Als u een groot aantal rapporten wijzigt, kan het bijwerken enige tijd duren.

## [!DNL Find/Replace] gebruiken {#findreplace}

1. Klik het tandwielpictogram (![ het pictogram van het Gear ](../../assets/gear-icon.png)) naast de naam van uw dashboard, toen het [!UICONTROL Bulk Edit Reports] venster.

1. Klik op **[!UICONTROL Chart Title Find and Replace]** in de pop-up.

1. Typ in het veld `Chart Title Find` de woorden of tekens die u wilt zoeken.

1. Typ in het veld `Replace With` de woorden of tekens die de tekst in het veld `Find` moeten vervangen.

1. Klik op **[!UICONTROL Update Reports]**.

Voorbeeld:

![ bulkgeef uit ](../../assets/bulk_edit.gif)

## Voorbehandeling `Chart Names` {#prepend}

1. Klik het tandwielpictogram (![ het pictogram van het Gear ](../../assets/gear-icon.png)) naast de naam van uw dashboard, toen het [!UICONTROL Bulk Edit Reports] venster.

1. Klik op **[!UICONTROL Prepend Report Names]** in de pop-up.

1. Typ de woorden of tekens die u aan uw diagrammen wilt toevoegen.

1. Klik op **[!UICONTROL Update Reports]**.

Voorbeeld:

![ prepend ](../../assets/prepend.gif)

## Wijzigen `Dates` {#dates}

1. Klik het tandwielpictogram (![ het pictogram van het Gear ](../../assets/gear-icon.png)) naast de naam van uw dashboard, dan selecteer het [!UICONTROL Bulk Edit Reports] venster.

1. Klik op **[!UICONTROL Change Dates]** in het pop-upvenster.

1. Stel de nieuwe `Start/End Date` en `Time Interval` in. U kunt deze velden ook ongewijzigd laten.

1. Klik op **[!UICONTROL Update Reports]**.

Voorbeeld:

![ veranderende data ](../../assets/dates.gif)
