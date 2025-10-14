---
title: Google Analytics-diagrammen maken
description: Leer hoe u grafieken maakt op basis van uw Google Analytics-gegevens.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# [!DNL Google Analytics] grafieken maken

(met regex syntaxis help)

Nadat u uw [[!DNL Google Analytics]  rekening &#x200B;](../../data-analyst/importing-data/integrations/google-analytics.md) hebt verbonden, kunt u grafieken met uw [!DNL Google Analytics] gegevens tot stand brengen.

## [!DNL Google Analytics] Grafieken maken

1. Klik op **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Wanneer u een metrische waarde selecteert in de `Chart Builder` , bladert u naar de onderkant van de lijst om een sectie te zoeken met uw [!DNL Google Analytics] -profielen. Er wordt een tweede metrische vervolgkeuzelijst weergegeven. Hier kunt u de metrische waarde kiezen die u wilt analyseren.

1. Nadat u metrisch hebt gekozen, kunt u met dit diagram te werk gaan alsof het om een andere grafiek door `time period`, `interval`, en gegevens `perspectives` te selecteren die u zou willen zien.

1. Het enige grote verschil is dat `√` reguliere expressies voor filters gebruikt. Een reguliere expressie (regex for short) is een speciale tekstreeks die een zoekpatroon beschrijft. Zie voorbeelden van regex syntaxis in de [[!DNL Google]  gids over Regelmatige Uitdrukkingen van Analytics &#x200B;](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>De enige speciale tekens die met het teken \ moeten worden beschermd, zijn de onderstaande metatekens:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
