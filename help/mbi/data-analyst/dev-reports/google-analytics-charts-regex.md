---
title: Grafieken Googles Analytics maken
description: Leer hoe u grafieken maakt op basis van de gegevens van uw Googles Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Maken [!DNL Google Analytics] grafieken

(met regex syntaxis help)

Nadat u verbinding hebt gemaakt met uw [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md)kunt u grafieken maken met uw [!DNL Google Analytics] gegevens.

## Maken [!DNL Google Analytics] Grafieken

1. Klik op **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Wanneer u een metrische waarde selecteert in het dialoogvenster `Chart Builder`, scrol aan de bodem van de lijst om een sectie met inbegrip van uw [!DNL Google Analytics] Profielen. Er wordt een tweede metrische vervolgkeuzelijst weergegeven. Hier kunt u de metrische waarde kiezen die u wilt analyseren.

1. Nadat u metrisch hebt gekozen, kunt u met deze grafiek te werk gaan alsof het om een andere grafiek door te selecteren was `time period`, `interval`en gegevens `perspectives` die u graag wilt zien.

1. Het enige grote verschil is dat: `√` gebruikt reguliere expressies voor filters. Een reguliere expressie (regex for short) is een speciale tekstreeks die een zoekpatroon beschrijft. Zie voorbeelden van regex syntaxis in [[!DNL Google] handleiding over reguliere analytische expressies](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>De enige speciale tekens die met het teken \ moeten worden beschermd, zijn de onderstaande metatekens:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
