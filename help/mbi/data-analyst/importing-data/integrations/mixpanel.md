---
title: Deelvenster Verbinden
description: Leer hoe u kunt analyseren hoe gebruikers door uw websites en apps navigeren en deze gebruiken.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Verbinden [!DNL Mixpanel]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Met [!DNL Mixpanel]kunt u analyseren hoe gebruikers door uw websites en apps navigeren en deze gebruiken. Als u goed kijkt naar gegevens over gebruikersgedrag, leidt dit tot slimmere beslissingen over ontwerp en ontwikkeling, wat over het algemeen een beter product betekent. Verbinding maken [!DNL Mixpanel] tot [!DNL MBI] Hiermee kunt u analyseren hoe uw gebruikers zich gedragen en hoe dat gedrag omzet oplevert.

Uw [!DNL Mixpanel] gegevens naar [!DNL MBI] een eenvoudig proces in drie stappen:

1. [Open de [!DNL Mixpanel] aanmeldingspagina in [!DNL MBI]](#stepone)
1. [Uw [!DNL Mixpanel] API-referenties](#steptwo)
1. [Voer uw [!DNL Mixpanel] API-referenties in MBI](#stepthree)

Als u dit proces wilt voltooien, moet u twee browservensters of tabbladen openen - één voor [!DNL MBI], de andere optie voor uw [!DNL Mixpanel] account.

## Het openen van de [!DNL Mixpanel] aanmeldingspagina {#stepone}

Aan de slag:

1. Ga naar de `Connections` pagina onder **[!DNL Manage Data** > **Connections]**.
1. Klikken **[!UICONTROL Add a New Source]**, die zich aan de rechterkant van het scherm boven het `Data Sources` tabel.
1. Klik op de knop [!DNL Mixpanel] en wordt de pagina met referenties geopend.

Laat deze pagina voorlopig open en schakel over naar het browservenster met uw [!DNL Mixpanel] account.

## Uw [!DNL Mixpanel] API-referenties {#steptwo}

Als u zich niet hebt aangemeld bij uw [!DNL Mixpanel] nog, doe dit en doe dan het volgende:

1. Klikken **[!UICONTROL Account]** in de rechterbovenhoek.
1. Klik in het weergegeven dialoogvenster op **[!UICONTROL Projects]**.
1. De weergave van uw API-referenties:

![Inloggegevens van de Mixpanel-API ophalen](../../../assets/Mixpanel_API_creds.png)

Houd dit open - u hebt het nodig om dit rond te krijgen.

## Uw [!DNL Mixpanel] API-referenties in [!DNL MBI] {#stepthree}

1. Kopieer de `API Key` en `Secret` in de [!DNL Mixpanel] aanmeldingspagina in [!DNL MBI].
1. Klikken **[!UICONTROL Connect to Mixpanel]** om de installatie te voltooien.

Dat is het! Als de verbinding is gelukt, kunt u _Succes!_ wordt boven aan de pagina weergegeven.

### Verwante

* [Verwacht [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
