---
title: Databanken verbinden via VPN
description: Leer hoe te om gegevensbestanden via VPN in plaats van de Tunnel van SSH te verbinden.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Databanken verbinden via VPN

Terwijl Adobe aanbeveelt dat u uw databases aansluit met behulp van een `SSH tunnel`kunt u ook een gecodeerde `VPN` verbinding om de zaken veilig te houden. A `VPN` kan voor om het even welk van uw gegevensbestandintegratie worden gebruikt en, om dingen eenvoudig te houden, is het proces enkel het zelfde als vestiging `SSH tunnel`:

1. [Een [!DNL Commerce Intelligence] databasegebruiker](#database)
1. [Een [!DNL Commerce Intelligence] VPN-gebruiker](#vpn)
1. [Toegang tot de [!DNL Commerce Intelligence] IP-adres](#allowlist)
1. [Ga de verbinding en de gebruikersinfo van VPN in de Intelligentie van de Handel](#finish)

Naast gegevensbestandgeloofsbrieven, moet u geloofsbrieven voor een gebruiker van VPN ingaan om dingen omhoog te verpakken. Om het even welke gebruiker van VPN werkt, maar Adobe adviseert u tot een [!DNL Commerce Intelligence] -gebruiker, omdat u de gebruikers op uw account gemakkelijker kunt volgen.

## Databasegebruikers maken voor [!DNL Commerce Intelligence] {#database}

Het proces voor het maken van een databasegebruiker is afhankelijk van het databasetype waarmee u verbinding maakt. Klik op de onderstaande koppelingen om de instructies voor elk databasetype weer te geven.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Een `VPN` gebruiker voor [!DNL Commerce Intelligence] {#vpn}

Zoals eerder vermeld, zijn alle geldige `VPN` gebruiker werkt - maar Adobe raadt u aan een gebruiker alleen te maken voor [!DNL Commerce Intelligence] gebruik.

## Toegang tot de [!DNL Commerce Intelligence] IP-adressen {#allowlist}

De verbinding is alleen gelukt als u uw firewall configureert om toegang vanaf uw IP-adressen toe te staan. Ze zijn `54.88.76.97` en `34.250.211.151`, maar het is ook `credentials` pagina voor elke databaseintegratie:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## De verbinding betreden en `VPN` gebruikersgegevens in [!DNL Commerce Intelligence] {#finish}

Als u de inhoud wilt samenvoegen, moet u de verbinding en gebruikersgegevens invoeren in [!DNL Commerce Intelligence]. Hebt u de database verlaten? `credentials` pagina geopend? Indien niet, ga naar **[!UICONTROL Manage Data** > **Connections]**. Klikken **[!UICONTROL Add New Data Source]** en klik vervolgens op het pictogram voor de database waarmee u verbinding maakt. Vergeet niet de `Encrypted` schakelen naar `Yes`.

Voer de volgende gegevens in op deze pagina, te beginnen met de `Database Connection` sectie:

* `Username`: De gebruikersnaam voor de [!DNL Commerce Intelligence] databasegebruiker
* `Password`: Het wachtwoord voor de [!DNL Commerce Intelligence] databasegebruiker
* `Port`: De poort van de database op de server. Standaardwaarden zijn:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: Standaard is dit localhost `127.0.0.1`, maar het kan ook het openbare IP-adres van uw server of een lokaal netwerkadres van uw server zijn.
* `Database Name (optional)`: Als u slechts toegang tot één gegevensbestand hebt toegestaan (dit wordt gespecificeerd tijdens de stap van de gegevensbestandgebruiker creeert), ga hier de naam van dat gegevensbestand in.

Onder de `Encryption Connection` sectie:

* `Encryption Type`: Stel deze in op `Cisco IPsec VPN`
* `Gateway Address`: Het IP adres van de server van VPN
* `Group Name`: De naam van de groep die wordt gebruikt voor groepsverificatie
* `Group Secret`: Het wachtwoord dat overeenkomt met de groep.
* `Username`: De [!DNL Commerce Intelligence] `VPN` gebruikersnaam
* `Password`: De [!DNL Commerce Intelligence] `VPN` gebruikerswachtwoord

Als u klaar bent, klikt u op **[!UICONTROL Save & Test]** om de installatie te voltooien.
