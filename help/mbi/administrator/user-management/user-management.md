---
title: Adobe Commerce-gebruikers en -machtigingen beheren
description: Leer hoe u de gebruikers van de Commerce Intelligence beheert.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Gebruikersmachtigingen beheren

[!DNL Adobe Commerce Intelligence] is bedoeld als één enkele bron van waarheid in uw organisatie. Elke gebruiker heeft zijn eigen set dashboards die hij kan [delen met andere gebruikers](../../data-user/dashboards/share-dashboard-with-users.md).

## Machtigingsniveaus gebruiker

In [!DNL Commerce Intelligence]Er zijn drie algemene machtigingsniveaus die van toepassing zijn op gebruikers. Deze niveaus worden geselecteerd wanneer een account wordt gemaakt:

* `Admin`
* `Standard`
* `Read-Only`

Met deze machtigingen kunnen gebruikers bepaalde handelingen uitvoeren of toegang krijgen tot specifieke onderdelen van [!DNL Commerce Intelligence]. Hier is een lijst van wat elk toestemmingsniveau binnen kan doen [!DNL Commerce Intelligence]:

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Gebruikers maken/beheren** | ✔ |  |  |
| **E-mailsamenvattingen maken** | ✔ | ✔ |  |
| **Dashboards maken/bewerken/delen** | ✔ | ✔ |  |
| **dashboards weergeven** | ✔ | ✔ | ✔ |
| **Visuele rapporten maken/bewerken/verwijderen** | ✔ | ✔* |  |
| **SQL-rapporten maken/bewerken/verwijderen** | ✔ |  |  |
| **Kloondashboards** | ✔ |  |  |
| **Integraties toevoegen/beheren** | ✔ |  |  |
| **Toegang tot de Manager van de Data Warehouse** | ✔ |  |  |
| **Tabellen en kolommen synchroniseren/desynchroniseren** | ✔ |  |  |
| **Metrisch maken/bewerken** | ✔ |  |  |
| **Filtersets maken/bewerken** | ✔ |  |  |
| **Berekende kolommen maken/bewerken** | ✔ |  |  |
| **Lijst met afhankelijke rapporten maken** | ✔ |  |  |
| **Overzicht van toegangssystemen** | ✔ |  |  |
| **Toegang tot tijdzone-instellingen** | ✔ |  |  |
| **Facturering openen** | ✔ | ✔** |  |
| **Contact opnemen met ondersteuning** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_U kunt een **[!UICONTROL Standard]**gebruikers [toegang tot specifieke meetgegevens](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _gebruikers hebben toegang tot facturering met een extra machtigingsinstelling._
>
>**[!UICONTROL Read-Only]** gebruikers kunnen alleen _weergave_ dashboards die met hen zijn gedeeld; ze kunnen niets maken of bewerken in [!DNL Commerce Intelligence]en kunnen ze ook geen nieuwe dashboards zoeken en aan hun account toevoegen. Adobe raadt u aan een specifieke set dashboards te delen met **[!UICONTROL Read-Only]** gebruikers die u of een ander lid van uw team onderhoudt. U kunt geen set dashboards klonen.

## Aanvullende machtigingen: Facturering en technische {#billingtech}

Naast de algemene machtigingsniveaus bestaan er nog twee andere gebruikersbenamingen: `Billing` en `Technical`. Deze aanwijzingen moeten worden gebruikt met de algemene machtigingsniveaus.

### Facturering

`Billing` gebruikers hebben toegang tot de facturatiepagina en kunnen betalingsgegevens wijzigen. Adobe kan ook contact met hen opnemen voor factureringsvragen.

`Admin` gebruikers hebben toegang tot `Billing` standaard op, maar `Standard` gebruikers kunnen ook toegang krijgen als zij beschikken over `Billing` Schakel het selectievakje in in het profiel.

![facturering](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Technisch

`Technical` gebruikers hebben geen specifieke machtigingen voor deze gebruikers - deze instelling markeert alleen een technische contactpersoon binnen uw organisatie. Adobe kan contact met deze gebruikers opnemen voor technische vragen.

`Admin` gebruikers kunnen nieuwe gebruikers aan hun account toevoegen door op **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** en volgt u de aanwijzingen. Nadat de gebruiker binnen is gecreeerd [!DNL Commerce Intelligence]De gelukkige persoon die u uitnodigt, ontvangt e-mailinstructies over hoe u het installatieproces van de account kunt voltooien.

Op elk gewenst moment `Admins` kan alle gebruikers in hun account bekijken door op **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Op deze pagina worden de machtigingen van de gebruiker weergegeven en de gegevens en dashboards waartoe deze toegang heeft.
