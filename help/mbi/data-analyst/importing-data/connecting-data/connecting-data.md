---
title: Uw gegevens verbinden
description: Leer hoe u in Data Warehouse Manager door de tabellen kunt bladeren die u kunt synchroniseren.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Uw gegevens verbinden

In [!DNL Adobe Commerce Intelligence], worden gegevensbronnen aangeroepen `integrations`. Na een `integration` is verbonden, kunt u door de tabellen bladeren die beschikbaar zijn voor synchronisatie in Beheer Data Warehouse.

Integraties worden toegevoegd en beheerd met behulp van de `Connections` pagina, die u kunt openen door te klikken **[!UICONTROL Manage Data** > **Connections]**. Hier zie je:

* een lijst met alle integraties die op uw account zijn aangesloten

* het integratietype

* status ([!DNL Google Analytics] en [!DNL Data Import API] verbindingen hebben lege statusvelden)

* de laatste keer dat een verbindingstest wordt uitgevoerd (`Last Connection Started` kolom) is uitgevoerd

![Gegevens\_Bronnen\_Tabel.png](../../../assets/Data_Sources_Table.png)

## Typen integraties

Er zijn vier manieren om uw gegevens in te voeren [!DNL Commerce Intelligence]: verbind een gegevensbestand, verbind een integratie SaaS, upload een `.csv` of gebruik de Adobe-API.

## Database-integratie

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] ondersteunt SQL- en NoSQL-databases zoals [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [MICROSOFT SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), en [PostgreSQL](../integrations/postgresql.md).

Terwijl u direct uw gegevensbestand kunt verbinden met [!DNL Commerce Intelligence] het gebruiken van gegevensbestandgeloofsbrieven, adviseert de Adobe u een bewezen encryptiemethode zoals een tunnel van SSH gebruikt. Dit zorgt ervoor dat uw gegevens veilig en veilig blijven aangezien het zijn weg in uw Data Warehouse maakt.

Afhankelijk van de verbindingsmethode en het type van gegevensbestand, zou wat technische deskundigheid kunnen worden vereist om de opstelling te voltooien.

## `SaaS` Integraties

![](../../../assets/SaaS_icons.jpg)pree-commerce-logo.png

`SaaS` integratie is diensten zoals [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), en [[!DNL Zendesk]](../integrations/zendesk.md). Aangezien gegevens van derden op de server van de leverancier aanwezig zijn, kunt u deze niet rechtstreeks benaderen zoals u dat kunt met de gegevens in uw database.

Doorgaans kunt u een integratie instellen in [!DNL Commerce Intelligence] is even eenvoudig als het invoeren van uw accountgegevens. Voor sommige services is mogelijk een API-sleutel vereist om de autorisatie te voltooien. Kijk uit de [sectie integratie](../integrations/integrations.md) voor instructies over het produceren van om het even welke geloofsbrieven u wenst.

## Bestand uploaden

Weet u niet zeker hoe u gegevens van een aanvullende bron in uw Data Warehouse kunt krijgen? [Met de `File Upload` functie](../connecting-data/using-file-uploader.md) is een goede manier om gegevens in te zamelen die u niet nodig hebt voor de dagelijkse besluitvorming. Na de opmaakregels kunt u snel uploaden `.csv` in de Data Warehouse en sluit deze aan bij andere gegevensbronnen.

## [!DNL Commerce Intelligence] `Import API`

Als u het ophalen van gegevens uit een van uw eigen bronnen liever wilt automatiseren, kunt u de opdracht [!DNL Commerce Intelligence] `Import API`. Als het zich niet in een database of een `SaaS` integratie, `Import API` function is jouw beste weddenschap.

Het gebruik van de API vereist een beetje technische expertise - iemand die graag een klein Ruby- of PHP-script schrijft en onderhoudt, is meer dan gekwalificeerd.

Meer informatie over het aan de slag gaan met de `Import API`, bekijk de [Ontwikkelaarssite](https://developer.adobe.com/commerce/services/reporting/) en [hoe te om een API sleutel te produceren](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Integratie toevoegen

Om een integratie toe te voegen, klik **[!UICONTROL Manage Data** > **Connections]** en klik vervolgens op **[!UICONTROL Add a New Data Source]**. Klik op het pictogram van de integratie dat u wilt toevoegen en volg de instructies in Help-onderwerpen om de volgende zaken in te stellen:

* [Veelgestelde vragen over integratie](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Beschikbaar ](../integrations/integrations.md)
* [Tabellen consolideren](../../../best-practices/consolidating-your-tables.md)
* [Toegang tot uw database beperken](../../../administrator/account-management/restrict-db-access.md)

**Ziet u niet een gewenste integratie?** Sommige integraties moeten worden geactiveerd om zichtbaar te zijn in uw account. Als je op zoek bent naar zoiets [!DNL Facebook] maar het is niet in de lijst opgenomen, [een ondersteuningsticket indienen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**Als er een foutstatus voor een integratie wordt weergegeven**, bekijk de [Sectie Problemen oplossen](https://support.magento.com/hc/en-us/sections/360003078151) voor hulp.
