---
title: Databanken verbinden via VPN
description: Leer hoe te om gegevensbestanden via VPN in plaats van de Tunnel van SSH te verbinden.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Databanken verbinden via VPN

Hoewel Adobe aanbeveelt dat u uw databases aansluit met behulp van een `SSH tunnel` , kunt u ook een gecodeerde `VPN` -verbinding gebruiken om de beveiliging te behouden. Een `VPN` kan worden gebruikt voor al uw database-integratie en om de zaken eenvoudig te houden, is het proces ongeveer hetzelfde als het instellen van een `SSH tunnel` :

1. [Creeer een  [!DNL Commerce Intelligence]  gegevensbestandgebruiker](#database)
1. [Creeer een  [!DNL Commerce Intelligence]  gebruiker van VPN](#vpn)
1. [Toestaan toegang tot het  [!DNL Commerce Intelligence]  IP adres](#allowlist)
1. [Ga de verbinding en de gebruikersinfo van VPN in Commerce Intelligence in](#finish)

Naast gegevensbestandgeloofsbrieven, moet u geloofsbrieven voor een gebruiker van VPN ingaan om dingen omhoog te verpakken. Elke VPN-gebruiker werkt, maar Adobe raadt u aan een [!DNL Commerce Intelligence] -gebruiker te maken, omdat u hiermee de gebruikers op uw account gemakkelijker kunt bijhouden.

## Databasegebruikers maken voor [!DNL Commerce Intelligence] {#database}

Het proces voor het maken van een databasegebruiker is afhankelijk van het databasetype waarmee u verbinding maakt. Klik op de onderstaande koppelingen om de instructies voor elk databasetype weer te geven.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Een `VPN` gebruiker voor [!DNL Commerce Intelligence] maken {#vpn}

Zoals eerder vermeld, werkt elke geldige `VPN` -gebruiker - maar Adobe raadt u aan een gebruiker alleen voor [!DNL Commerce Intelligence] -gebruik te maken.

## Toegang tot de IP-adressen van [!DNL Commerce Intelligence] toestaan {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze staan `54.88.76.97` en `34.250.211.151` , maar ze staan ook op de pagina `credentials` voor alle databaseintegratie:

![&#x200B; MBI_Allow_Access_IPs.png &#x200B;](../../../assets/MBI_allow_access_IPs.png)

## De verbinding en `VPN` gebruikersgegevens invoeren in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence] . Hebt u de database `credentials` pagina geopend? Zo niet, ga naar **[!UICONTROL Manage Data** > **Connections]** . Klik op **[!UICONTROL Add New Data Source]** en klik vervolgens op het pictogram voor de database waarmee u verbinding maakt. Vergeet niet de `Encrypted` -schakeloptie in `Yes` te wijzigen.

Voer de volgende gegevens op deze pagina in, te beginnen met de sectie `Database Connection` :

* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] databasegebruiker
* `Password`: Het wachtwoord voor de [!DNL Commerce Intelligence] databasegebruiker
* `Port`: De poort van de database op de server. Standaardwaarden zijn:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: Standaard is dit localhost `127.0.0.1` , maar het kan ook het openbare IP-adres van uw server of een lokaal netwerkadres zijn.
* `Database Name (optional)`: Als u slechts toegang tot één database hebt toegestaan (dit is opgegeven tijdens de stap voor het maken van de databasegebruiker), voert u hier de naam van die database in.

Onder de sectie `Encryption Connection` :

* `Encryption Type`: stel deze in op `Cisco IPsec VPN`
* `Gateway Address`: Het IP-adres van de VPN-server
* `Group Name`: De naam van de groep die wordt gebruikt voor groepsverificatie
* `Group Secret`: Het wachtwoord dat overeenkomt met de groep.
* `Username`: De gebruikersnaam [!DNL Commerce Intelligence] `VPN`
* `Password`: Het [!DNL Commerce Intelligence] `VPN` -gebruikerswachtwoord

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.
