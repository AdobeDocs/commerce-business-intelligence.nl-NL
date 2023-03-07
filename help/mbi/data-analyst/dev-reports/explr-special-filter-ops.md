---
title: Speciale filteroperatoren
description: Leer over een paar speciale exploitanten die in filters worden gebruikt wanneer het creëren van een rapport of het creëren van metrisch.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Filteropties

In dit artikel worden enkele speciale `operators` gebruikt in `filters` wanneer [opstellen van een rapport](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} of [metrisch maken](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` voor patroonovereenkomst. Dit moet worden gebruikt met de jokertekens % (voor een jokerteken met een variabel aantal letters) of _ (voor een jokerteken met één letter).  De beperking `LIKE \_ake%` retourneert true voor `Jake Stein`, `Jake Smith`, of `Fake Smith`.  Het zou vals voor terugkeren `Drake Smith`.

* `NOT LIKE` is vergelijkbaar met bovenstaande patroonovereenkomst, maar controleert op welke patronen geen overeenkomende patronen voorkomen.

* `IS` controleert of de kolom is `NULL`, of leeg.

* `IS NOT` is vergelijkbaar met de `IS` hierboven, maar controleert op kolommen die niet NULL zijn.

* `IN` controleert of een waarde voorkomt in een lijst met komma&#39;s als scheidingsteken. (bijvoorbeeld &quot;Kleur `IN` rood,oranje&quot; is het equivalent van kleur `equal to` rood OF kleur `equal to` oranje).

* `NOT IN` is vergelijkbaar met `IN` hierboven, maar controleert of er geen waarde is.
