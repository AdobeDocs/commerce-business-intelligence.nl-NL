---
title: Toegang tot uw database beperken
description: Leer hoe u toegang kunt beperken, die toegang tot de server beperken die uw gegevensbestand opneemt.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Toegang beperken

Wanneer u een tunnel van SSH aan uw server creeert, is er geen behoefte aan [!DNL MBI] om toegang te hebben tot om het even wat behalve het gegevensbestand. Als u dat niet wilt [!DNL MBI] om volledige toegang te hebben tot de server die uw gegevensbestand opneemt, kunt u toegang beperken door [!DNL MBI Linux®] gebruiker in een [schelp](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Mogelijk hebt u de naam als uitgangspunt genomen, maar een beperkte schaal wordt gebruikt om een omgeving in te stellen die beter wordt bestuurd dan de standaardshell. Het belangrijkste aan dit type shell is dat beperkte shell gebruikers tot systeemfuncties kunnen toegang hebben of om het even welk soort wijzigingen maken.

De [!DNL MBI Linux®] gebruiker, moet u twee dingen doen:

1. Wijzig de omgevingsvariabele PATH in de lege tekenreeks. Dit betekent dat de gebruiker geen toegang heeft tot systeem uitvoerbare bestanden.

1. Zorg ervoor dat shell wordt uitgevoerd `bash -r`

Beide kunnen binnen `authorized_keys` bestand in de woning van de gebruiker `dir/.ssh` als onderdeel van de opdracht die wordt uitgevoerd wanneer de gebruiker zich aanmeldt. Het ziet er ongeveer als volgt uit:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Zodra dit volledig is, de gebruiker u voor creeerde [!DNL MBI] kan geen wijzigingen aanbrengen in uw systeem.
