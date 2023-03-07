---
title: Connect Zendesk
description: Leer hoe u uw helpdeskrapportage kunt consolideren in [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Verbinden [!DNL Zendesk]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Uw [!DNL Zendesk] met gegevens kunt u uw helpdeskrapportage consolideren in [!DNL MBI]. Hierdoor kunt u de klantenondersteuning optimaliseren en de prestaties van de helpdesk bewaken, naast uw inkomsten.

Uw [!DNL Zendesk] gegevens zijn een eenvoudig proces in drie stappen:

1. [Open de [!DNL Zendesk] aanmeldingspagina in [!DNL MBI]](#stepone)
1. [Uw [!DNL Zendesk] API-token](#steptwo)
1. [Voer uw [!DNL Zendesk] aanmeldingsgegevens en token in [!DNL MBI]](#stepthree)

Als u dit proces wilt voltooien, moet u twee browservensters of tabbladen openen - één voor [!DNL MBI], de andere optie voor uw [!DNL Zendesk] account.

## Open de [!DNL Zendesk] aanmeldingspagina in [!DNL MBI] {#stepone}

1. Ga naar de `Integrations` pagina onder **[!UICONTROL Manage Data** > ** Gegevensbronnen **> **Integraties]**.
1. Klikken **[!UICONTROL Add Integration]**, die zich aan de rechterkant van het scherm bevindt.
1. Klik op de knop [!DNL Zendesk] pictogram. Hierdoor wordt het [!DNL Zendesk] aanmeldingspagina.

## Uw [!DNL Zendesk] API-token {#steptwo}

1. In het venster/tabblad waar u zich hebt aangemeld bij uw [!DNL Zendesk] op het pictogram Instellingen (versnelling) in de linkerbenedenhoek van het scherm.
1. Wanneer de `Settings` weergegeven menu, zoekt u de `Channels` sectie. Klikken **[!UICONTROL API]** in deze afdeling.
1. In de `Token Access` van deze pagina klikt u op het selectievakje naast `Enabled`. Een lijst met Active API Tokens die worden weergegeven.
1. Klikken **[!UICONTROL Add New Token]**.
1. Voer desgevraagd een label voor het token in. Adobe raadt u aan `MBI`In één oogopslag weet u dus welke toepassing de token gebruikt.
1. Klikken **[!UICONTROL Create]**.
1. Er wordt een API-token gemaakt. Kopieer dit token; het zal in de volgende stap worden gebruikt .

## Enter [!DNL Zendesk] aanmeldingsgegevens en API-token in [!DNL MBI] {#stepthree}

1. Voer uw [!DNL Zendesk] site-voorvoegsel en aanmeldings-e-mail in de [!DNL Zendesk] aanmeldingspagina in [!DNL MBI].
1. Voer uw API-token in.
1. Klikken **[!UICONTROL Save & Connect]**. Als de verbinding is gelukt, kunt u *Verbinding gelukt!* wordt boven in het scherm weergegeven.

## Verwante:

* [Verwacht [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
