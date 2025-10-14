---
title: MailChimp-gegevens importeren
description: Leer om gegevens te importeren MailChimp in  [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# [!DNL Mailchimp] -gegevens importeren

Als u een uitgebreid beeld wilt krijgen van uw campagnes, kunt u uw [!DNL Mailchimp] e-mailcampagnegegevens importeren in [!DNL Commerce Intelligence] . Als u het importeren wilt voltooien, moet u het volgende doen voor elke [!DNL Mailchimp] -campagne die u hebt:

## Gegevens voor openen exporteren {#opens}

1. Nadat u zich hebt aangemeld bij [!DNL Mailchimp] , gaat u naar de tab `Campaigns` .

   ![&#x200B; de invoer mailchimp 1 &#x200B;](../../../assets/import-mailchimp-1.png)

1. Klik op **[!UICONTROL View Report]** naast de naam van de campagne.

   ![&#x200B; invoer mailchimp 2 &#x200B;](../../../assets/import-mailchimp-2.png)

1. Klik op het **[!UICONTROL Opened]** nummer.

   ![&#x200B; de invoer mailchimp 3 &#x200B;](../../../assets/import-mailchimp-3.png)

1. Klik op **[!UICONTROL Export]** en sla het `.csv` -bestand op.

   U moet kolommen `primary key` , `date (mm/dd/yyyy)` en `campaign name` aan dit bestand toevoegen. Zorg ervoor dat `primary keys` uniek is voor elke rij.

   ![&#x200B; invoer mailchimp 4 &#x200B;](../../../assets/import-mailchimp-4.png)

## Klikgegevens exporteren {#clicks}

1. Navigeer terug naar het `View Report` -scherm voor de campagne.

1. Klik op het nummer dat `Clicked` bevat.

   ![&#x200B; invoer mailchimp 5 &#x200B;](../../../assets/import-mailchimp-5.png)

1. Klik op het nummer onder de kolom `Total Clicks` OR `Unique Clicks` .

   ![&#x200B; invoer mailchimp 6 &#x200B;](../../../assets/import-mailchimp-6.png)

1. Klik op **[!UICONTROL Export]** en sla het `.csv` -bestand op.

   U moet kolommen `Primary Key` , `date (mm/dd/yyyy)` , `campaign name` en `URL` aan dit bestand toevoegen. U hoeft niet de volledige URL toe te voegen, alleen iets dat u laat weten wat er is geklikt.

   ![&#x200B; de invoer mailchimp 7 &#x200B;](../../../assets/import-mailchimp-7.png)

1. Herhaal stap 3 en 4 voor elke URL waarop u in uw e-mail hebt geklikt, waarbij alle gegevens na afloop in hetzelfde `.csv` -bestand worden gecombineerd.

## Verzonden gegevens exporteren {#sent}

1. Ga naar de tab `Campaigns` van [!DNL Mailchimp] .

1. Klik op **[!UICONTROL View Report]** naast de naam van de campagne.

1. Klik op het nummer naast `Recipients` .

   ![&#x200B; de invoer mailchimp 8 &#x200B;](../../../assets/import-mailchimp-8.png)

1. Klik op **[!UICONTROL Export]** en sla het `.csv` -bestand op.

   U moet kolommen `Primary Key` , `date (mm/dd/yyyy)` en `campaign name` aan dit bestand toevoegen.

   ![&#x200B; de invoer mailchimp 9 &#x200B;](../../../assets/import-mailchimp-9.png)

## Bestanden voorbereiden voor uploaden naar [!DNL Commerce Intelligence] {#upload}

Elk bestand - `Opens` , `Clicks` en `Sent` - moet in [!DNL Commerce Intelligence] als afzonderlijk bestand worden geüpload. Adobe raadt u aan de bestanden een naam te geven met deze naamgevingsconventie: `MailChimp\_ACTION\_DATE` . Vervang `ACTION` door `Open` , `Click` of `Sent` en vervang `DATE` door de datum van export.

Wanneer u klaar bent om de bestanden te uploaden, gebruikt u de [`File Upload` functie &#x200B;](../connecting-data/using-file-uploader.md) om de gegevens over te brengen naar uw Data Warehouse.
