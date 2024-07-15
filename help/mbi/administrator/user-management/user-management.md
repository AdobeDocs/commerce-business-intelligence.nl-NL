---
title: Adobe Commerce-gebruikers en -machtigingen beheren
description: Leer hoe je Commerce Intelligence-gebruikers beheert.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Gebruikersmachtigingen beheren

[!DNL Adobe Commerce Intelligence] is bedoeld als één bron van waarheid in uw hele organisatie. Elke gebruiker heeft hun eigen reeks dashboards die zij [ met andere gebruikers ](../../data-user/dashboards/share-dashboard-with-users.md) kunnen delen.

## Machtigingsniveaus gebruiker

In [!DNL Commerce Intelligence] zijn er drie algemene machtigingsniveaus die van toepassing zijn op gebruikers. Deze niveaus worden geselecteerd wanneer een account wordt gemaakt:

* `Admin`
* `Standard`
* `Read-Only`

Met deze machtigingen kunnen gebruikers bepaalde handelingen uitvoeren of toegang krijgen tot specifieke onderdelen van [!DNL Commerce Intelligence] . Hier volgt een tabel met wat elk machtigingsniveau kan doen in [!DNL Commerce Intelligence] :

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **creeer/beheer gebruikers** | ✔ |   |   |
| **creeer e-mailoverzichten** | ✔ | ✔ |   |
| **creeer/geef/deel dashboards** | ✔ | ✔ |   |
| **dashboards van de Mening** | ✔ | ✔ | ✔ |
| **creeer/geef/schrap visuele rapporten uit** | ✔ | ✔* |   |
| **creeer/geef/schrap SQL rapporten** uit | ✔ |  |   |
| **dashboards van de Kloon** | ✔ |   |   |
| **voeg/beheer integratie** toe | ✔ |   |   |
| **heb toegang tot de Manager van de Data Warehouse** | ✔ |   |   |
| **Synchroniseer/unsync lijsten en kolommen** | ✔ |   |   |
| **creeer/geef metriek** uit | ✔ |   |   |
| **creeer/geef filterreeksen uit** | ✔ |   |   |
| **creeer/geef berekende kolommen uit** | ✔ |   |   |
| **creeer lijst van afhankelijke rapporten** | ✔ |   |   |
| **Samenvatting van het Systeem van de Toegang** | ✔ |   |   |
| **montages van de Tijdzone van de Toegang** | ✔ |   |   |
| **het Factureren van de Toegang** | ✔ | ✔** |   |
| **Steun van het Contact** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_u kunt de toegang van de a **[!UICONTROL Standard]**gebruiker [ tot specifieke metriek ](../../administrator/user-management/restrict-metric-access.md) beperken._
>
>** [!UICONTROL Standard] _de gebruikers kunnen tot het Factureren met een extra toestemming toegang hebben plaatsend._
>
>**[!UICONTROL Read-Only]** de gebruikers kunnen __ dashboards slechts bekijken die met hen zijn gedeeld; zij kunnen om het even wat in [!DNL Commerce Intelligence] niet tot stand brengen of uitgeven, noch kunnen zij naar nieuwe dashboards aan hun rekening zoeken en toevoegen. Adobe raadt u aan een specifieke set dashboards te delen met **[!UICONTROL Read-Only]** -gebruikers die u of een ander teamlid onderhoudt. U kunt geen set dashboards klonen.

## Aanvullende machtigingen: facturering en technische {#billingtech}

Naast de algemene machtigingsniveaus bestaan er ook twee andere gebruikersaanduidingen: `Billing` en `Technical` . Deze aanwijzingen moeten worden gebruikt met de algemene machtigingsniveaus.

### Facturering

`Billing` -gebruikers hebben toegang tot de facturatiepagina en kunnen betalingsgegevens wijzigen. Ook kan de Adobe contact met hen opnemen voor factureringsvragen.

`Admin` -gebruikers hebben standaard toegang tot de tab `Billing` , maar `Standard` -gebruikers kunnen ook toegang krijgen als ze het selectievakje `Billing` in hun profiel hebben ingeschakeld.

![ het factureren ](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Technisch

`Technical` -gebruikers hebben geen specifieke rechten. Deze instelling markeert alleen een technische contactpersoon binnen uw organisatie. Deze gebruikers kunnen door de Adobe worden benaderd voor technische vragen.

`Admin` -gebruikers kunnen nieuwe gebruikers aan hun account toevoegen door op **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** te klikken en de aanwijzingen te volgen. Nadat de gebruiker in [!DNL Commerce Intelligence] is gemaakt, ontvangt de gelukkige persoon die u uitnodigt, e-mailinstructies over het voltooien van het accountinstellingsproces.

Op elk gewenst moment kan `Admins` alle gebruikers in hun account weergeven door op **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]** te klikken. Op deze pagina worden de machtigingen van de gebruiker weergegeven en de gegevens en dashboards waartoe deze toegang heeft.
