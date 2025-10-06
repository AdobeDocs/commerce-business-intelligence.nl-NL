---
title: Kies een rapportbuilder
description: Leer hoe u de rapportbuilder kunt kiezen.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Kies een rapportbuilder

>[!NOTE]
>&#x200B;>Vereist [&#x200B; toestemmingen Admin &#x200B;](../../administrator/user-management/user-management.md).

Nu u meer opties hebt voor het maken van analyses, is het soms moeilijk om precies te weten welke smaak van de rapportbuilder aan uw behoeften voldoet. Dit onderwerp begeleidt u door de beste manier te kiezen om uw analyse te bouwen.

## Wanneer moet ik de [!DNL SQL Report Builder] gebruiken? {#whensql}

Bekijk een aantal van de meer algemene redenen waarom u de [!DNL SQL Report Builder] over de [!DNL traditional Report Builder] zou gebruiken.

### Als u [!DNL SQL] -specifieke functies wilt gebruiken...

Een deel van de schoonheid van [!DNL SQL Report Builder] is dat het u de capaciteit geeft om functies te gebruiken die momenteel niet beschikbaar in de Manager van Data Warehouse zijn. In het verleden had een analist u misschien moeten helpen uw visie volledig te realiseren.

[!DNL SQL Report Builder] steunt functies zoals [`LISTAGG` &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) en [`GETDATE` &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), die u niet kon eerder gebruiken. U kunt tot [`full list` toegang hebben &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), maar sommige andere SQL-Specifieke functies omvatten:

* [`Bitwise aggregate` functies &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Als u wat tests wilt uitvoeren...

Als u verschillende technieken en strategieën wilt uitproberen om te bepalen wat het beste werkt voor uw analyse, kunt u [!DNL SQL Report Builder] gebruiken. Het opbouwen van kolommen in de Manager van Data Warehouse vergt tijd en kolommen die u gebruikend DWM creeert hangt van updatecycli af.

U moet op zijn best een updatecyclus doorlopen voordat u de kolom kunt gebruiken. Als u realiseert hebt u een fout in de bouw van de kolom gemaakt, moet u door *twee* cycli wachten: om de kolom aanvankelijk te bevolken, en een andere cyclus voor de revisies om zich te verspreiden.

### Als u slechts eenmaal een nieuwe kolom gebruikt...

Zoals vermeld in de bovenstaande sectie, kost het maken van een kolom in Data Warehouse Manager tijd. Als u slechts van plan bent om een kolom te gebruiken u in één rapport creeert, stelt Adobe voor [!DNL SQL Report Builder] te gebruiken. Hierdoor hoeft u niet langer te wachten tot een updatecyclus is voltooid, zodat u sneller weer aan de slag kunt.

### Als u werkt met gegevens die een één-op-vele verhouding hebben...

Soms kan de structuur van de gegevens van [!DNL SQL Report Builder] een efficiëntere en logische keuze maken om uw analyse samen te stellen. Het maken van kolommen voor één-op-één relaties is eenvoudig in Data Warehouse Manager, maar het kan een beetje verwarrend zijn wanneer u met één-op-veel relaties werkt.

Stel dat één product wordt beschouwd als onderdeel van meerdere productcategorieën en u wilt de inkomsten bekijken die aan elke categorie van elk product zijn gekoppeld. Het maken van deze relatie met behulp van DWM kan vervelend en moeilijk zijn, maar het schrijven van een query [!DNL SQL] kan wat eenvoudiger zijn:

![&#x200B; SQL vraag die opbrengst door productcategorie met één-aan-vele verhoudingen toont &#x200B;](../../assets/When_should_I_use_the_RB_2.png)

## Wanneer moet ik de traditionele Report Builder gebruiken? {#whentraditionalrb}

Hoewel [!DNL SQL Report Builder] u meer controle en toegang tot eerder niet beschikbare functionaliteit geeft, is het misschien niet altijd de juiste keuze. Adobe stelt voor dat u ook rekening houdt met het volgende wanneer u bepaalt welke smaak de rapportaannemer moet gebruiken.

### Als u een eenvoudig rapport opstelt...

Als u eenvoudig wilt maken, kunt u de traditionele Report Builder veel sneller gebruiken dan een volledige [!DNL SQL] query schrijven. Het is handig als de kolommen die u nodig hebt om de analyse te maken, al in Data Warehouse Manager staan.

### Als u uw werk deelt met andere gebruikers...

Gebruikt/bekijkt u deze analyse door gebruikers in uw hele organisatie? Afhankelijk van met wie u uw werk deelt, kan het beter zijn om met Visual Report Builder te blijven hangen. Gebruikers kunnen snel naar de definitie in de [!DNL Visual Report Builder] zoeken en een mogelijk lange [!DNL SQL] -query lezen.

Als er mensen zijn die het rapport nodig hebben maar niet bekend zijn met [!DNL SQL] , stelt Adobe voor de oorspronkelijke smaak van de Report Builder te gebruiken. Het maakt het makkelijker voor hen.

## Omloop {#wrapup}

Zowel [!DNL SQL Report Builder] als [!DNL Visual Report Builder] zijn geschikt voor een groot aantal gebruiksgevallen. Dit hangt meestal af van wat uw analytische behoeften zijn en wie de analyse gebruikt.
