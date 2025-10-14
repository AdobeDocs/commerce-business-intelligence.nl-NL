---
title: Verwachte spreadgegevens
description: Onderzoek de belangrijkste gegevenslijsten die u van Spree in uw  [!DNL Commerce Intelligence]  rekening kunt invoeren.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# [!DNL Spree] gegevens verwacht

Nadat u uw [&#x200B; opslag  [!DNL Spree]  hebt verbonden &#x200B;](../../../data-analyst/importing-data/integrations/spree.md), kunt u de [&#x200B; Manager van Data Warehouse &#x200B;](../../data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden van uw [!DNL Spree] platform voor analyse gemakkelijk te volgen.

Dit onderwerp verkent de belangrijkste gegevenslijsten die u van [!DNL Spree] in uw [!DNL Commerce Intelligence] rekening kunt invoeren, met inbegrip van verbindingen aan [&#x200B; extra documentatie &#x200B;](https://guides.spreecommerce.org/developer/addresses.html#address) over [!DNL Spree] gegevens.

| **de naam van de Lijst** | **Beschrijving** |
|-----|-----|
| `Users` | De tabel `users` bevat de accountgegevens voor geregistreerde klanten, zoals de e-mail, naam en registratiedatum van de persoon. Hierdoor kunt u verschillende klantsegmenten en hun koopgedrag analyseren. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | De tabel `orders` fungeert als basis voor al uw metingen op bestelniveau. Hier worden alle bestelgegevens van aankopen in uw [!DNL Spree] -winkel opgenomen, waaronder `completed\_at` (het tijdstempel van de bestelling) `user\_id` (id van geregistreerde gebruiker die de bestelling heeft geplaatst). Als de volgorde is gemaakt door een geregistreerde gebruiker, verwijst `user\_id` terug naar de tabel `users` voor analyse van het aankoopgedrag van de gebruiker. |
| `Line items` | De tabel `line\_items` is een onderliggend element van de tabel `orders` of `subscriptions` . Hiermee worden de regelitemgegevens van een bestelling of abonnement vastgelegd. Voor bestellingen met meerdere producten heeft elk product zijn eigen gegevensrij in deze tabel, inclusief een `product\_id` die u toestaat deze aan de `Products` -tabel te koppelen. |
| `Products` | In de tabel `products` worden alle productdetails van een verkoopbaar item in de Spree-catalogus vastgelegd. Dit staat u toe om uw lijn punt-vlakke metriek door productattributen te segmenteren. |
| `Subscriptions` | Als u de extensie [!DNL Spree] abonnementen hebt, bevat de tabel `subscriptions` de gegevens van elk abonnement, waaronder `created\_at` (de startdatum), `cancelled\_at` (de datum waarop een abonnement is geannuleerd) en de `interval` van het abonnement. |

{style="table-layout:auto"}

## Verwante:

* [Verbinding maken  [!DNL Spree]](../integrations/spree.md)
* [&#x200B; Reauthenticating integrations &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
