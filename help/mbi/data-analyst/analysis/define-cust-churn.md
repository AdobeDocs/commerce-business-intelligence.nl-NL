---
title: Bepaal klantenkring
description: Leer hoe u een dashboard instelt dat u zal helpen karn voor uw transactieklanten bepalen.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Transactionele Klantenketen

In dit artikel, tonen wij hoe te opstelling een dashboard dat u zal helpen karn voor uw transactieklanten bepalen.

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
* Bestellingen die we tellen

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
* Metrisch A: Alle herhaalde opdrachten
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrisch B: Alle tijdbestellingen
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

* Metrisch C: Alle tijden herhalen orden (verbergen)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Group door]: `Independent`

* Metrisch D: Alle laatste bestellingen bij tijd (verbergen)
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

De formule die wij gebruiken vereenvoudigt aan (het Totaal herhaalde orden die na X maanden voorkwamen)/ (het Totale aantal orden die minstens X maanden oud zijn). Het toont ons dat historisch gezien, aangezien het X maanden is sinds een orde, er een Y% kans is dat de gebruiker een andere orde zal plaatsen.

Zodra u uw dashboard hebt opgebouwd, is de gemeenschappelijkste vraag wij: Hoe gebruik ik dit om een kanteldrempel te bepalen?

**Er is geen &quot;één goed antwoord&quot;.** Nochtans, adviseren wij het punt vinden waar de lijn de waarde kruist die de helft van het aanvankelijke herhalingskanspercentage is. Dit is het punt waarop we kunnen zeggen: &quot;Als een gebruiker een herhalingsbestelling zou maken, zouden ze dat waarschijnlijk al gedaan hebben.&quot; Uiteindelijk is het doel de drempel te selecteren waar het zinvol is om over te schakelen van &quot;retentie&quot; naar &quot;reactivering&quot;.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het eindresultaat ziet er mogelijk uit als de afbeelding boven aan de pagina

Als u op vragen loopt terwijl u deze analyse bouwt, of eenvoudig ons professionele de dienstenteam wilt in dienst nemen, [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
