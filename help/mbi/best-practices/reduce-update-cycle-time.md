---
title: De tijd van de updatecyclus verkorten
description: Leer hoe u de updatecyclus verkort.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Verminder de verwerkingstijd van de updatecyclus

[!DNL Adobe Commerce Intelligence] synchroniseert de hele dag met uw database om nieuwe gegevens te repliceren, zodat op de dashboards altijd de meest recente informatie wordt weergegeven.

Veel factoren kunnen een reeds lange updatetijd vergroten. Bepaalde replicatiemethodes, hogere recheck frequenties, en het aantal dashboards en grafieken zijn enkel een paar contribuanten. In deze onderwerpen worden enkele aanbevolen procedures besproken om de updatetijden te verkorten.

## Frequentie voor opnieuw controleren verlagen

In een gegevensbestandlijst, kunnen er gegevenskolommen met veranderlijke waarden zijn. Bijvoorbeeld, in een **orde** lijst zou er een kolom kunnen zijn genoemd **status**. Wanneer een volgorde voor het eerst naar de database wordt geschreven, bevat de statuskolom mogelijk de waarde `pending` . De orde wordt herhaald in uw [ Data Warehouse ](../data-analyst/data-warehouse-mgr/tour-dwm.md) met deze `pending` waarde.

De veranderlijke kolommen moeten [ opnieuw gecontroleerd voor bijgewerkte waarden ](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) in tijd zijn. [!DNL Commerce Intelligence] controleert deze kolommen standaard opnieuw tijdens elke update, maar als er een grote hoeveelheid gegevens is die opnieuw moet worden gecontroleerd en gerepliceerd, kan dit een negatief effect hebben op de updatetijd. In plaats van tijdens elke update opnieuw te controleren, raadt Adobe aan de frequentie voor het opnieuw controleren in te stellen op dagelijks, wekelijks of maandelijks.

## Methoden voor incrementele replicatie gebruiken

Zoals hierboven vermeld, zijn lange updatetijden rechtstreeks gecorreleerd aan hoeveel gegevens opnieuw moeten worden gecontroleerd en worden gerepliceerd. [ de Incrementele replicatiemethodes ](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) kunnen de hoeveelheid gegevens zeer verminderen die tijdens de updatecyclus worden verwerkt. Indien mogelijk raadt Adobe u aan deze methoden te gebruiken of uw database te wijzigen ter ondersteuning van een incrementele methode.

## Ongebruikte grafieken verwijderen uit dashboards

Aan het einde van de updatecyclus voert [!DNL Commerce Intelligence] een cachebewerking uit voor alle grafieken. In een cache worden gegevens opgeslagen zodat toekomstige verzoeken om informatie sneller kunnen worden voltooid. In [!DNL Commerce Intelligence] betekent dit dat dashboards snel worden geladen, omdat grafieken niet telkens opnieuw gegevens hoeven te vragen wanneer ze worden geladen.

Aangezien [!DNL Commerce Intelligence] alleen cachebewerkingen uitvoert voor grafieken die in een dashboard worden gevonden, neemt het verwijderen van ongebruikte grafieken uit uw dashboards de updatetijd in beslag. Houd er rekening mee dat hetzelfde diagram zich op meerdere dashboards kan bevinden - raadpleeg uw team om ervoor te zorgen dat ongebruikte grafieken ook worden verwijderd.

>[!NOTE]
>
>Als u grafieken verwijdert van het dashboard, wordt het diagram niet verwijderd. U kunt [ het terug op elk ogenblik ](../data-user/dashboards/add-charts-dashboard.md) toevoegen.

## Uw database optimaliseren voor analyse

Naast het opnieuw evalueren van recheck frequenties, replicatiemethodes, en grafieknut, kunt u uw gegevensbestand voor analyse [ ook ](../best-practices/opt-db-analysis.md) optimaliseren.

## Omloop omhoog

Als uw updatetijd nog langzaam lijkt zelfs na het uitvoeren van deze aanbevelingen, [ contacteer het steunteam ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
