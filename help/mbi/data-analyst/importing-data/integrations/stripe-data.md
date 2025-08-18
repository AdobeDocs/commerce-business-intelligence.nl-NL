---
title: Stripe-gegevens verwacht
description: Bekijk de belangrijkste gegevenstabellen die u vanuit Stripe kunt importeren in Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# [!DNL Stripe] gegevens verwacht

Nadat [ u uw  [!DNL Stripe]  rekening ](../integrations/stripe.md) hebt verbonden, kunt u de [ Manager van Data Warehouse ](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.

In dit onderwerp worden de belangrijkste gegevenstabellen besproken die u vanuit [!DNL Stripe] kunt importeren in [!DNL Commerce Intelligence] . Nadat de installatie is voltooid, worden de volgende tabellen gemaakt in uw Data Warehouse. Klik op de koppelingen in de kolom Tabelnaam voor meer informatie over de kenmerken in elke tabel.

| **Naam van de Lijst** | **Beschrijving** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | De voorwerpen van de klant staan u toe om terugkomende kosten uit te voeren en veelvoudige kosten te volgen die met de zelfde klant worden geassocieerd. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Deze tabel bevat informatie over de kosten voor creditcards en betaalkaarten, zoals het bedrag, de valuta, de status, de klant-id en nog veel meer. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Deze lijst bevat informatie over een percentage- of afkoopkorting die u op een klant kunt toepassen. Coupons zijn alleen van toepassing op facturen; ze zijn niet van toepassing op eenmalige kosten. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Deze tabel bevat informatie over facturen, waaronder het verschuldigde bedrag, abonnementen, factuurposten, eventuele automatische correcties van de proratie en meer. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Deze tabel bevat de prijsgegevens voor verschillende producten en functieniveaus op uw site. U hebt bijvoorbeeld een abonnement van $10/maand voor basisfuncties en een abonnement van $20/maand voor premiumfuncties. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Deze lijst bevat de details van abonnementsplannen uw klanten tot behoren. Tot de kenmerken behoren de id van de klant, de status, geannuleerd/beëindigd op datums, het belastingpercentage, de proefgegevens en nog veel meer. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Gebeurtenissen geven u informatie over iets interessants dat in een account is gebeurd. [ wanneer een interessante gebeurtenis ](https://stripe.com/docs/api/events/types) voorkomt, wordt een nieuw gebeurtenisvoorwerp gecreeerd. Wanneer bijvoorbeeld de gebeurtenis `charge.succeeded` slaagt en een factuur niet kan worden betaald, wordt een gebeurtenis `invoice.payment\_failed` gemaakt. |

{style="table-layout:auto"}

>[!NOTE]
>
>Veel API-aanvragen kunnen ertoe leiden dat meerdere gebeurtenissen worden gemaakt. Als u bijvoorbeeld een abonnement voor een klant maakt, ontvangt u zowel een `customer.subscription.created` -gebeurtenis als een `charge.succeeded` -gebeurtenis.

## Verwante:

* [Verbinding maken  [!DNL Stripe]](../integrations/stripe.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
