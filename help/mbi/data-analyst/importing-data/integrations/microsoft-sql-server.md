---
title: Connect Microsoft SQL Server
description: Leer hoe te om uw SQL van Microsoft gegevensbestand met  [!DNL Commerce Intelligence]  in een proces in vier stappen te verbinden.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 736dbdc3ea6bc8b7c852f06110705765f040c31f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Connect [!DNL Microsoft SQL] Server

>[!NOTE]
>
>Vereist [&#x200B; toestemmingen Admin &#x200B;](../../../administrator/user-management/user-management.md).

![&#x200B; het embleem van de Server van Microsoft SQL &#x200B;](../../../assets/MicrosoftSQLServer-logo.png)

In dit onderwerp wordt uitgelegd hoe u de [!DNL Microsoft SQL] -database in vier stappen met [!DNL Commerce Intelligence] kunt verbinden. Dit proces vereist enige technische expertise met betrekking tot serververbindingen en SQL, en kan steun van ontwikkelaars op uw team vereisen.

[!DNL Commerce Intelligence] ondersteunt [!DNL Amazon RDS] , [!DNL EC2] , [!DNL Microsoft SQL Azure] en de meeste andere cloudserverproviders. Als u een vraag op uw bijzondere gastheer hebt, [&#x200B; voorlegt een steunkaartje &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) vragend ons om deze informatie te verstrekken.

Uw systeem moet SELECT-query&#39;s uitvoeren op uw database. Dit wordt eerst gedaan om een momentopname van uw gegevensbestandstructuur en dan regelmatig overwerk te krijgen om uw gegevens bijgewerkt te houden. Uw updates zijn incrementeel en Adobe beperkt de updatefrequentie en -tijd om ongewenste laadtijden op uw server te voorkomen.

De beste manier om dit te doen is voor ons om met uw gegevensbestandserver over TCP/IP te verbinden. Maak een gebruiker voor gebruik die alleen SELECT-query&#39;s kan uitvoeren (en eventueel alleen gegevens kan selecteren uit de tabellen die u opgeeft). Dit moet worden gedaan voor elk van uw servers waarmee u verbinding maakt [!DNL Commerce Intelligence].

## `Microsoft SQL` verbinden met [!DNL Commerce Intelligence] :

1. Controleer of uw server verbindingen via TCP/IP en verificatie met gemengde modus toestaat.

1. Zorg ervoor dat uw firewall de specifieke IP van uw server toestaat om te verbinden.

   U kunt het IP-adres dat wordt gebruikt om verbinding te maken met uw server vinden in de sectie Verbindingen op uw `Settings` -pagina.

1. Maak een gebruiker om u aan te melden bij uw databaseserver. U hebt twee opties: via `UI` of via een `query` :
   * `UI`
   * `Query`

1. Voer het IP-adres, de gebruikersnaam en het wachtwoord van de server in [!DNL Commerce Intelligence] onder **[!UICONTROL Manage Data** > **Connections]** .

   ![&#x200B; beheert de pagina van de Verbindingen van Gegevens die gegevensbestandintegratie tonen &#x200B;](../../../assets/manage-data-connections.png)

1. Klik op **[!UICONTROL Add a Data Source]**.

1. Selecteer deze optie om een `Microsoft SQL` -database te verbinden en voer uw referenties in de velden op de nieuwe `Connections` -pagina in.

   Als u `Windows Azure` gebruikt, moet u ook een databasenaam opgeven.
