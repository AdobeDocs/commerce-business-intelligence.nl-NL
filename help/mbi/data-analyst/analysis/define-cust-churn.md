---
title: Bepaal klantenkring
description: Leer hoe u een dashboard instelt waarmee u het koor voor uw klanten van de transactie kunt definiëren.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Transactionele Klantenketen

Dit onderwerp toont aan hoe te opstelling een dashboard dat u helpt karn voor uw transactieklanten bepalen.

![](../../assets/churn-deashboard.png)

Deze analyse bevat [geavanceerd berekende kolommen](../data-warehouse-mgr/adv-calc-columns.md).

## Berekende kolommen

Te maken kolommen

* `customer_entity` table
* `Customer's lifetime number of orders`
* Selecteer een definitie: `Count`
* Selecteer een [!UICONTROL table]: `sales_flat_order`
* Selecteer een [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entiteit.entiteit_id
* [!UICONTROL Filter]:
* Orders die worden geteld

* `sales_flat_order` table
* `Customer's lifetime number of orders`
* Selecteer een definitie: Samengevoegde kolom
* Selecteer een [!UICONTROL table]: `customer_entity`
* Selecteer een [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Selecteer een definitie: `Age`
* Selecteer een [!UICONTROL column]: `created_at`

* **`Customer's order number`** wordt gemaakt door een analist als onderdeel van uw **[CHURN DEFINIËREN]** kaartje
* **`Is customer's last order`** wordt gemaakt door een analist als onderdeel van uw **[CHURN DEFINIËREN]** kaartje
* **`Seconds since previous order`** wordt gemaakt door een analist als onderdeel van uw **[CHURN DEFINIËREN]** kaartje
* **`Months since order`** wordt gemaakt door een analist als onderdeel van uw **[CHURN DEFINIËREN]** kaartje
* **`Months since previous order`** wordt gemaakt door een analist als onderdeel van uw **[CHURN DEFINIËREN]** kaartje

## Metrisch

Geen nieuwe metriek!

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

## Rapporten

* **Waarschijnlijk eerste herhalingsvolgorde**
* Metrisch A: Volgorde voor herhalingen bij alle tijd
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrisch B: Volgorde in alle tijd
* [!UICONTROL Metric]: Aantal orders

* [!UICONTROL Formula]: Waarschijnlijk eerste herhalingsvolgorde
* 
  [!UICONTROL-formule]: `A/B`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Herhaal de waarschijnlijkheid van de volgorde van maanden sinds de bestelling**
* Metrisch A: Volgorde van maanden sinds vorige volgorde herhalen (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrisch B: Laatste bestellingen per maand sinds bestelling (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Metrisch C: Volgorde voor herhaalde herhalingen (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 
  [!UICONTROL Group door]: `Independent`

* Metrisch D: Laatste bestellingen bij volledige uitvoering (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 
  [!UICONTROL Group door]: `Independent`

* [!UICONTROL Formula]: Waarschijnlijk eerste herhalingsvolgorde
* 
  [!UICONTROL-formule]: `(C-A)/(C+D-A-B)`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Boven weergeven.onder: Top 24 categorieën, gesorteerd op categorienaam

* 
  [!UICONTROL Chart type]: `Line`

Het waarschijnlijkheidsrapport voor de eerste herhalingsvolgorde vertegenwoordigt de Totaal aantal herhalingsorders / Totaal aantal bestellingen. Elke order is een mogelijkheid om een herhalingsbevel te geven; het aantal herhalingsorders is de subset van die welke daadwerkelijk worden uitgevoerd .

De formule die u gebruikt, vereenvoudigt (Totaal aantal herhaalde orders die na X maanden zijn uitgevoerd)/ (Totaal aantal orders die minstens X maanden oud zijn). Het toont ons dat historisch gezien, aangezien het X maanden sinds een orde is geweest, er een Y% kans is dat de gebruiker een andere orde plaatst.

Nadat u het dashboard hebt opgebouwd, wordt de meest voorkomende vraag gesteld: Hoe gebruik ik dit om een kanteldrempel te bepalen?

**Er is geen &quot;één goed antwoord&quot;.** Adobe raadt echter aan het punt te zoeken waar de lijn de waarde kruist die de helft is van de waarschijnlijkheid bij eerste herhaling. Dit is het punt waar u kunt zeggen &quot;Als een gebruiker een herhalingsorde gaat maken, zouden zij het waarschijnlijk tegen nu hebben gedaan.&quot; Uiteindelijk is het doel de drempel te selecteren waar het zinvol is om over te schakelen van &quot;retentie&quot; naar &quot;reactivering&quot;.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan lijken op de afbeelding boven aan de pagina

Als u op om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten wilt in dienst nemen, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
