---
title: MySQL via cPanel verbinden
description: Leer hoe u MySQL via cPanel kunt verbinden.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Verbinden [!DNL MySQL] via [!DNL cPanel]

* [Een [!DNL Commerce Intelligence] [!DNL MySQL] gebruiker in [!DNL cPanel]](#cpanel)
* [Verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]](#finish)

## Springen naar

* [[!DNL MySQL] via SSH-tunnel](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via directe verbinding](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] raadt u aan SSH of een andere codering te gebruiken om uw gegevens te beveiligen. Als dit geen optie is, kunt u nog steeds rechtstreeks verbinding maken [!DNL Commerce Intelligence] aan uw gegevensbestand gebruikend de instructies in dit onderwerp.

Dit onderwerp loopt u door het rechtstreeks verbinden van uw [!DNL MySQL] database naar [!DNL Commerce Intelligence] gebruiken [!DNL cPanel]. Dit proces kan ook worden gebruikt om verbinding te maken [!DNL Adobe Commerce] en andere MySQL-gebaseerde eCommerce-databases naar [!DNL Commerce Intelligence].

1. Een [!DNL Commerce Intelligence] [!DNL MySQL] gebruiker in [!DNL cPanel]
1. Verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]

Aan de slag.

## Een [!DNL Commerce Intelligence] [!DNL MySQL] gebruiker in [!DNL cPanel] {#cpanel}

1. Aanmelden bij [!DNL cPanel] via uw hostingprovider.
1. Klikken **[!UICONTROL [!DNL MySQL] Databases]**, gevestigd in de `Database` sectie.
1. Omlaag schuiven naar de `Add New User` en maak een gebruiker voor [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Klikken **[!UICONTROL Create User]**.
1. Nu u de gebruiker hebt gecreeerd, moet u het aan een gegevensbestand associëren. Ga terug naar de `Add New User` sectie - zie de montages voor `Add User to Database?` Dat is wat u nodig hebt.
1. In de `User` Selecteer de gebruiker die u hebt gemaakt in het vervolgkeuzemenu van deze sectie.
1. In de `Database` vervolgkeuzelijst van deze sectie, selecteer de database waarmee u verbinding wilt maken [!DNL Commerce Intelligence].
1. Klikken **[!UICONTROL Add]**.
1. Schakel het selectievakje naast `SELECT` - dit alles [!DNL Commerce Intelligence] moet verbinding maken met uw database.

## De verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]. Heb je de [!DNL MySQL] aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** en de [!DNL MySQL] pictogram.

Voer de volgende gegevens in op deze pagina in het dialoogvenster `Database Connection` sectie:

* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: Het wachtwoord voor de [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: De openbare adressen van de `MySQL` server [!DNL Commerce Intelligence] maakt verbinding met. Dit is gewoonlijk de URL waarmee u zich aanmeldt `[!DNL cPanel]`.

Als u een [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), moet u de versleutelingsgegevens invoeren. Stel de `Encrypted` schakelen naar `Yes` om het formulier weer te geven.

* `Connection Type`: Stel deze in op `SSH Tunnel`
* `Remote Address`: Het IP-adres of de hostnaam van de server [!DNL Commerce Intelligence] wordt
* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] `SSH (Linux)` gebruiker, zie [instructies](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) over hoe dit moet gebeuren, als u dat nog niet hebt gedaan)
* `SSH Port`: SSH-poort op uw server (`22` standaard)

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Verwante:

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
