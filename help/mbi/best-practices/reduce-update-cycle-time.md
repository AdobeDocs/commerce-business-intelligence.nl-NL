---
title: De tijd van de updatecyclus verkorten
description: Leer hoe u de updatecyclus verkort.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Verminder de verwerkingstijd van de updatecyclus

[!DNL Adobe Commerce Intelligence] synchroniseert de hele dag met de database om nieuwe gegevens te repliceren, zodat op de dashboards altijd de meest recente informatie wordt weergegeven.

Veel factoren kunnen een reeds lange updatetijd vergroten. Bepaalde replicatiemethodes, hogere recheck frequenties, en het aantal dashboards en grafieken zijn enkel een paar contribuanten. In deze onderwerpen worden enkele aanbevolen procedures besproken om de updatetijden te verkorten.

## Frequentie voor opnieuw controleren verlagen

In een gegevensbestandlijst, kunnen er gegevenskolommen met veranderlijke waarden zijn. Bijvoorbeeld in een **orders** tabel kan een kolom met de naam **status**. Wanneer een orde aanvankelijk aan het gegevensbestand wordt geschreven, zou de statuskolom de waarde kunnen bevatten `pending`. De volgorde wordt overgenomen in uw [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) met `pending` waarde.

Wijzigbare kolommen moeten [opnieuw gecontroleerd op bijgewerkte waarden](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) na verloop van tijd. Standaard, [!DNL Commerce Intelligence] controleert deze kolommen tijdens elke update opnieuw, maar als er een grote hoeveelheid gegevens is die opnieuw moet worden gecontroleerd en worden herhaald, kan het negatief uw updatetijd beïnvloeden. In plaats van tijdens elke update opnieuw te controleren, raadt Adobe aan de frequentie voor het opnieuw controleren in te stellen op dagelijks, wekelijks of maandelijks.

## Methoden voor incrementele replicatie gebruiken

Zoals hierboven vermeld, zijn lange updatetijden rechtstreeks gecorreleerd aan hoeveel gegevens opnieuw moeten worden gecontroleerd en worden gerepliceerd. [Incrementele replicatiemethoden](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) kan de hoeveelheid gegevens die tijdens de updatecyclus wordt verwerkt sterk verminderen. Waar mogelijk, adviseert Adobe het gebruiken van deze methodes of het wijzigen van uw gegevensbestand om een stijgende methode te steunen.

## Ongebruikte grafieken verwijderen uit dashboards

Aan het einde van de updatecyclus [!DNL Commerce Intelligence] voert een geheim voorgeheugenverrichting voor alle grafieken uit. In een cache worden gegevens opgeslagen zodat toekomstige verzoeken om informatie sneller kunnen worden voltooid. In [!DNL Commerce Intelligence], betekent dit dat dashboards snel geladen moeten worden omdat grafieken niet gegevens hoeven te vragen telkens als zij laden.

Sinds [!DNL Commerce Intelligence] voert alleen cachebewerkingen uit voor diagrammen die in een dashboard worden gevonden. Als u ongebruikte grafieken verwijdert uit uw dashboards, neemt de updatetijd af. Houd er rekening mee dat hetzelfde diagram zich op meerdere dashboards kan bevinden - raadpleeg uw team om ervoor te zorgen dat ongebruikte grafieken ook worden verwijderd.

>[!NOTE]
>
>Als u grafieken verwijdert van het dashboard, wordt het diagram niet verwijderd. U kunt [altijd opnieuw toevoegen](../data-user/dashboards/add-charts-dashboard.md).

## Uw database optimaliseren voor analyse

Naast het opnieuw evalueren van recheck frequenties, replicatiemethodes, en grafieknut, kunt u ook [uw database optimaliseren voor analyse](../best-practices/opt-db-analysis.md).

## Omloop omhoog

Als de update nog steeds traag lijkt, zelfs nadat u deze aanbevelingen hebt uitgevoerd [contact opnemen met het ondersteuningsteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
