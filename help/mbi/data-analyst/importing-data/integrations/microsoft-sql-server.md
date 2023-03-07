---
title: Microsoft; reg; SQL Server
description: Leer hoe u verbinding maakt met uw Microsoft&reg. SQL-database naar [!DNL MBI] in vier stappen.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Connect Microsoft® SQL Server

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

In dit artikel wordt uitgelegd hoe u verbinding kunt maken met uw `Microsoft SQL` database naar [!DNL MBI] in vier stappen. Dit proces vereist enige technische expertise met betrekking tot serververbindingen en SQL, en kan steun van ontwikkelaars op uw team vereisen.

MBI-ondersteuning [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft®; SQL Azure]en de meeste andere cloudserverproviders. Als u een vraag hebt op uw bepaalde gastheer, [een ondersteuningsticket indienen](../../../guide-overview.md) ons te vragen deze informatie te verstrekken.

Uw systeem moet SELECT-query&#39;s uitvoeren op uw database. Dit wordt eerst gedaan om een momentopname van uw gegevensbestandstructuur en dan regelmatig overwerk te krijgen om uw gegevens bijgewerkt te houden. Uw updates zijn incrementeel en Adobe beperkt de updatefrequentie en -tijd om ongewenste laadtijden op uw server te voorkomen.

De beste manier om dit te doen is voor ons om met uw gegevensbestandserver over TCP/IP te verbinden. Maak een gebruiker voor gebruik die alleen SELECT-query&#39;s kan uitvoeren (en eventueel alleen gegevens kan selecteren uit de tabellen die u opgeeft). Dit moet worden gedaan voor elk van uw servers waarmee u verbindt [!DNL MBI].

## Verbinding maken `Microsoft SQL` tot [!DNL MBI]:

1. Controleer of uw server verbindingen via TCP/IP en verificatie met gemengde modus toestaat.

1. Zorg ervoor dat uw firewall de specifieke IP van uw server toestaat om te verbinden.

   U kunt het IP-adres dat wordt gebruikt om verbinding te maken met uw server vinden in de sectie Verbindingen van uw `Settings` pagina.

1. Maak een gebruiker die u wilt gebruiken om u aan te melden bij uw databaseserver. U hebt twee opties; hetzij via `UI` of via een `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (tweede voorbeeld)

1. Voer het IP-adres, de gebruikersnaam en het wachtwoord van de server in [!DNL MBI] krachtens **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Klikken **[!UICONTROL Add a Data Source]**.

1. Selecteer deze optie om een verbinding te maken met een `Microsoft SQL` en voer uw gegevens in in de velden op het nieuwe `Connections` pagina.

   Als u `Windows Azure`, moet u ook een databasenaam opgeven.
