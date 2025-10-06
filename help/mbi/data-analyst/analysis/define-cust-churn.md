---
title: Bepaal klantenkring
description: Leer hoe u een dashboard instelt waarmee u het koor voor uw klanten van de transactie kunt definiëren.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Transactionele Klantenketen

Dit onderwerp toont aan hoe te opstelling een dashboard dat u helpt karn voor uw transactieklanten bepalen.

![ Klantkurn dashboard die klaringstarief en behoudmetriek tonen ](../../assets/churn-deashboard.png)

Deze analyse bevat [ geavanceerde berekende kolommen ](../data-warehouse-mgr/adv-calc-columns.md).

## Berekende kolommen

Te maken kolommen

* `customer_entity` table
* `Customer's lifetime number of orders`
* Selecteer een definitie: `Count`
* Selecteer een [!UICONTROL table]: `sales_flat_order`
* Selecteer een [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: verkoop_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Orders die worden geteld

* `sales_flat_order` table
* `Customer's lifetime number of orders`
* Een definitie selecteren: samengevoegde kolom
* Selecteer een [!UICONTROL table]: `customer_entity`
* Selecteer een [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Selecteer een definitie: `Age`
* Selecteer een [!UICONTROL column]: `created_at`

* **`Customer's order number`** wordt gecreeerd door een analist als deel van uw **[HET DEFINIËREN 2} kaartje van het KLOOFJE {]**
* **`Is customer's last order`** wordt gecreeerd door een analist als deel van uw **[HET DEFINIËREN 2} kaartje van het KLOOFJE {]**
* **`Seconds since previous order`** wordt gecreeerd door een analist als deel van uw **[HET DEFINIËREN 2} kaartje van het KLOOFJE {]**
* **`Months since order`** wordt gecreeerd door een analist als deel van uw **[HET DEFINIËREN 2} kaartje van het KLOOFJE {]**
* **`Months since previous order`** wordt gecreeerd door een analist als deel van uw **[HET DEFINIËREN 2} kaartje van het KLOOFJE {]**

## Metrisch

Geen nieuwe metriek!

>[!NOTE]
>
>Zorg ervoor om [ alle nieuwe kolommen als afmetingen aan metriek ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) toe te voegen alvorens nieuwe rapporten te bouwen.

## Rapporten

* **Aanvankelijke waarschijnlijkheid van de herhalingsorde**
* Metrisch A: Volgorde bij herhaling tijdens de hele tijd
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrisch B: Voltijdorders
* [!UICONTROL Metric]: aantal bestellingen

* [!UICONTROL Formula]: waarschijnlijkheid van eerste herhalingsvolgorde
* 
  [!UICONTROL-formule]: `A/B`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Herhaal orde kansingsmaanden sinds orde**
* Metrisch A: Volgorde van maanden sinds vorige orde (huid) herhalen
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrisch B: Laatste bestellingen per maand sinds bestelling (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Metrisch C: Alle-tijd herhalingsorders (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 
  [!UICONTROL Group door]: `Independent`

* Metrisch D: All-time last orders (hide)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 
  [!UICONTROL Group door]: `Independent`

* [!UICONTROL Formula]: waarschijnlijkheid van eerste herhalingsvolgorde
* 
  [!UICONTROL-formule]: `(C-A)/(C+D-A-B)`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Bovenkant weergeven.Onder: bovenste 24 categorieën, gesorteerd op categorienaam

* 
  [!UICONTROL Chart type]: `Line`

Het waarschijnlijkheidsrapport voor de eerste herhalingsvolgorde vertegenwoordigt de Totaal aantal herhalingsorders / Totaal aantal bestellingen. Elke order is een kans om een herhalingsvolgorde te maken; het aantal herhalingsorders is de subset van de orders die daadwerkelijk worden uitgevoerd.

De formule die u gebruikt, vereenvoudigt (Totaal aantal herhaalde orders die na X maanden zijn uitgevoerd)/ (Totaal aantal orders die minstens X maanden oud zijn). Het toont ons dat historisch gezien, aangezien het X maanden sinds een orde is geweest, er een Y% kans is dat de gebruiker een andere orde plaatst.

Zodra u uw dashboard hebt opgebouwd, de gemeenschappelijkste vraag is: Hoe gebruik ik dit om een kindrempelwaarde te bepalen?

**Er is geen &quot;één juist antwoord&quot;op dit.** Adobe raadt echter aan het punt te zoeken waar de lijn de waarde kruist die de helft is van de waarschijnlijkheid van de eerste herhaling. Dit is het punt waar u kunt zeggen &quot;Als een gebruiker een herhalingsorde gaat maken, zouden zij het waarschijnlijk tegen nu hebben gedaan.&quot; Uiteindelijk is het doel de drempel te selecteren waar het zinvol is om over te schakelen van &quot;retentie&quot; naar &quot;reactivering&quot;.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat kan lijken op de afbeelding boven aan de pagina

Als u in om het even welke vragen loopt terwijl het bouwen van deze analyse, of eenvoudig het Professionele team van de Diensten in dienst willen nemen, [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
