---
title: MySQL via cPanel verbinden
description: Leer hoe u MySQL via cPanel kunt verbinden.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: e4ac176492913623ae461484c8ef2abe034e5f62
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# MySQL via cPanel verbinden

* [Een [!DNL MBI] MySQL-gebruiker in cPanel](#cpanel)
* [Verbinding en gebruikersgegevens invoeren in MBI](#finish)

## Springen naar

* [MySQL via SSH-tunnel](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL via directe verbinding](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>Adobe raadt u aan SSH of een andere codering te gebruiken om uw gegevens te beveiligen! Als dit geen optie is, kunt u nog steeds rechtstreeks verbinding maken [!DNL MBI] aan uw database toe met behulp van de instructies in dit artikel.

Dit artikel begeleidt u door direct het verbinden van uw gegevensbestand MySQL met [!DNL MBI] gebruiken `cPanel`. Dit proces kan ook worden gebruikt om verbinding te maken [!DNL Adobe Commerce] en andere MySQL-gebaseerde eCommerce-databases naar [!DNL MBI].

1. Een [!DNL MBI] MySQL-gebruiker in `cPanel`
1. Verbinding en gebruikersgegevens invoeren in [!DNL MBI]

Aan de slag.

## Een [!DNL MBI] MySQL-gebruiker in `cPanel` {#cpanel}

1. Aanmelden bij [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) via uw hostingprovider.
1. Klikken **[!UICONTROL MySQL Databases]**, gevestigd in de `Database` sectie.
1. Omlaag schuiven naar de `Add New User` en maak een gebruiker voor [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Klikken **[!UICONTROL Create User]**.
1. Nu u de gebruiker hebt gecreeerd, moet u het aan een gegevensbestand associëren. Ga terug naar de `Add New User` sectie - zie de montages voor `Add User to Database?` Dat is wat u nodig hebt.
1. In de `User` Selecteer de gebruiker die u hebt gemaakt in het vervolgkeuzemenu van deze sectie.
1. In de `Database` vervolgkeuzelijst van deze sectie, selecteer de database waarmee u verbinding wilt maken [!DNL MBI].
1. Klikken **[!UICONTROL Add]**.
1. Schakel het selectievakje naast `SELECT` - dit alles [!DNL MBI] moet verbinding maken met uw database.

## De verbinding en gebruikersgegevens invoeren in [!DNL MBI] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL MBI]. Hebt u de MySQL aanmeldingspagina geopend? Indien niet, ga naar **[!UICONTROL Manage Data** > **Connections]** en klik op **[!UICONTROL Add New Data Source]** en vervolgens het MySQL-pictogram.

Voer de volgende gegevens in op deze pagina in het dialoogvenster `Database Connection` sectie:

* `Username`: De gebruikersnaam voor de [!DNL MBI] MySQL-gebruiker
* `Password`: Het wachtwoord voor de [!DNL MBI] MySQL-gebruiker
* `Port`: De poort van MySQL op uw server (`3306` standaard)
* `Host`: De openbare adressen van de `MySQL` server [!DNL MBI] maakt verbinding met. Dit is gewoonlijk de URL waarmee u zich aanmeldt `cPanel`.

Als u een [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), moet u de versleutelingsgegevens invoeren. Stel de `Encrypted` schakelen naar `Yes` om het formulier weer te geven.

* `Connection Type`: Stel deze in op `SSH Tunnel`
* `Remote Address`: Het IP-adres of de hostnaam van de server [!DNL MBI] wordt
* `Username`: De gebruikersnaam voor de [!DNL MBI] `SSH (Linux)` gebruiker, zie [instructies](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) over hoe dit moet gebeuren, als u dat nog niet hebt gedaan)
* `SSH Port`: SSH-poort op uw server (`22` standaard)

Dat is het! Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.

## Verwante:

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
