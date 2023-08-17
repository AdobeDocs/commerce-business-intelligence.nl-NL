---
title: Grafieken voor bulkbewerking in dashboards
description: Leer hoe u de functie voor bulkbewerking kunt gebruiken in [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# Bulkbewerkingsgrafieken in dashboards

Met de functie voor het bewerken van grote hoeveelheden kunt u heel gemakkelijk namen en datums van grafieken in uw dashboards wijzigen. U wilt bijvoorbeeld dat alle grafieken op een specifiek dashboard naar één winkel verwijzen en dat deze op maandbasis worden gerapporteerd in plaats van op kwartaalbasis. In plaats van alles handmatig te wijzigen, kunt u `bulk-editing` doen het werk. In dit onderwerp leert u hoe u kunt gebruiken:

* [De [!DNL Find/Replace] Functie](#findreplace)

* [De [!DNL Prepend Name] Functie](#prepend)

* [De [!DNL Change Dates] Functie](#dates)

Dit gezegd hebbende, bedenk dit - *Moeten deze veranderingen permanent zijn?* Als dat niet het geval is, kunt u het dashboard klonen en vervolgens de datums in het nieuwe dashboard wijzigen. Zo kunt u het oorspronkelijke dashboard behouden en toch de gewenste wijzigingen aanbrengen.

>[!NOTE]
>
>Als u een groot aantal rapporten wijzigt, kan het bijwerken enige tijd duren.

## Gebruiken [!DNL Find/Replace] {#findreplace}

1. Klik op het gereedschap (![](../../assets/gear-icon.png)) naast de naam van het dashboard, gevolgd door de [!UICONTROL Bulk Edit Reports] venster.

1. Klikken **[!UICONTROL Chart Title Find and Replace]** in de popup.

1. In de `Chart Title Find` veld, typt u de woorden of tekens die u wilt zoeken.

1. In de `Replace With` veld, typt u de woorden of tekens die in de plaats moeten komen van `Find` veld.

1. Klik op **[!UICONTROL Update Reports]**.

Voorbeeld:

![bulkbewerking](../../assets/bulk_edit.gif)

## Voorbehandeling `Chart Names` {#prepend}

1. Klik op het gereedschap (![](../../assets/gear-icon.png)) naast de naam van het dashboard, gevolgd door de [!UICONTROL Bulk Edit Reports] venster.

1. Klikken **[!UICONTROL Prepend Report Names]** in de popup.

1. Typ de woorden of tekens die u aan uw diagrammen wilt toevoegen.

1. Klik op **[!UICONTROL Update Reports]**.

Voorbeeld:

![prepend](../../assets/prepend.gif)

## Wijzigen `Dates` {#dates}

1. Klik op het gereedschap (![](../../assets/gear-icon.png)) naast de naam van het dashboard, selecteert u vervolgens het pictogram [!UICONTROL Bulk Edit Reports] venster.

1. Klikken **[!UICONTROL Change Dates]** in het pop-upvenster.

1. Nieuwe instellen `Start/End Date` en `Time Interval`. U kunt deze velden ook ongewijzigd laten.

1. Klik op **[!UICONTROL Update Reports]**.

Voorbeeld:

![datums wijzigen](../../assets/dates.gif)
