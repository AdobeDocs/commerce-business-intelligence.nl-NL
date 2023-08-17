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

De stappen voor het verbinden van uw [!DNL RDS] -instantie variëren, afhankelijk van het type database dat u gebruikt en of u een gecodeerde verbinding gebruikt (zoals een [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), maar hier zijn de grondbeginselen.

## Autoriseren [!DNL Commerce Intelligence] om toegang te krijgen tot uw database

Op de pagina met referenties (**[!UICONTROL Manage Data** > **Integrations]**) voor elke database, ziet u een vak met de IP-adressen die u moet machtigen om R te verbinden[!DNL RDS] tot [!DNL Commerce Intelligence]: `54.88.76.97` en `34.250.211.151`. Hier is een blik op `MySQL credentials` pagina, waar u het IP adresvakje benadrukte:

![](../../../assets/RDS_IP.png)

Voor [!DNL Commerce Intelligence] om verbinding te maken met uw [!DNL RDS] instantie, moet u deze IP adressen aan de aangewezen groep van de gegevensbestandveiligheid via de het beheersconsole van AWS toevoegen. Deze IP adressen kunnen aan een bestaande groep worden toegevoegd of u kunt tot één leiden - het belangrijke ding is dat de groep wordt gemachtigd om tot de instantie toegang te hebben u met wilt verbinden [!DNL Commerce Intelligence].

Wanneer u het gereedschap [!DNL Commerce Intelligence] IP adressen, zorg ervoor u toevoegt `/32` aan het einde van het adres dat moet worden aangegeven aan [!DNL Amazon] dat het een nauwkeurig IP adres is. Maakt u zich geen zorgen; de interface van AWS maakt duidelijk dat dit vereist is.

## Een `Linux` gebruiker voor [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Deze stap is alleen vereist als u een gecodeerde verbinding gebruikt. Voor instructies op hoe te om dit te doen, verwijs naar het opstellingsonderwerp voor het gegevensbestand u gebruikt (bv: MySQL). De `Linux` gebruiker stelt ons in staat een `SSH tunnel`, de veiligste methode om gegevens via internet te verzenden.

## Een databasegebruiker maken voor [!DNL Commerce Intelligence]

Dit is het deel van het proces waar, afhankelijk van het gegevensbestand u gebruikt, de stappen variëren. Het idee is echter hetzelfde: u maakt een gebruiker voor [!DNL Commerce Intelligence] die wordt gebruikt voor toegang tot uw database. Instructies voor het maken van een database [!DNL Commerce Intelligence] De gebruiker kan in het opstellingsonderwerp voor het gegevensbestand worden gevonden u gebruikt.

## Verbindingsgegevens invoeren in [!DNL Commerce Intelligence]

Nadat u [!DNL Commerce Intelligence] toegang tot uw instantie en creeerde een gebruiker voor ons, het laatste ding u moet doen is de verbindingsinfo in ingaan [!DNL Commerce Intelligence].

De referentiepagina&#39;s voor `MySQL`, `Microsoft SQL`, en `PostgreSQL` zijn toegankelijk via de `Integrations` pagina (**[!UICONTROL Manage Data** > **Integrations]**) door op **[!UICONTROL Add Integration]**. Wanneer de lijst met integraties wordt weergegeven, klikt u op het pictogram voor de database die u gebruikt om naar de pagina met referenties te gaan. Neem contact op met het accountteam van de Adobe als u momenteel geen toegang hebt tot de gewenste .

Als u de verbinding wilt maken, hebt u de volgende informatie nodig:

* Het openbare adres van uw RDS-instantie: dit vindt u in het [!DNL AWS] beheerconsole.
* De poort die uw database-instantie gebruikt: sommige databases hebben een standaardpoort, die automatisch de `Port` veld. Deze informatie kan ook in de opstellingsdocumentatie voor het gegevensbestand worden gevonden.
* De gebruikersnaam en het wachtwoord van de gebruiker waarvoor u hebt gemaakt [!DNL Commerce Intelligence].

Als u een gecodeerde verbinding gebruikt, wijzigt u de instelling `Encrypted` schakelen op de pagina met databasereferenties naar `Yes`. Er wordt een extra formulier weergegeven voor het instellen van de codering:

![](../../../assets/sql-integration-encrypted-yes.png)


