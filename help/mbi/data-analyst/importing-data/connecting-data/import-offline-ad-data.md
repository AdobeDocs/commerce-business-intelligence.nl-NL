---
title: Andere gegevens importeren en doorgeven
description: Leer om off-line of andere in te voeren en gegevens in  [!DNL Commerce Intelligence] uit te geven.
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Andere gegevens importeren en doorgeven

Door uw advertentieuitgavengegevens te uploaden, kunt u het investeringsrendement van de campagne meten door uw advertentiekosten en `customer lifetime value (CLV)` gebruikers die u van uw campagnes hebt aangeschaft, te laten vergelijken.

## Reclamegegevens uploaden

De eerste stap bij het analyseren en uitgeven van gegevens is het krijgen van de gegevens. Aangezien de meeste advertentieplatforms u toestaan om rapporten uit te voeren, beveelt Adobe u aan de ruwe gegevens van uw advertentieplatform uit te voeren en het direct te uploaden aan [!DNL Commerce Intelligence] zonder enige manipulatie. U kunt bewerkingen uitvoeren op de gegevens in uw Data Warehouse, zodat het niet nodig is om uw inspanningen te verdubbelen.

Nadat u de advertentie hebt geëxporteerd, gebruikt u de functie [`File Upload` &#x200B;](../connecting-data/using-file-uploader.md) om de gegevens over te brengen naar uw Data Warehouse. U kunt nieuwe gegevens in de loop der tijd naar dezelfde [!DNL Commerce Intelligence] -tabel uploaden.

## Offline bronnen

Naast uw online campagnes, kunt u ook reclame, zoals op de radio of een billboard offline hebben. Als u deze gevallen wilt verwerken, kunt u handmatig een spreadsheet met de kostengegevens uploaden naar [!DNL Commerce Intelligence] .

De onderstaande tabelstructuur wordt aanbevolen wanneer u een `.csv` -bestand maakt om gegevens op te nemen en uit te geven. Een malplaatjedossier is ook in bijlage bij de bodem van dit onderwerp als voorbeeld. Aanbevolen kolommen zijn:

* `ID` - Dit is een unieke id voor elke gegevensrij die door de database als primaire sleutel wordt gebruikt. Dit moet voor elke rij anders zijn.
* `Date` - Dit is de datum waarop de campagne is gestart, in jjjj-mm-dd-indeling.
* `Amount` - Dit is het bedrag dat u aan de campagne hebt uitgegeven.
* `campaign` - Dit is de naam van de campagne. Als u [!DNL Google Analytics] gebruikt om uw andere gegevens bij te houden en te besteden, moet deze overeenkomen met de naam van de utm\_campagne.
* `source` - Dit is de bronnaam. Als u [!DNL Google Analytics] gebruikt, moet dit overeenkomen met de naam `utm_source` .
* `other` (Optioneel) - U kunt ook extra kolommen opnemen die u helpen campagnes en kosten te segmenteren. Het kan ook een manier zijn om verschillende namen van UTM-campagnes samen te vatten in één coherente campagne voor traceringsdoeleinden. In plaats van dit manueel opstelling, zou het goed kunnen zijn om V-Lookup aan een tweede blad te gebruiken om elke Naam van de Campagne aan Andere Naam aan te passen en het hier dynamisch te melden.

## Verwante

* [Verbind  [!DNL AdWords]  gegevens](../integrations/google-adwords.md)
* [Rendement op reclamecampagnes verhogen](../../analysis/roi-ad-camp.md)
