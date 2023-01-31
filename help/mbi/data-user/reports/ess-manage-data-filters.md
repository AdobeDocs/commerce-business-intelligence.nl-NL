---
title: Filtersets maken voor metriek
description: Leer hoe u opgeslagen filtersets maakt en deze op de metriek toepast.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Filtersets maken

Als u meerdere meetwaarden hebt in [!DNL MBI] die op gelijkaardige wijze moeten worden gefiltreerd (bijvoorbeeld, filter uit testorden), kunt u bewaarde Reeksen van de Filter tot stand brengen en hen op metriek toepassen. Hierdoor bespaart u tijd, omdat u geen afzonderlijke filters hoeft toe te voegen wanneer u een metrisch object maakt of bewerkt.

Zie onze [trainingsvideo](https://support.magento.com/hc/en-us/articles/360016730151) voor meer informatie.

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).

1. Klikken **[!DNL Manage Data** > **Filter Sets]** in de zijbalk.

   ![](../../assets/create-filter-sets.png)

1. Klikken **[!UICONTROL Add Filter Set]** boven aan de pagina.

1. Selecteer de tabel die de metriek bevat waarop u het filter wilt toepassen.

   Als u bijvoorbeeld uw `Total number of orders` metrisch en het bouwt op `orders` tabel, selecteert u die tabel.

1. Geef de naam `Filter Set`.

1. Voeg alle relevante filters toe.

   Als we bijvoorbeeld alleen orders met de status &quot;complete&quot; in onze `Total number of orders` metrisch, zouden wij een filter toepassen dat alle orden sluit die status = niet hebben `complete`.

1. Controleer de filterlogica en of de ronde haakjes en operatoren correct zijn geplaatst: bijvoorbeeld: `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Een onjuist filter is vaak de oorzaak van gegevensdiscrepanties tussen [!DNL MBI] rapporten en de verwachte resultaten.

1. Sla de `Filter Set`.

Nadat een filterset is opgeslagen, kunt u deze toepassen op elke metrische waarde die dezelfde tabel gebruikt. Als u bijvoorbeeld een `Filter Set` op de `orders` tabel, kunt u deze toepassen op *alle metriek* op basis van deze tabel, zoals `Revenue`.

>[!NOTE]
>
>`Filter Sets` kan ook worden toegepast op berekende kolommen in [!DNL MBI]. U kunt een filterset toepassen op een gegevensdimensie die is gemaakt in [!DNL MBI] via contact op te nemen met ondersteuning.

## Verwante

* [Aanbevolen procedures voor segmentatie en filteren](../../best-practices/segment-filter.md)
