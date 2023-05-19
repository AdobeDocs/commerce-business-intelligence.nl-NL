---
title: Kies een rapportbuilder
description: Leer hoe u de rapportbuilder kunt kiezen.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Kies een rapportbuilder

>[!NOTE]
>>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).


Nu u meer opties hebt voor het maken van analyses, is het soms moeilijk om precies te weten welke smaak van de rapportbuilder aan uw behoeften voldoet. Dit onderwerp begeleidt u door de beste manier te kiezen om uw analyse te bouwen.

## Wanneer moet ik de [!DNL SQL Report Builder]? {#whensql}

Kijk naar een aantal van de meer algemene redenen die u zou gebruiken [!DNL SQL Report Builder] over de [!DNL traditional Report Builder].

### Als u wilt gebruiken [!DNL SQL]-specifieke functies...

Deel van de schoonheid van de [!DNL SQL Report Builder] is dat het u de capaciteit geeft om functies te gebruiken die momenteel niet beschikbaar in de Manager van de Data Warehouse zijn. In het verleden had een analist u misschien moeten helpen uw visie volledig te realiseren.

De [!DNL SQL Report Builder] ondersteunt functies zoals [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) en [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), die u voorheen niet kon gebruiken. U hebt toegang tot de [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), maar enkele andere SQL-specifieke functies zijn:

* [`Bitwise aggregate` functies](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Als u wat tests wilt uitvoeren...

Als u verschillende technieken en strategieën wilt uitproberen om uit te vinden wat het beste voor uw analyse werkt, zou u kunnen willen gebruiken [!DNL SQL Report Builder]. Het opbouwen van kolommen in de Manager van de Data Warehouse vergt tijd en kolommen die u gebruikend DWM creeert hangt van updatecycli af.

U moet op zijn best een updatecyclus doorlopen voordat u de kolom kunt gebruiken. Als u zich realiseert maakte u een fout in de bouw van de kolom, moet u door wachten *twee* cycli: één om de kolom aanvankelijk te vullen, en een andere cyclus voor de revisies om zich te verspreiden.

### Als u slechts eenmaal een nieuwe kolom gebruikt...

Zoals vermeld in de bovenstaande sectie, kost het maken van een kolom in de Manager van de Data Warehouse tijd. Als u slechts van plan bent om een kolom te gebruiken u in één rapport creeert, stelt Adobe het gebruiken van voor [!DNL SQL Report Builder]. Hierdoor hoeft u niet te wachten tot een updatecyclus is voltooid, zodat u sneller weer aan de slag kunt.

### Als u werkt met gegevens die een één-op-vele verhouding hebben...

Soms kan de structuur van de gegevens de [!DNL SQL Report Builder] een efficiëntere en logische keuze voor het maken van uw analyse. Het creëren van kolommen voor één-op-één verhoudingen is ongecompliceerd in de Manager van de Data Warehouse, maar de dingen kunnen een beetje verwarrend worden wanneer u met één-aan-vele verhoudingen behandelt.

Stel dat één product wordt beschouwd als onderdeel van meerdere productcategorieën en u wilt de inkomsten bekijken die aan elke categorie van elk product zijn gekoppeld. Het maken van deze relatie met de DWM kan vervelend en moeilijk zijn, maar het schrijven van een [!DNL SQL] query kan wat eenvoudiger zijn:

![](../../assets/When_should_I_use_the_RB_2.png)

## Wanneer moet ik de traditionele Report Builder gebruiken? {#whentraditionalrb}

Terwijl de [!DNL SQL Report Builder] geeft u meer controle en toegang tot eerder niet beschikbare functionaliteit, zou het niet altijd de juiste keus kunnen zijn. Adobe stelt voor dat u ook rekening houdt met het volgende wanneer u bepaalt welke smaak de rapportaannemer moet gebruiken.

### Als u een eenvoudig rapport opstelt...

Als u eenvoudig wilt maken, is het gebruik van de traditionele Report Builder veel sneller dan het schrijven van een volledige [!DNL SQL] query. Het helpt als om het even welke kolommen die u de analyse moet tot stand brengen reeds in de Manager van de Data Warehouse zijn.

### Als u uw werk deelt met andere gebruikers...

Gebruikt/bekijkt u deze analyse door gebruikers in uw hele organisatie? Afhankelijk van wie u uw werk met deelt, kan het plakken met Visual Report Builder soms beter zijn. Gebruikers kunnen snel naar de definitie in de [!DNL Visual Report Builder] versus het lezen van een potentieel lange [!DNL SQL] query.

Als er mensen zijn die het verslag nodig hebben maar die niet bekend zijn met [!DNL SQL]Adobe stelt voor de oorspronkelijke smaak van de Report Builder te gebruiken. Het maakt het makkelijker voor hen.

## Omloop {#wrapup}

Beide [!DNL SQL Report Builder] en [!DNL Visual Report Builder] geschikt zijn voor een groot aantal gebruiksgevallen. Dit hangt meestal af van wat uw analytische behoeften zijn en wie de analyse gebruikt.
