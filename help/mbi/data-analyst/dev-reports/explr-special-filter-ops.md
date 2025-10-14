---
title: Speciale filteroperatoren
description: Leer over een paar speciale exploitanten die in filters worden gebruikt wanneer het creëren van een rapport of het creëren van metrisch.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Filteropties

Dit onderwerp verkent een paar speciale `operators` die in `filters` worden gebruikt wanneer [&#x200B; creërend een rapport &#x200B;](../../tutorials/using-visual-report-builder.md){: target="_blank"} of [&#x200B; creërend metrisch &#x200B;](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}.

## `Filter Operators`

* `LIKE` voor overeenkomende patronen. Dit moet worden gebruikt met de jokertekens % (voor een jokerteken met een variabel aantal letters) of _ (voor een jokerteken met één letter).  De beperking `LIKE \_ake%` retourneert bijvoorbeeld true voor `Jake Stein` , `Jake Smith` of `Fake Smith` .  Deze geeft false voor `Drake Smith` .

* `NOT LIKE` is vergelijkbaar met bovenstaande patroonovereenkomst, maar controleert op welke patronen niet overeenkomen.

* `IS` controleert of de kolom `NULL` of leeg is.

* `IS NOT` lijkt op de bovenstaande operator `IS` , maar controleert op kolommen die niet gelijk zijn aan NULL.

* `IN` controleert of een waarde voorkomt in een lijst met komma&#39;s als scheidingsteken. (Kleur `IN` rood,oranje is bijvoorbeeld het equivalent van kleur `equal to` rood OF kleur `equal to` oranje).

* `NOT IN` lijkt op `IN` hierboven, maar controleert of er geen waarde is.
