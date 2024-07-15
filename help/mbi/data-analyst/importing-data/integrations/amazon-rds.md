---
title: Connect Amazon RDS
description: Leer de stappen voor het aansluiten van uw instantie RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Verbinden [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] is een beheerde gegevensbestanddienst die op gegevensbestandmotoren loopt die u waarschijnlijk reeds vertrouwd met bent:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

De stappen voor het verbinden van uw [!DNL RDS] -instantie variëren, afhankelijk van het type database dat u gebruikt en of u een gecodeerde verbinding gebruikt (zoals een [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md) ), maar dit zijn de basisbeginselen.

## Autoriseren [!DNL Commerce Intelligence] voor toegang tot uw database

Op de geloofsbrieven pagina (**[!UICONTROL Manage Data** > **Integrations]**) voor elke gegevensbestand, ziet u een doos die de IP adressen bevat u moet machtigen om R [!DNL RDS] aan [!DNL Commerce Intelligence] te verbinden: `54.88.76.97` en `34.250.211.151`. Hier is een blik op de `MySQL credentials` pagina, waar u het IP adresvakje benadrukte:

![](../../../assets/RDS_IP.png)

[!DNL Commerce Intelligence] kan alleen verbinding maken met uw [!DNL RDS] -instantie als u deze IP-adressen via de AWS-beheerconsole toevoegt aan de betreffende beveiligingsgroep van de database. Deze IP-adressen kunnen worden toegevoegd aan een bestaande groep of u kunt een groep maken. Het belangrijkste is dat de groep gemachtigd is om toegang te krijgen tot de instantie waarmee u verbinding wilt maken [!DNL Commerce Intelligence] .

Wanneer u de [!DNL Commerce Intelligence] IP-adressen toevoegt, moet u een `/32` aan het einde van het adres toevoegen om aan [!DNL Amazon] aan te geven dat het een exact IP-adres is. Maakt u zich geen zorgen; de interface van AWS maakt duidelijk dat dit vereist is.

## Een `Linux` gebruiker voor [!DNL Commerce Intelligence] maken {#linux}

>[!NOTE]
>
>Deze stap is alleen vereist als u een gecodeerde verbinding gebruikt. Voor instructies op hoe te om dit te doen, verwijs naar het opstellingsonderwerp voor het gegevensbestand u gebruikt (bv: MySQL). De gebruiker van `Linux` staat ons toe om een `SSH tunnel` tot stand te brengen, die de veiligste methode is om gegevens over Internet te verzenden.

## Een databasegebruiker maken voor [!DNL Commerce Intelligence]

Dit is het deel van het proces waar, afhankelijk van het gegevensbestand u gebruikt, de stappen variëren. Het idee is echter hetzelfde als wanneer u een gebruiker voor [!DNL Commerce Intelligence] maakt die wordt gebruikt om toegang te krijgen tot uw database. Instructies voor het creëren van een gegevensbestand [!DNL Commerce Intelligence] gebruiker kunnen in het opstellingsonderwerp voor het gegevensbestand worden gevonden u gebruikt.

## Verbindingsgegevens invoeren in [!DNL Commerce Intelligence]

Nadat u [!DNL Commerce Intelligence] toegang tot uw instantie hebt verleend en een gebruiker voor ons hebt gemaakt, moet u de verbindingsgegevens in [!DNL Commerce Intelligence] invoeren.

De referentiepagina&#39;s voor `MySQL` , `Microsoft SQL` en `PostgreSQL` zijn toegankelijk via de `Integrations` pagina (**[!UICONTROL Manage Data** > **Integrations]**) door op **[!UICONTROL Add Integration]** te klikken. Wanneer de lijst met integraties wordt weergegeven, klikt u op het pictogram voor de database die u gebruikt om naar de pagina met referenties te gaan. Neem contact op met het accountteam van de Adobe als u momenteel geen toegang hebt tot de gewenste .

Als u de verbinding wilt maken, hebt u de volgende informatie nodig:

* Het openbare adres van uw RDS-instantie: dit vindt u in de [!DNL AWS] -beheerconsole.
* De poort die uw database-instantie gebruikt: sommige databases hebben een standaardpoort die het veld `Port` automatisch vult. Deze informatie kan ook in de opstellingsdocumentatie voor het gegevensbestand worden gevonden.
* De gebruikersnaam en het wachtwoord van de gebruiker die u voor [!DNL Commerce Intelligence] hebt gemaakt.

Als u een gecodeerde verbinding gebruikt, wijzigt u de schakeloptie `Encrypted` op de pagina met databasereferenties in `Yes` . Er wordt een extra formulier weergegeven voor het instellen van de codering:

![](../../../assets/sql-integration-encrypted-yes.png)


