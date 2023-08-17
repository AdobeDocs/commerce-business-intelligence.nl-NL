---
title: Deelvenster Verbinden
description: Leer hoe u kunt analyseren hoe gebruikers door uw websites en apps navigeren en deze gebruiken.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Verbinden [!DNL Mixpanel]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Met [!DNL Mixpanel]kunt u analyseren hoe gebruikers door uw websites en apps navigeren en deze gebruiken. Als u goed kijkt naar gegevens over gebruikersgedrag, leidt dit tot slimmere beslissingen over ontwerp en ontwikkeling, wat over het algemeen een beter product betekent. Verbinding maken [!DNL Mixpanel] tot [!DNL Commerce Intelligence] Hiermee kunt u analyseren hoe uw gebruikers zich gedragen en hoe dat gedrag omzet oplevert.

Uw [!DNL Mixpanel] gegevens naar [!DNL Commerce Intelligence] een eenvoudig proces in drie stappen:

1. [Open de [!DNL Mixpanel] pagina met referenties in [!DNL Commerce Intelligence]](#stepone)
1. [Uw gegevens ophalen [!DNL Mixpanel] API-referenties](#steptwo)
1. [Voer uw [!DNL Mixpanel] API-referenties in [!DNL Commerce Intelligence]](#stepthree)

Als u dit proces wilt voltooien, moet u twee browservensters of tabbladen openen, één voor [!DNL Commerce Intelligence] en de andere [!DNL Mixpanel] account.

## Het openen van de [!DNL Mixpanel] pagina met referenties {#stepone}

Aan de slag:

1. Ga naar de `Connections` pagina onder **[!DNL Manage Data** > **Connections]**.

1. Klikken **[!UICONTROL Add a New Source]**, die zich rechts boven het scherm bevinden `Data Sources` tabel.

1. Klik op de knop [!DNL Mixpanel] en wordt de pagina met referenties geopend.

Laat deze pagina voorlopig open en schakel over naar het browservenster met uw [!DNL Mixpanel] account.

## Uw [!DNL Mixpanel] API-referenties {#steptwo}

Als u zich niet hebt aangemeld bij uw [!DNL Mixpanel] nog, doe dit en doe dan het volgende:

1. Klikken **[!UICONTROL Account]** in de rechterbovenhoek.

1. Klik in het weergegeven dialoogvenster op **[!UICONTROL Projects]**.

1. De weergave van uw API-referenties:

![Inloggegevens van de Mixpanel-API ophalen](../../../assets/Mixpanel_API_creds.png)

Houd dit open, u hebt het nodig om dit op te pakken.

## Het ingaan van uw [!DNL Mixpanel] API-referenties in [!DNL Commerce Intelligence] {#stepthree}

1. De `API Key` en `Secret` in de [!DNL Mixpanel] pagina met referenties in [!DNL Commerce Intelligence].
1. Klikken **[!UICONTROL Connect to Mixpanel]** om de installatie te voltooien.

Als de verbinding is gelukt, kunt u een _Succes!_ wordt boven aan de pagina weergegeven.

### Verwante

* [Verwacht [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
