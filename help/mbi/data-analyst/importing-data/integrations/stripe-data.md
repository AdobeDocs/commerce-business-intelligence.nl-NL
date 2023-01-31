---
title: Streepgegevens verwacht
description: De belangrijkste gegevenstabellen verkennen die u kunt importeren van Stripe naar [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Verwacht [!DNL Stripe] data

Na [u hebt verbinding gemaakt met uw [!DNL Stripe] account](../integrations/stripe.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

In dit artikel bekijken we de belangrijkste gegevenstabellen waaruit u kunt importeren [!DNL Stripe] in [!DNL MBI]. Nadat de opstelling wordt voltooid, zullen de volgende lijsten in uw gegevenspakhuis worden gecreeerd. Klik op de koppelingen in de kolom Tabelnaam voor meer informatie over de kenmerken in elke tabel.

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/api/curl#customer_object) | De voorwerpen van de klant staan u toe om terugkomende kosten uit te voeren en veelvoudige kosten te volgen die met de zelfde klant worden geassocieerd. |
| [`Charges`](https://stripe.com/docs/api/curl#charge_object) | Deze tabel bevat informatie over de kosten voor creditcards en betaalkaarten, zoals het bedrag, de valuta, de status, de klant-id en nog veel meer. |
| [`Coupons`](https://stripe.com/docs/api/curl#coupon_object) | Deze tabel bevat informatie over een korting die u op een bepaald percentage of bedrag wilt toepassen op een klant. Merk op dat coupons alleen van toepassing zijn op facturen; zij zijn niet van toepassing op eenmalige kosten. |
| [`Invoices`](https://stripe.com/docs/api/curl#invoice_object) | Deze tabel bevat informatie over facturen, waaronder het verschuldigde bedrag, abonnementen, factuurposten, eventuele automatische correcties van de proratie en meer. |
| [`Plans`](https://stripe.com/docs/api/curl#plan_object) | Deze tabel bevat de prijsgegevens voor verschillende producten en functieniveaus op uw site. U hebt bijvoorbeeld een abonnement van $10/maand voor basisfuncties en een abonnement van $20/maand voor premiumfuncties. |
| [`Subscriptions`](https://stripe.com/docs/api/curl#subscription_object) | Deze lijst bevat de details van abonnementsplannen uw klanten tot behoren. Tot de kenmerken behoren de id van de klant, de status, geannuleerd/beëindigd op datums, het belastingpercentage, de proefgegevens en nog veel meer. |
| [`Events`](https://stripe.com/docs/api/curl#event_object) | Gebeurtenissen geven u informatie over iets interessants dat zojuist in een account is gebeurd. [Wanneer een interessante gebeurtenis plaatsvindt](https://stripe.com/docs/api/curl#event_types), wordt een nieuw gebeurtenisobject gemaakt. Bijvoorbeeld wanneer een last slaagt `charge.succeeded` gebeurtenis wordt gecreëerd; of wanneer een factuur niet kan worden betaald `invoice.payment\_failed` wordt gemaakt. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Veel API-aanvragen kunnen ertoe leiden dat meerdere gebeurtenissen worden gemaakt. Als u bijvoorbeeld een nieuw abonnement voor een klant maakt, ontvangt u beide `customer.subscription.created` en een  `charge.succeeded` gebeurtenis.

## Verwante:

* [Verbinding maken [!DNL Stripe]](../integrations/stripe.md)
* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151)
