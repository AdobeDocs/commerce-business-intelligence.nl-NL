---
title: Andere gegevens importeren en doorgeven
description: Leer offline of andere bestanden te importeren en gegevens uit te geven in [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Andere gegevens importeren en doorgeven

Door uw advertentieuitgaven te uploaden, kunt u het rendement van de campagne meten door uw advertentiekosten en de `customer lifetime value (CLV)` van gebruikers die zijn aangeschaft via uw campagnes.

## Reclamegegevens uploaden

De eerste stap bij het analyseren en uitgeven van gegevens is het krijgen van de gegevens. Aangezien u met de meeste advertentieplatforms rapporten kunt exporteren, raadt Adobe u aan de onbewerkte gegevens te exporteren van uw advertentieplatform en deze rechtstreeks te uploaden naar [!DNL Commerce Intelligence] zonder enige manipulatie. U kunt bewerkingen uitvoeren op de gegevens in uw Data Warehouse, zodat het niet nodig is om uw inspanningen te verdubbelen.

Nadat u de advertentie hebt geëxporteerd, kunt u de opdracht [`File Upload` functie](../connecting-data/using-file-uploader.md) om de gegevens in uw Data Warehouse te brengen. U kunt nieuwe gegevens uploaden naar hetzelfde [!DNL Commerce Intelligence] tabel in de tijd.

## Offline bronnen

Naast uw online campagnes, kunt u ook reclame, zoals op de radio of een billboard offline hebben. Als u deze gevallen wilt verwerken, kunt u handmatig een spreadsheet met de kostengegevens uploaden naar [!DNL Commerce Intelligence].

De onderstaande tabelstructuur wordt aanbevolen bij het maken van een `.csv` om gegevens op te nemen en uit te geven. Een malplaatjedossier is ook in bijlage bij de bodem van dit onderwerp als voorbeeld. Aanbevolen kolommen zijn:

* `ID` - Dit is een unieke id voor elke gegevensrij die door de database wordt gebruikt als primaire sleutel. Dit moet voor elke rij anders zijn.
* `Date` - Dit is de datum waarop de campagne is gestart, in dd-formaat jjjj-mm.
* `Amount` - Dit is het bedrag dat u aan de campagne hebt uitgegeven.
* `campaign` - Dit is de naam van de campagne. Als u [!DNL Google Analytics] om uw andere gegevens te volgen en door te geven, moet deze overeenkomen met de naam van de utm\_campagne.
* `source` - Dit is de bronnaam. Als u [!DNL Google Analytics], moet dit overeenkomen met de `utm_source` naam.
* `other` (Optioneel) - U kunt ook extra kolommen opnemen die u helpen campagnes en kosten te segmenteren. Het kan ook een manier zijn om verschillende namen van UTM-campagnes samen te vatten in één coherente campagne voor traceringsdoeleinden. In plaats van dit manueel opstelling, zou het goed kunnen zijn om V-Lookup aan een tweede blad te gebruiken om elke Naam van de Campagne aan Andere Naam aan te passen en het hier dynamisch te melden.

## Verwante

* [Verbinden [!DNL AdWords] data](../integrations/google-adwords.md)
* [Rendement op reclamecampagnes verhogen](../../analysis/roi-ad-camp.md)
