---
title: Gegevenscontroles configureren
description: Leer hoe te om gegevenskolommen met veranderlijke waarden te vormen.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Gegevenscontroles configureren

In een gegevensbestandlijst, kunnen er gegevenskolommen met veranderlijke waarden zijn. In een `orders` -tabel kan bijvoorbeeld een kolom met de naam `status` voorkomen. Wanneer een orde aanvankelijk aan het gegevensbestand wordt geschreven, zou de statuskolom de waarde _in afwachting van_ kunnen bevatten. De orde wordt herhaald in uw [ Data Warehouse ](../data-warehouse-mgr/tour-dwm.md) met deze `pending` waarde.

De status van de orde kan veranderen, hoewel zij niet altijd in een `pending` status zijn. Uiteindelijk kan het `complete` of `cancelled` worden. Om ervoor te zorgen dat uw Data Warehouse deze wijziging synchroniseert, moet de kolom opnieuw worden gecontroleerd op nieuwe waarden.

Hoe past dit binnen met de [ replicatiemethodes ](../data-warehouse-mgr/cfg-replication-methods.md) die werd besproken? De verwerking van nieuwe controles varieert op basis van de gekozen replicatiemethode. De `Modified\_At` replicatiemethode is de beste keus voor verwerking veranderende waarden, aangezien de hercontroles niet moeten worden gevormd. Voor de methoden `Auto-Incrementing Primary Key` en `Primary Key Batch Monitoring` moet de configuratie opnieuw worden gecontroleerd.

Wanneer u een van deze methoden gebruikt, moeten verwisselbare kolommen worden gemarkeerd voor nieuwe controle. Er zijn drie manieren om dit te doen:

1. Een controleproces dat als deel van de update loopt markeert kolommen die opnieuw moeten worden gecontroleerd.

   >[!NOTE]
   >
   >De controleur baseert zich op een bemonsteringsproces en de veranderende kolommen kunnen niet onmiddellijk worden gevangen.

1. U kunt hen plaatsen zelf door checkbox naast de kolom in de Manager van de Data Warehouse te selecteren, **[!UICONTROL Set Recheck Frequency]** te klikken, en een aangewezen tijdinterval te kiezen wanneer u op veranderingen zou moeten controleren.

1. Een lid van het team van de Data Warehouse [!DNL Adobe Commerce Intelligence] kan de kolommen voor het opnieuw controleren in uw Data Warehouse manueel merken. Als u zich bewust bent van veranderbare kolommen, contacteer het team om te verzoeken dat de nieuwe controles worden geplaatst. Neem een lijst met kolommen en de frequentie op met uw verzoek.

## Frequenties opnieuw controleren {#frequency}

**Wist u het?**
Als u een nieuwe controle op een kolom van het type `primary key` instelt, wordt de kolom niet gecontroleerd op gewijzigde waarden. De tabel wordt gecontroleerd op verwijderde rijen en eventuele verwijderingen worden uit de Data Warehouse gewist.

Wanneer een kolom wordt gemarkeerd voor opnieuw controleren, kunt u ook instellen hoe vaak een nieuwe controle plaatsvindt. Als een bepaalde kolom niet vaak verandert, kan het kiezen van minder frequente hercontrole [ uw updatecyclus ](../../best-practices/reduce-update-cycle-time.md) optimaliseren.

Frequentieopties zijn:

* `always` - opnieuw controleren vindt plaats tijdens elke update
* `daily` - opnieuw controleren vindt plaats na middernacht update voor uw gedeclareerde tijdzone
* `weekly` - opnieuw controleren vindt elke week na 21.00 uur vrijdag een update voor uw aangegeven tijdzone plaats
* `monthly` - opnieuw controleren vindt plaats na 21.00 uur vrijdag bijwerken elke vier weken voor uw gedeclareerde tijdzone
* `once` - komt slechts in de volgende update voor (a-off verfrist zich)

Aangezien de updatetijden gecorreleerd zijn aan hoeveel gegevens moeten worden gesynchroniseerd, raadt de Adobe aan een `daily` -, `weekly` - of `monthly` -controle te kiezen in plaats van elke update.

## Hercontrolefrequenties beheren {#manage}

De frequenties van de nieuwe controle kunnen in de Data Warehouse worden beheerd door een lijstnaam te klikken en dan individuele kolommen te controleren. De synchroniserende status en recheck frequentie (de **Veranderingen?** (kolom) wordt weergegeven voor elke kolom in de tabel.

Als u de frequentie voor het opnieuw controleren wilt wijzigen, klikt u op het selectievakje naast de kolommen die u wilt wijzigen. Klik vervolgens op de vervolgkeuzelijst **[!UICONTROL Set Recheck Frequency]** en stel de gewenste frequentie in.

![](../../assets/dwm-recheck.png)

Soms ziet u `Paused` in de kolom `Changes?` . Deze waarde toont wanneer de 0&rbrace; replicatiemethode van de lijst [&#128279;](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) aan `Paused` wordt geplaatst.

[!DNL Adobe] raadt u aan deze kolommen te controleren om de updates te optimaliseren en ervoor te zorgen dat de verwisselbare kolommen opnieuw worden gecontroleerd. Als de frequentie voor het opnieuw controleren van een kolom hoog is gezien hoe vaak de gegevens veranderen, adviseert de Adobe het te verminderen om uw updates te optimaliseren.

Neem contact met ons op met vragen of vraag naar de huidige replicatiemethoden of hercontroles.

**Verwante:**

* [Bijwerktijden reduceren](../../best-practices/reduce-update-cycle-time.md)
* [Uw database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md)
