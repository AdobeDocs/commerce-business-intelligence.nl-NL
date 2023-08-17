---
title: Verwachte spreadgegevens
description: Bekijk de belangrijkste gegevenstabellen die u vanuit Spreiding kunt importeren in uw [!DNL Commerce Intelligence] account.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Verwacht [!DNL Spree] data

Nadat u [heeft uw [!DNL Spree] winkel](../../../data-analyst/importing-data/integrations/spree.md), kunt u de [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) om relevante gegevensvelden gemakkelijk van uw [!DNL Spree] platform voor analyse.

Dit onderwerp verkent de belangrijkste gegevenslijsten die u van kunt invoeren [!DNL Spree] in uw [!DNL Commerce Intelligence] account, inclusief koppelingen naar [aanvullende documentatie](https://guides.spreecommerce.org/developer/addresses.html#address) info [!DNL Spree] gegevens.

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| `Users` | De `users` de tabel bevat de accountgegevens voor geregistreerde klanten, waaronder de e-mail, naam en registratiedatum van de persoon. Hierdoor kunt u verschillende klantsegmenten en hun koopgedrag analyseren. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | De `orders` tabel fungeert als de basis voor al uw metingen op orderniveau. Hier worden alle bestelgegevens van aankopen van uw [!DNL Spree] winkel, inclusief `completed\_at` (tijdstempel van de bestelling), `user\_id` (id van geregistreerde gebruiker die de bestelling heeft geplaatst). Als de bestelling is gemaakt door een geregistreerde gebruiker, `user\_id` koppelingen terug naar de `users` tabel voor analyse van het aankoopgedrag van gebruikers. |
| `Line items` | De `line\_items` tabel is een onderliggend element van een van de `orders` tabel of `subscriptions`. Hiermee worden de regelitemgegevens van een bestelling of abonnement vastgelegd. Voor bestellingen met meerdere producten heeft elk product zijn eigen gegevensrij in deze tabel, inclusief een `product\_id` zodat je het aan de `Products` tabel. |
| `Products` | De `products` in de tabel worden alle productgegevens van een verkoopbaar item in de Spree-catalogus vastgelegd. Dit staat u toe om uw lijn punt-vlakke metriek door productattributen te segmenteren. |
| `Subscriptions` | Als u een [!DNL Spree] abonnementsextensie, de `subscriptions` de tabel bevat de gegevens van elk individueel abonnement, inclusief `created\_at` (de begindatum), `cancelled\_at` (de datum waarop een abonnement is geannuleerd) en de `interval` van het abonnement. |

{style="table-layout:auto"}

## Verwante:

* [Verbinding maken [!DNL Spree]](../integrations/spree.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
