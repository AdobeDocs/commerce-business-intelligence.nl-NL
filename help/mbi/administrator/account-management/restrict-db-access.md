---
title: Toegang tot uw database beperken
description: Leer hoe u toegang kunt beperken, die toegang tot de server beperken die uw gegevensbestand opneemt.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Toegang beperken

Wanneer u een tunnel van SSH aan uw server creeert, is er geen behoefte aan [!DNL Adobe Commerce Intelligence] om toegang te hebben tot om het even wat behalve het gegevensbestand. Als u dat niet wilt [!DNL Commerce Intelligence] om volledige toegang te hebben tot de server die uw gegevensbestand opneemt, kunt u toegang beperken door [!DNL Commerce Intelligence Linux] gebruiker in een [schelp](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Mogelijk hebt u de naam als uitgangspunt genomen, maar een beperkte schaal wordt gebruikt om een omgeving in te stellen die beter wordt bestuurd dan de standaardshell. Het belangrijkste aan dit type shell is dat beperkte shell gebruikers tot systeemfuncties kunnen toegang hebben of om het even welk soort wijzigingen maken.

Om de [!DNL Commerce Intelligence Linux] gebruiker, moet u twee dingen doen:

1. Wijzig de omgevingsvariabele PATH in de lege tekenreeks. Dit betekent dat de gebruiker geen toegang heeft tot systeem uitvoerbare bestanden.

1. Zorg ervoor dat shell wordt uitgevoerd `bash -r`

Beide kunnen worden uitgevoerd binnen de `authorized_keys` bestand in de woning van de gebruiker `dir/.ssh` als onderdeel van de opdracht die wordt uitgevoerd wanneer de gebruiker zich aanmeldt. Het ziet er ongeveer als volgt uit:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Wanneer deze bewerking is voltooid, heeft de gebruiker waarvoor u [!DNL Commerce Intelligence] kan geen wijzigingen aanbrengen in uw systeem.
