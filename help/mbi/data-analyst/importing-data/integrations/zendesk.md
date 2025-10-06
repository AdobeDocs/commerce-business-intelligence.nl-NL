---
title: Connect Zendesk
description: Leer hoe te om uw helpdesk rapportering in  [!DNL Commerce Intelligence] te consolideren.
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# Verbinden [!DNL Zendesk]

>[!NOTE]
>
>Vereist [&#x200B; toestemmingen Admin &#x200B;](../../../administrator/user-management/user-management.md).

![&#x200B; het embleem van Zendesk &#x200B;](../../../assets/Zendesk_logo.png)

Door uw [!DNL Zendesk] -gegevens te verbinden, kunt u de helpdeskrapportage consolideren in [!DNL Commerce Intelligence] . Hierdoor kunt u de klantenondersteuning optimaliseren en de prestaties van de helpdesk bewaken, naast uw inkomsten.

Het verbinden van uw [!DNL Zendesk] gegevens is een eenvoudig proces in drie stappen:

1. [Open de  [!DNL Zendesk]  geloofsbrieven pagina in  [!DNL Commerce Intelligence]](#stepone)
1. [Haal uw  [!DNL Zendesk]  API Token terug](#steptwo)
1. [Ga uw  [!DNL Zendesk]  login info en Token binnen  [!DNL Commerce Intelligence] in](#stepthree)

Als u dit proces wilt voltooien, moet u twee browservensters of tabbladen openen: een voor [!DNL Commerce Intelligence] en een voor uw [!DNL Zendesk] -account.

## Open de pagina met [!DNL Zendesk] referenties in [!DNL Commerce Intelligence] {#stepone}

1. Ga naar de `Integrations` pagina onder **[!UICONTROL Manage Data** > **&#x200B; Gegevensbronnen &#x200B;**> **Integraties]**.
1. Klik op **[!UICONTROL Add Integration]** aan de rechterkant van het scherm.
1. Klik op het pictogram [!DNL Zendesk] . Hierdoor wordt de aanmeldingspagina van [!DNL Zendesk] geopend.

## Uw API-token [!DNL Zendesk] ophalen {#steptwo}

1. Klik in het venster/tabblad waar u bent aangemeld bij uw [!DNL Zendesk] -account op het pictogram Instellingen (versnelling) in de linkerbenedenhoek van het scherm.
1. Zoek de sectie `Settings` wanneer het menu `Channels` wordt weergegeven. Klik op **[!UICONTROL API]** in deze sectie.
1. Klik in de sectie `Token Access` van deze pagina op het selectievakje naast `Enabled` . Een lijst met Active API Tokens die worden weergegeven.
1. Klik op **[!UICONTROL Add New Token]**.
1. Voer desgevraagd een label voor het token in. Adobe raadt u aan `Commerce Intelligence` te gebruiken, zodat u in één oogopslag weet welke toepassing het token gebruikt.
1. Klik op **[!UICONTROL Create]**.
1. Er wordt een API-token gemaakt. Kopieer deze token; deze wordt in de volgende stap gebruikt.

## Voer [!DNL Zendesk] aanmeldingsgegevens en API-token in [!DNL Commerce Intelligence] {#stepthree}

1. Voer het voorvoegsel en de aanmelding van de [!DNL Zendesk] -site in op de pagina met [!DNL Zendesk] referenties [!DNL Commerce Intelligence] .
1. Voer uw API-token in.
1. Klik op **[!UICONTROL Save & Connect]**. Als de verbinding succesvol is, succesvol a *Verbinding!* wordt boven in het scherm weergegeven.

## Verwante:

* [Verwachte  [!DNL Zendesk]  gegevens](../integrations/exp-zendesk-data.md)
* [&#x200B; Reauthenticating integrations &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
