---
title: Filtersets maken voor metriek
description: Leer hoe u opgeslagen filtersets maakt en toepast op de metriek.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Filtersets maken

Als u meerdere metriek in [!DNL Commerce Intelligence] hebt die op een vergelijkbare manier moeten worden gefilterd (bijvoorbeeld testopdrachten uitfilteren), kunt u opgeslagen filtersets maken en deze op de metriek toepassen. Hierdoor bespaart u tijd, omdat u geen afzonderlijke filters hoeft toe te voegen wanneer u een metrisch object maakt of bewerkt.

Zie de [&#x200B; opleidingsvideo &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=nl-NL) voor meer informatie.

>[!NOTE]
>
>Vereist [&#x200B; toestemmingen Admin &#x200B;](../../administrator/user-management/user-management.md).

1. Klik op **[!DNL Manage Data** > **Filter Sets]** in de zijbalk.

   ![&#x200B; creeer filterreeksen interface met toevoegen filterplaatoptie &#x200B;](../../assets/create-filter-sets.png)

1. Klik op **[!UICONTROL Add Filter Set]** boven aan de pagina.

1. Selecteer de tabel die de metriek bevat waarop u het filter wilt toepassen.

   Als u bijvoorbeeld de metrische waarde van `Total number of orders` wilt filteren en deze is gebaseerd op de tabel van `orders` , selecteert u die tabel.

1. Geef de `Filter Set` een naam.

1. Voeg alle relevante filters toe.

   Als u bijvoorbeeld alleen orders met de status &#39;complete&#39; in de `Total number of orders` -metrische code wilt opnemen, past u een filter toe dat alle orders zonder status = `complete` uitsluit.

1. Controleer de filterlogica en of de ronde haakjes en operatoren correct zijn geplaatst, bijvoorbeeld `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]` .

   Een onjuist filter is vaak de oorzaak van gegevensdiscrepanties tussen [!DNL Commerce Intelligence] -rapporten en de verwachte resultaten.

1. Sla de `Filter Set` op.

Nadat een filterset is opgeslagen, kunt u deze toepassen op elke metrische waarde die dezelfde tabel gebruikt. Bijvoorbeeld, als u a `Filter Set` op de `orders` lijst creeerde, kunt u het op *toepassen om het even welke metriek* die op deze lijst, zoals `Revenue` wordt voortgebouwd.

>[!NOTE]
>
>`Filter Sets` kan ook worden toegepast op berekende kolommen in [!DNL Commerce Intelligence] . U kunt een filterset toepassen op een gegevensdimensie die in [!DNL Commerce Intelligence] is gemaakt, door contact op te nemen met de ondersteuningsafdeling.

## Verwante

* [Aanbevolen procedures voor segmentatie en filteren](../../best-practices/segment-filter.md)
