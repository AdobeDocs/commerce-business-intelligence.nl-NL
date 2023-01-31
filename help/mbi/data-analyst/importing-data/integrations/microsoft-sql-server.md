---
title: Connect Microsoft SQL Server
description: Leer hoe u uw Microsoft SQL-database kunt verbinden met [!DNL MBI] in vier stappen.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Connect Microsoft SQL Server

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

In dit artikel wordt uitgelegd hoe u verbinding kunt maken met uw `Microsoft SQL` database naar [!DNL MBI] in vier stappen. Dit proces vereist enige technische expertise met betrekking tot serververbindingen en SQL, en kan steun van ontwikkelaars op uw team vereisen.

Wij steunen [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]en de meeste andere cloudserverproviders. Als u een vraag hebt op uw bepaalde gastheer, [een ondersteuningsticket indienen](../../../guide-overview.md) ons te vragen deze informatie te verstrekken.

Ons systeem moet SELECT-query&#39;s uitvoeren op uw database. Dit doen we eerst om een momentopname van uw databasestructuur te krijgen en dan regelmatig overwerk om onze gegevens up-to-date te houden. Onze updates zijn incrementeel en we beperken de updatefrequentie en -tijd om ongewenste belasting op uw server te voorkomen.

De beste manier om dit te doen is voor ons om met uw gegevensbestandserver over TCP/IP te verbinden. Maak een gebruiker voor gebruik die alleen SELECT-query&#39;s kan uitvoeren (en eventueel alleen gegevens kan selecteren uit de tabellen die u opgeeft). Dit moet gebeuren voor elk van uw servers waarmee u verbinding maakt [!DNL MBI].

## Verbinding maken `Microsoft SQL` tot [!DNL MBI]:

1. Controleer of uw server verbindingen via TCP/IP en verificatie met gemengde modus toestaat.

1. Zorg ervoor dat uw firewall de specifieke IP van onze server toestaat om verbinding te maken.

   U kunt het IP-adres dat we gebruiken om verbinding te maken met uw server vinden in de sectie Verbindingen van uw `Settings` pagina.

1. Maak een gebruiker die we gebruiken om u aan te melden bij uw databaseserver.  U hebt twee opties; hetzij via `UI` of via een `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (tweede voorbeeld)

1. Voer het IP-adres, de gebruikersnaam en het wachtwoord van de server in [!DNL MBI] krachtens **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Klikken **[!UICONTROL Add a Data Source]**.

1. Selecteer deze optie om een verbinding te maken met een `Microsoft SQL` en voer uw gegevens in in de velden op het nieuwe `Connections` pagina.

   Als u `Windows Azure`, moet u ook een databasenaam opgeven.
