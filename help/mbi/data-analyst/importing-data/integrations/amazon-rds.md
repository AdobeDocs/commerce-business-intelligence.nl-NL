---
title: Connect Amazon RDS
description: Leer de stappen voor het aansluiten van uw instantie RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Connect Amazon RDS

De Relationele Diensten van het Gegevensbestand van Amazon (RDS) is een beheerde gegevensbestanddienst die op gegevensbestandmotoren loopt die u waarschijnlijk reeds vertrouwd met bent - [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md), en [[!DNL PostgreSQ]](../integrations/postgresql.md).

De stappen voor het verbinden van uw instantie RDS variëren lichtjes afhankelijk van het type van gegevensbestand u gebruikt (gebruik de verbindingen hierboven voor gedetailleerde instructies voor elke gegevensbestand), en of u al dan niet een gecodeerde verbinding gebruikt (als [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), maar hier zijn de grondbeginselen:

## Autoriseren [!DNL MBI] om toegang te krijgen tot uw database

Op de pagina met referenties (**[!UICONTROL Manage Data** > **Integrations]**) voor elke database ziet u een vak met de IP-adressen die u nodig hebt om RDS te verbinden met MBI: `54.88.76.97` en `34.250.211.151`. Hier is een blik op `MySQL credentials` pagina, waar wij het IP adresvakje benadrukten:

![](../../../assets/RDS_IP.png)

Voor [!DNL MBI] Als u verbinding wilt maken met uw RDS-instantie, moet u deze IP-adressen via de AWS-beheerconsole toevoegen aan de desbetreffende databasebeveiligingsgroep. Deze IP adressen kunnen aan een bestaande groep worden toegevoegd of u kunt tot nieuwe leiden - het belangrijke ding is dat de groep wordt gemachtigd om tot de instantie toegang te hebben u met wilt verbinden [!DNL MBI].

Wanneer u het gereedschap [!DNL MBI] IP adressen, zorg ervoor u toevoegt `/32` aan het eind van het adres om aan Amazon erop te wijzen dat het een nauwkeurig IP adres is. Maak u geen zorgen. de AWS-interface zal duidelijk maken dat dit noodzakelijk is.

## Een `Linux` gebruiker voor [!DNL MBI] {#linux}

>[!NOTE]
>
>Deze stap is alleen vereist als u een gecodeerde verbinding gebruikt. Raadpleeg het installatieartikel voor de database die u gebruikt (bijvoorbeeld: MySQL). De `Linux` gebruiker stelt ons in staat een `SSH tunnel`, de veiligste methode om gegevens via internet te verzenden.

## Een databasegebruiker voor MBI maken

Dit is het deel van het proces waar, afhankelijk van het gegevensbestand u gebruikt, de stappen zullen variëren. Het idee is echter hetzelfde: u zult een gebruiker voor [!DNL MBI] die wordt gebruikt voor toegang tot uw database. Instructies voor het maken van een database [!DNL MBI] kan worden gevonden in het installatieartikel voor het gegevensbestand u gebruikt.

## Verbindingsgegevens invoeren in MBI

Nadat u [!DNL MBI] toegang tot uw instantie en creeerde een gebruiker voor ons, het laatste ding u moet doen is de verbindingsinfo in ingaan [!DNL MBI].

De referentiepagina&#39;s voor `MySQL`, `Microsoft SQL`, en `PostgreSQL` zijn toegankelijk via de `Integrations` pagina (**[!UICONTROL Manage Data** > **Integrations]**) door te klikken op **[!UICONTROL Add Integration]**. Wanneer de lijst met integraties wordt weergegeven, klikt u op het pictogram voor de database die u gebruikt om naar de pagina met referenties te gaan. Neem contact op met het accountteam van Adobe als u momenteel geen toegang hebt tot de gewenste-integratie.

Als u de verbinding wilt maken, hebt u de volgende informatie nodig:

* Het openbare adres van uw instantie RDS: Dit vindt u in de AWS-beheerconsole.
* De poort die uw database-instantie gebruikt: Sommige databases hebben een standaardpoort, die automatisch de `Port` veld. Deze informatie kan ook in onze opstellingsdocumentatie voor het gegevensbestand worden gevonden.
* De gebruikersnaam en het wachtwoord van de gebruiker waarvoor u hebt gemaakt [!DNL MBI].

Als u een gecodeerde verbinding gebruikt, wijzigt u de instelling `Encrypted` schakelen op de pagina met databasereferenties naar `Yes`. Hiermee wordt een extra formulier weergegeven voor het instellen van de versleuteling:

![](../../../assets/sql-integration-encrypted-yes.png)

Dat is alles wat er aan te pas komt! Het aansluiten van uw RDS-instantie is voltooid.
