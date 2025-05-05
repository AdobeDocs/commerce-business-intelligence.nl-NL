---
title: Deelvenster Verbinden
description: Leer hoe u kunt analyseren hoe gebruikers door uw websites en apps navigeren en deze gebruiken.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Verbinden [!DNL Mixpanel]

>[!NOTE]
>
>Vereist [ toestemmingen Admin ](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Met [!DNL Mixpanel] kunt u analyseren hoe gebruikers door uw websites en apps navigeren en deze gebruiken. Als u goed kijkt naar gegevens over gebruikersgedrag, leidt dit tot slimmere beslissingen over ontwerp en ontwikkeling, wat over het algemeen een beter product betekent. Door [!DNL Mixpanel] aan [!DNL Commerce Intelligence] te verbinden, kunt u analyseren hoe uw gebruikers zich gedragen en hoe dat gedrag omzet oplevert.

Het aansluiten van uw [!DNL Mixpanel] gegevens op [!DNL Commerce Intelligence] een eenvoudig proces in drie stappen:

1. [Open de  [!DNL Mixpanel]  geloofsbrieven pagina in  [!DNL Commerce Intelligence]](#stepone)
1. [Haal uw  [!DNL Mixpanel]  API geloofsbrieven terug](#steptwo)
1. [Ga uw  [!DNL Mixpanel]  API geloofsbrieven in  [!DNL Commerce Intelligence]](#stepthree)

Als u dit proces wilt voltooien, moet u twee browservensters of tabbladen openen, een voor [!DNL Commerce Intelligence] en een voor uw [!DNL Mixpanel] -account.

## De pagina met [!DNL Mixpanel] referenties openen {#stepone}

Aan de slag:

1. Ga naar de pagina `Connections` onder **[!DNL Manage Data** > **Connections]** .

1. Klik op **[!UICONTROL Add a New Source]** rechts van het scherm boven de `Data Sources` -tabel.

1. Klik op het pictogram [!DNL Mixpanel] en open de pagina met referenties.

Laat deze pagina voorlopig open en schakel over naar het browservenster met uw [!DNL Mixpanel] -account.

## Uw [!DNL Mixpanel] API-referenties ophalen {#steptwo}

Als u zich nog niet hebt aangemeld bij uw [!DNL Mixpanel] -account, doet u dit en doet u het volgende:

1. Klik op **[!UICONTROL Account]** in de rechterbovenhoek.

1. Klik in het weergegeven dialoogvenster op **[!UICONTROL Projects]** .

1. De weergave van uw API-referenties:

![ het terugwinnen van de geloofsbrieven van Mixpanel API ](../../../assets/Mixpanel_API_creds.png)

Houd dit open, u hebt het nodig om dit op te pakken.

## Uw [!DNL Mixpanel] API-referenties invoeren in [!DNL Commerce Intelligence] {#stepthree}

1. Kopieer `API Key` en `Secret` naar de aanmeldingspagina van [!DNL Mixpanel] in [!DNL Commerce Intelligence] .
1. Klik op **[!UICONTROL Connect to Mixpanel]** om de installatie te voltooien.

Als de verbinding succesvol is, a _Succes!_ wordt boven aan de pagina weergegeven.

### Verwante

* [Verwachte  [!DNL Mixpanel]  gegevens](../integrations/mixpanel-data.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
