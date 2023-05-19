---
title: Streepgegevens verwacht
description: Onderzoek de belangrijkste gegevenslijsten die u van Stripe in de Intelligentie van de Handel kunt invoeren.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Verwacht [!DNL Stripe] data

Na [u hebt verbinding gemaakt met uw [!DNL Stripe] account](../integrations/stripe.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

Dit onderwerp verkent de belangrijkste gegevenslijsten die u van kunt invoeren [!DNL Stripe] in [!DNL Commerce Intelligence]. Nadat de opstelling wordt voltooid, zullen de volgende lijsten in uw Data Warehouse worden gecreeerd. Klik op de koppelingen in de kolom Tabelnaam voor meer informatie over de kenmerken in elke tabel.

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | De voorwerpen van de klant staan u toe om terugkomende kosten uit te voeren en veelvoudige kosten te volgen die met de zelfde klant worden geassocieerd. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Deze tabel bevat informatie over de kosten voor creditcards en betaalkaarten, zoals het bedrag, de valuta, de status, de klant-id en nog veel meer. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Deze lijst bevat informatie over een percentage- of afkoopkorting die u op een klant kunt toepassen. Coupons zijn alleen van toepassing op facturen; zij zijn niet van toepassing op eenmalige kosten. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Deze tabel bevat informatie over facturen, waaronder het verschuldigde bedrag, abonnementen, factuurposten, eventuele automatische correcties van de proratie en meer. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Deze tabel bevat de prijsgegevens voor verschillende producten en functieniveaus op uw site. U hebt bijvoorbeeld een abonnement van $10/maand voor basisfuncties en een abonnement van $20/maand voor premiumfuncties. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Deze lijst bevat de details van abonnementsplannen uw klanten tot behoren. Tot de kenmerken behoren de id van de klant, de status, geannuleerd/beëindigd op datums, het belastingpercentage, de proefgegevens en nog veel meer. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Gebeurtenissen geven u informatie over iets interessants dat in een account is gebeurd. [Wanneer een interessante gebeurtenis plaatsvindt](https://stripe.com/docs/api/events/types), wordt een nieuw gebeurtenisobject gemaakt. Bijvoorbeeld wanneer een last slaagt `charge.succeeded` gebeurtenis wordt gecreëerd; of wanneer een factuur niet kan worden betaald `invoice.payment\_failed` wordt gemaakt. |

{style="table-layout:auto"}

>[!NOTE]
>
>Veel API-aanvragen kunnen ertoe leiden dat meerdere gebeurtenissen worden gemaakt. Als u bijvoorbeeld een abonnement voor een klant maakt, ontvangt u beide `customer.subscription.created` en een  `charge.succeeded` gebeurtenis.

## Verwante:

* [Verbinding maken [!DNL Stripe]](../integrations/stripe.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
