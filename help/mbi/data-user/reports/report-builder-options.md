---
title: Kies een rapportbuilder
description: Leer hoe u de rapportbuilder kunt kiezen.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Kies een rapportbuilder

>[!NOTE]
>>Vereisten [Beheerdersmachtigingen](../../administrator/user-management/user-management.md).


We hebben allemaal graag opties. Maar als we geconfronteerd worden met keuzes, kunnen sommigen van ons het idee van het moeten toezeggen aan een beslissing blokkeren. Opties zijn geweldig, maar ze kunnen ook overweldigend en verwarrend zijn.

Nu u meer opties hebt om analyses te maken, is het soms moeilijk om precies te weten welke smaak van de rapportaannemer aan uw behoeften zal aanpassen. Als u wat begeleiding bij het kiezen van de beste manier nodig hebt om uw analyse te bouwen, is dit artikel voor u.

## Wanneer moet ik de `SQL Report Builder`? {#whensql}

Neem een blik bij enkele gemeenschappelijkere redenen u SQL Report Builder over de traditionele Report Builder zou gebruiken.

### Als u SQL-specifieke functies wilt gebruiken...

Deel van de schoonheid van de `SQL Report Builder` is dat het u de capaciteit geeft om functies te gebruiken die momenteel niet beschikbaar in de Manager van de Data Warehouse zijn. In het verleden had een analist u misschien moeten helpen uw visie volledig te realiseren.

De SQL Report Builder ondersteunt functies zoals [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) en [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), die u voorheen niet kon gebruiken. U hebt toegang tot de [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), maar enkele andere SQL-specifieke functies zijn:

* [`Bitwise aggregate` functies](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Als u wat tests wilt uitvoeren...

Als u verschillende technieken en strategieën wilt uitproberen om uit te vinden wat het beste voor uw analyse werkt, zou u kunnen willen gebruiken `SQL Report Builder`. Het opbouwen van kolommen in de Manager van de Data Warehouse vergt tijd en de kolommen u creeert gebruikend DWM zijn afhankelijk van updatecycli.

U moet op zijn best een updatecyclus doorlopen voordat u de kolom kunt gebruiken. Als u zich realiseert hebt u een fout in de bouw van de kolom gemaakt, zult u door moeten wachten *twee* cycli: één om de kolom aanvankelijk te vullen, en een andere cyclus voor de revisies om zich te verspreiden.

### Als u slechts eenmaal een nieuwe kolom gebruikt...

Zoals we in de bovenstaande sectie hebben vermeld, kost het maken van een nieuwe kolom in Beheer Data Warehouse tijd. Als u slechts van plan bent om een kolom te gebruiken u in één rapport creeert, adviseren wij gebruikend `SQL Report Builder`. Hierdoor hoeft u niet langer te wachten tot een updatecyclus is voltooid, zodat u sneller weer aan de slag kunt.

### Als u werkt met gegevens die een één-op-vele verhouding hebben...

In sommige gevallen kan de structuur van de gegevens de `SQL Report Builder` een efficiëntere en logische keuze voor het maken van uw analyse. Het creëren van kolommen voor één-op-één verhoudingen is vrij ongecompliceerd in de Manager van de Data Warehouse, maar de dingen kunnen een beetje verwarrend worden wanneer u met één-aan-vele verhoudingen omgaat.

Stel dat één product wordt beschouwd als onderdeel van meerdere productcategorieën en u wilt de inkomsten bekijken die aan elke categorie van elk product zijn gekoppeld. Het proberen van deze verhouding tot stand te brengen gebruikend DWM kan vervelend en moeilijk zijn, maar het schrijven van een SQL vraag kan een beetje ongecompliceerder zijn:

![](../../assets/When_should_I_use_the_RB_2.png)

## Wanneer moet ik de traditionele Report Builder gebruiken? {#whentraditionalrb}

Terwijl de `SQL Report Builder` geeft u meer controle en toegang tot eerder niet beschikbare functionaliteit, zou het niet altijd de juiste keus kunnen zijn. Wij stellen voor dat u ook rekening houdt met het volgende wanneer u bepaalt welke smaak de rapportaannemer moet gebruiken.

### Als u een eenvoudig rapport opstelt...

Als u eenvoudig wilt maken, kunt u de traditionele Report Builder veel sneller gebruiken dan een volledige SQL-query schrijven. Het zal ook helpen als om het even welke kolommen u de analyse moet tot stand brengen reeds in de Manager van de Data Warehouse zijn.

### Als u uw werk deelt met andere gebruikers...

Zullen gebruikers in uw organisatie deze analyse gebruiken/bekijken? Afhankelijk van wie u uw werk met deelt, kan het kleven met Visual Report Builder in sommige gevallen beter zijn. De gebruikers kunnen snel de definitie in Visual Report Builder tegenover het lezen van een potentieel lange SQL vraag bekijken.

Als er mensen zijn die het rapport maar niet vertrouwd met SQL nodig hebben, adviseren wij het gebruiken van de originele smaak van de Report Builder. Het maakt het voor hen gemakkelijker.

## Omloop {#wrapup}

Beide `SQL Report Builder` en `Visual Report Builder` geschikt zijn voor een groot aantal gebruiksgevallen. Dit hangt meestal af van wat uw analytische behoeften zijn en wie de analyse zal gebruiken.
