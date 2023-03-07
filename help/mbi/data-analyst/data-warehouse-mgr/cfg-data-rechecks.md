---
title: Gegevenscontroles configureren
description: Leer hoe te om gegevenskolommen met veranderlijke waarden te vormen.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Gegevenscontroles configureren

In een gegevensbestandlijst, kunnen er gegevenskolommen met veranderlijke waarden zijn. Bijvoorbeeld in een `orders`) er kan een kolom met de naam `status`. Wanneer een orde aanvankelijk aan het gegevensbestand wordt geschreven, zou de statuskolom de waarde kunnen bevatten _hangend_. De volgorde wordt overgenomen in uw [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) met `pending` waarde.

De status van de orde kan veranderen echter - zij zijn niet altijd in a `pending` status. Uiteindelijk kan het worden `complete` of `cancelled`. Om ervoor te zorgen dat uw Data Warehouse deze wijziging synchroniseert, moet de kolom opnieuw worden gecontroleerd op nieuwe waarden.

Hoe past dit in de [replicatiemethoden](../data-warehouse-mgr/cfg-replication-methods.md) dat is besproken ? De verwerking van nieuwe controles varieert op basis van de gekozen replicatiemethode. De `Modified\_At` De replicatiemethode is de beste keus voor verwerking veranderende waarden, aangezien de hercontroles niet moeten worden gevormd. De `Auto-Incrementing Primary Key` en `Primary Key Batch Monitoring` voor methoden moet de configuratie opnieuw worden gecontroleerd.

Wanneer u een van deze methoden gebruikt, moeten verwisselbare kolommen worden gemarkeerd voor nieuwe controle. Er zijn drie manieren om dit te doen:

* Een controleproces dat als deel van de update loopt markeert kolommen die opnieuw moeten worden gecontroleerd.

   >[!NOTE]
   >
   >De controleur baseert zich op een bemonsteringsproces en de veranderende kolommen kunnen niet onmiddellijk worden gevangen.

* U kunt hen plaatsen zelf door checkbox naast de kolom in de Manager van de Data Warehouse te selecteren, die klikt **[!UICONTROL Set Recheck Frequency]** en het kiezen van een geschikt tijdsinterval voor wanneer u op wijzigingen moet controleren.
* Een lid van de [!DNL MBI] Het team van de Data Warehouse kan de kolommen voor het opnieuw controleren in uw Data Warehouse manueel merken. Als u zich bewust bent van veranderbare kolommen, contacteer het team om te verzoeken dat de nieuwe controles worden geplaatst. Neem een lijst met kolommen en de frequentie op met uw verzoek.

## Frequenties opnieuw controleren {#frequency}

**Wist je dat?**
Een nieuwe controle instellen op een `primary key` de kolom controleert niet op veranderde waarden. De tabel wordt gecontroleerd op verwijderde rijen en eventuele verwijderingen worden uit de Data Warehouse gewist.

Wanneer een kolom wordt gemarkeerd voor opnieuw controleren, kunt u ook instellen hoe vaak een nieuwe controle plaatsvindt. Als een bepaalde kolom niet vaak verandert, kan het kiezen van minder frequente hercontrole [uw updatecyclus optimaliseren](../../best-practices/reduce-update-cycle-time.md).

Frequentieopties zijn:

* `always` - opnieuw controleren vindt plaats tijdens elke update
* `daily` - opnieuw controleren vindt plaats na middernacht update voor uw aangegeven tijdzone
* `weekly` - opnieuw controleren vindt elke week na 21.00 uur vrijdag een update voor uw aangegeven tijdzone plaats
* `monthly` - opnieuw controleren vindt plaats na 21.00 uur vrijdag update elke vier weken voor uw aangegeven tijdzone
* `once` - komt slechts in de volgende update voor (a-off verfrist zich)

Adobe raadt aan een `daily`, `weekly`, of `monthly` in plaats van elke update opnieuw controleren.

## Hercontrolefrequenties beheren {#manage}

De frequenties van de nieuwe controle kunnen in de Data Warehouse worden beheerd door een lijstnaam te klikken en dan individuele kolommen te controleren. De synchronisatiestatus en de hercontrolefrequentie (de **Wijzigingen?** (kolom) wordt weergegeven voor elke kolom in de tabel.

Als u de frequentie voor het opnieuw controleren wilt wijzigen, klikt u op het selectievakje naast de kolommen die u wilt wijzigen. Klik vervolgens op de knop **[!UICONTROL Set Recheck Frequency]** en stelt de gewenste frequentie in.

![](../../assets/dwm-recheck.png)

Soms ziet u `Paused` in de `Changes?` kolom. Deze waarde wordt weergegeven wanneer de tabel [replicatiemethode](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) is ingesteld op `Paused`.

Adobe raadt aan deze kolommen te reviseren om de updates te optimaliseren en ervoor te zorgen dat de veranderlijke kolommen opnieuw worden gecontroleerd. Als de frequentie voor het opnieuw controleren van een kolom hoog is gezien hoe vaak de gegevens veranderen, adviseert Adobe het verminderen van het om uw updates te optimaliseren.

Neem contact met ons op met vragen of vraag naar de huidige replicatiemethoden of hercontroles.

**Verwante:**

* [Bijwerktijden reduceren](../../best-practices/reduce-update-cycle-time.md)
* [Uw database optimaliseren voor analyse](../../best-practices/opt-db-analysis.md)
