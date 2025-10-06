---
title: MySQL via cPanel verbinden
description: Leer hoe u MySQL via cPanel kunt verbinden.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Verbinden [!DNL MySQL] via [!DNL cPanel]

* [Een  [!DNL Commerce Intelligence] [!DNL MySQL] gebruiker maken in  [!DNL cPanel]](#cpanel)
* [Voer verbinding en gebruikersgegevens in  [!DNL Commerce Intelligence]](#finish)

## Springen naar

* [[!DNL MySQL] via SSH-tunnel](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via directe verbinding](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] raadt u aan SSH of een andere codering te gebruiken om uw gegevens te beveiligen. Als dit geen optie is, kunt u [!DNL Commerce Intelligence] met uw gegevensbestand nog direct verbinden gebruikend de instructies in dit onderwerp.

In dit onderwerp wordt u door de [!DNL MySQL] -database geleid voor het rechtstreeks verbinden met [!DNL Commerce Intelligence] using [!DNL cPanel] . Dit proces kan ook worden gebruikt om [!DNL Adobe Commerce] en andere op MySQL gebaseerde eCommerce-databases te verbinden met [!DNL Commerce Intelligence] .

1. Een [!DNL Commerce Intelligence] [!DNL MySQL] gebruiker maken in [!DNL cPanel]
1. Verbindings- en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]

Aan de slag.

## Een [!DNL Commerce Intelligence] [!DNL MySQL] gebruiker maken in [!DNL cPanel] {#cpanel}

1. Meld u via uw hostingprovider aan bij [!DNL cPanel] .
1. Klik op **[!UICONTROL [!DNL MySQL] Databases]** in de sectie `Database` .
1. Schuif omlaag naar de sectie `Add New User` en maak een gebruiker voor [!DNL Commerce Intelligence] :

   ![&#x200B; cPanel MySQL de interface die van Gegevensbestanden toont creeert gebruikersvorm &#x200B;](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Klik op **[!UICONTROL Create User]**.
1. Nu u de gebruiker hebt gecreeerd, moet u het aan een gegevensbestand associëren. Ga terug naar de sectie `Add New User` . Zie de instellingen voor `Add User to Database?` Dat is wat u nodig hebt.
1. Selecteer in het vervolgkeuzemenu `User` van deze sectie de gebruiker die u hebt gemaakt.
1. Selecteer in het vervolgkeuzemenu `Database` van deze sectie de database waarmee u verbinding wilt maken [!DNL Commerce Intelligence] .
1. Klik op **[!UICONTROL Add]**.
1. Wanneer de lijst met bevoegdheden wordt weergegeven, schakelt u het selectievakje naast `SELECT` in. Dit is alles wat [!DNL Commerce Intelligence] nodig heeft om verbinding te maken met uw database.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] . Hebt u de aanmeldingspagina van [!DNL MySQL] geopend? Als dat niet het geval is, gaat u naar **[!UICONTROL Manage Data** > **Connections]** en klikt u op **[!UICONTROL Add New Data Source]** , gevolgd door het pictogram [!DNL MySQL] .

Voer in de sectie `Database Connection` de volgende informatie in op deze pagina:

* `Username`: De gebruikersnaam voor de gebruiker [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: Het wachtwoord voor de gebruiker [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: het openbare adres van de `MySQL` server [!DNL Commerce Intelligence] maakt verbinding met. Dit is doorgaans de URL waarmee u zich aanmeldt bij `[!DNL cPanel]` .

Als u een [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md) gebruikt, moet u de versleutelingsinformatie invoeren. Stel de schakeloptie `Encrypted` in op `Yes` om het formulier weer te geven.

* `Connection Type`: stel deze in op `SSH Tunnel`
* `Remote Address`: Het IP-adres of de hostnaam van de server [!DNL Commerce Intelligence] wordt via een tunnel verzonden naar
* `Username`: De gebruikersbenaming voor de [!DNL Commerce Intelligence] `SSH (Linux)` gebruiker, zie [&#x200B; instructies &#x200B;](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) op hoe te om dit te doen, als u niet reeds hebt)
* `SSH Port`: SSH-poort op uw server (`22` standaard)

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Verwante:

* [&#x200B; Reauthenticating integrations &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
