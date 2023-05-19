---
title: MongoDB-gegevensmodellering
description: Leer hoe u gegevenspatronen kunt vermijden die een probleem vormen.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# [!DNL MongoDB] Gegevensmodellering

Wanneer [!DNL Adobe Commerce Intelligence] pulls in [!DNL MongoDB] gegevens, die gegevens worden omgezet in een relationeel model.

Het slechte nieuws: Hoewel de meeste gegevenspatronen geen probleem vormen, zijn er een aantal die niet worden ondersteund door [!DNL Commerce Intelligence]vanwege de vertaling naar een relationeel model.

Het goede nieuws: Al deze patronen kunnen worden vermeden.

## Subgeneste arrays {#subnested}

Als de verzameling er als volgt uitziet: [!DNL Commerce Intelligence] dupliceert alleen de gegevens in de itemarray. Gegevens uit de subitems-array worden niet opgehaald.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Toetsen voor variabele objecten {#varobjectkeys}

Verzamelingen die objecten met variabele-objectsleutels bevatten, worden niet gerepliceerd in [!DNL Commerce Intelligence]. Bijvoorbeeld:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Dit gebeurt gewoonlijk wanneer een object wordt gebruikt en een array geschikter is. Wijzig nu het bovenstaande voorbeeld:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
