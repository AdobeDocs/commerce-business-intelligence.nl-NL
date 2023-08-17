---
title: Rapportage van helpdesk voor Zendesk
description: Meer informatie over uw meest gewaardeerde verwijzingskanalen.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Helpdesk rapporteert voor [!DNL Zendesk]

>[!NOTE]
>
>Dit is alleen beschikbaar voor clients die zich op de `Pro` de nieuwe architectuur plannen en gebruiken. U bevindt zich op de nieuwe architectuur als u de `Data Warehouse Views` sectie beschikbaar na het selecteren `Manage Data` van de hoofdwerkbalk.

Uw [!DNL Zendesk] gegevens met uw transactionele gegevensbestand is een uitstekende manier om beter te begrijpen hoe uw klanten met uw verkoop of klantensuccesteams in wisselwerking staan. Het helpt u ook weten welk type klanten uw steunplatform gebruiken. In dit onderwerp wordt getoond hoe u een dashboard kunt instellen om gedetailleerde rapporten over uw [!DNL Zendesk] prestaties en tijd in uw transactieklanten.

Voordat u aan de slag gaat, wilt u verbinding maken met de [[!DNL Zendesk]](../integrations/zendesk.md). Deze analyse bevat [geavanceerd berekende kolommen](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Aan de slag

### Te traceren kolommen

* `audits` table
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` table
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` table
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` table
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Filtersets die moeten worden gemaakt

* `[!DNL Zendesk] Tickets` table
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Berekende kolommen

### Te maken kolommen

* **`[!DNL Zendesk] user's`** table
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` dan `Yes` wanneer `B` is niet `null` en `B` leuk `%@magento.com` dan `Yes` else `No` end

      * Vervangen `@magento.com` met uw domein

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** table
   * Selecteer een definitie: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] users`
   * Selecteer een [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** table
   * Selecteer een definitie: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Selecteer een definitie: `Exists`
   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** table
   * Selecteer een definitie: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] users`
   * Selecteer een [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Selecteer een definitie: `Joined Column`
   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] users`
   * Selecteer een [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Selecteer een definitie: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Selecteer een [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` gewijzigd in `solved = 1`

   * Selecteer een definitie: `Min`
   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Selecteer een [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` minus `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` minus `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;Zelfde tabel > Berekening&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Geheel getal

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Zelfde tabel > Berekening&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` – `String`

* **`customer_entity`** table
   * Selecteer een definitie: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 
     [!UICONTROL One]: `customer_entity.email`

   * Selecteer een [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Zelfde tabel > Berekening&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** table
   * Selecteer een definitie: `Joined Column`
   * Selecteer een [!UICONTROL table]: `customer_entity`
   * Selecteer een [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Metrisch

* **[!DNL Zendesk]Nieuwe tickets**
   * `Tickets we count`

* In de **`[!DNL Zendesk] tickets`** table
* Deze maatstaf voert een **Aantal**
* Op de **`id`** kolom
* Besteld door de **`created_at`** tijdstempel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Opgeslagen tickets**
   * `Tickets we count`
   * status IN `closed, solved`

* In de **`[!DNL Zendesk] tickets`** table
* Deze maatstaf voert een **Aantal**
* Op de **`id`** kolom
* Besteld door de **`created_at`** tijdstempel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Afzonderlijke gebruikers die tickets aanvragen**
   * `Tickets we count`

* In de **`[!DNL Zendesk] tickets`** table
* Deze maatstaf voert een **Verschil aantal**
* Op de **`requester_id`** kolom
* Besteld door de **`created_at`** tijdstempel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Gemiddelde/mediane resolutietijd van tickets**
   * `Tickets we count`
   * status IN `closed, solved`

* In de **`[!DNL Zendesk] tickets`** table
* Deze maatstaf voert een **Gemiddelde (of Mediaan)**
* Op de **`Seconds to resolution`** kolom
* Besteld door de **`created_at`** tijdstempel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Gemiddelde/mediane tijd tot eerste respons**
   * Tickets die worden geteld
   * status IN gesloten, opgeloste

* In de **`[!DNL Zendesk] tickets`** table
* Deze maatstaf voert een **Gemiddelde (of Mediaan)**
* Op de **`Seconds to first response`** kolom
* Besteld door de **`created_at`** tijdstempel
* [!UICONTROL Filter]:

>[!NOTE]
>
>Zorg ervoor dat [alle nieuwe kolommen als afmetingen toevoegen aan metriek](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) alvorens nieuwe rapporten op te stellen.

### Rapporten

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `new, open, pending`

* Metrisch `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Metrisch `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Metrisch `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Metrisch `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* Metrisch `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* Metrisch `A`: `New tickets`
* Metrisch `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Metrisch `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Metrisch `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* Metrisch `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* Metrisch `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Metrisch `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Metrisch `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 
     [!UICONTROL Metric]: Users

* Metrisch `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
