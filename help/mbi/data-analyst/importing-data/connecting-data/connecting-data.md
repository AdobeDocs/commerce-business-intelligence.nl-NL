---
title: Uw gegevens verbinden
description: Leer hoe u in Data Warehouse Manager door de tabellen kunt bladeren die u kunt synchroniseren.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Uw gegevens verbinden

In [!DNL Adobe Commerce Intelligence] worden gegevensbronnen `integrations` genoemd. Nadat de verbinding met `integration` is voltooid, kunt u in Beheer Data Warehouse door de tabellen bladeren die beschikbaar zijn voor synchronisatie.

Integraties worden toegevoegd en beheerd met behulp van de pagina `Connections` , die toegankelijk is door op **[!UICONTROL Manage Data** > **Connections]** te klikken. Hier zie je:

* een lijst met alle integraties die op uw account zijn aangesloten

* het integratietype

* status ([!DNL Google Analytics] en [!DNL Data Import API] -verbindingen hebben lege statusvelden)

* de laatste keer dat een verbindingstest (`Last Connection Started` kolom) werd uitgevoerd

![ Gegevens \_Bronnen\_Table.png ](../../../assets/Data_Sources_Table.png)

## Typen integraties

U kunt uw gegevens op vier manieren in [!DNL Commerce Intelligence] opnemen: een database verbinden, een SaaS-integratie verbinden, een `.csv` -bestand uploaden of de Adobe-API gebruiken.

## Database-integratie

![ Gegevensbestand \_icons.jpg ](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] steunt op SQL-Gebaseerde en gegevensbestanden NoSQL zoals [ MySQL ](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [ Microsoft SQL ](../integrations/microsoft-sql-server.md), [ MongoDB ](../integrations/mongodb-via-ssh-tunnel.md), en [ PostgreSQL ](../integrations/postgresql.md).

Hoewel u uw database rechtstreeks met [!DNL Commerce Intelligence] kunt verbinden via databasereferenties, raadt de Adobe u aan een bewezen coderingsmethode te gebruiken, zoals een SSH-tunnel. Dit zorgt ervoor dat uw gegevens veilig en veilig blijven aangezien het zijn weg in uw Data Warehouse maakt.

Afhankelijk van de verbindingsmethode en het type van gegevensbestand, zou wat technische deskundigheid kunnen worden vereist om de opstelling te voltooien.

## `SaaS` Integraties

![](../../../assets/SaaS_icons.jpg) pree-commerce-logo.png

`SaaS` integraties zijn services zoals [[!DNL Google Adwords]](../integrations/google-adwords.md) , [[!DNL Salesforce]](../integrations/salesforce.md) en [[!DNL Zendesk]](../integrations/zendesk.md) . Aangezien gegevens van derden op de server van de leverancier aanwezig zijn, kunt u deze niet rechtstreeks benaderen zoals u dat kunt met de gegevens in uw database.

Doorgaans is het instellen van een integratie in [!DNL Commerce Intelligence] net zo eenvoudig als het invoeren van uw accountgegevens. Voor sommige services is mogelijk een API-sleutel vereist om de autorisatie te voltooien. Controle uit de [ integratiesectie ](../integrations/integrations.md) voor instructies bij het produceren van om het even welke geloofsbrieven u wenst.

## Bestand uploaden

Weet u niet zeker hoe u gegevens van een aanvullende bron in uw Data Warehouse kunt krijgen? [ Gebruikend de `File Upload` eigenschap ](../connecting-data/using-file-uploader.md) is een goede manier om in gegevens te trekken die u niet voor dagelijkse besluitvorming vereist. Na de opmaakregels kunt u snel `.csv` bestanden uploaden naar uw Data Warehouse en deze samenvoegen met andere gegevensbronnen.

## [!DNL Commerce Intelligence] `Import API`

Als u het ophalen van gegevens uit een van uw eigen bronnen liever automatiseert, kunt u de instructie [!DNL Commerce Intelligence] `Import API` gebruiken. Als de functie zich niet in een database of een `SaaS` -integratie bevindt, is de functie `Import API` de beste keuze.

Het gebruik van de API vereist een beetje technische expertise - iemand die graag een klein Ruby- of PHP-script schrijft en onderhoudt, is meer dan gekwalificeerd.

Meer leren over het worden begonnen met `Import API`, controleer de [ plaats van de Ontwikkelaar ](https://developer.adobe.com/commerce/services/reporting/) en [ hoe te om een API sleutel ](https://developer.adobe.com/commerce/services/reporting/import-api/) te produceren.

## Integratie toevoegen

Als u een integratie wilt toevoegen, klikt u op **[!UICONTROL Manage Data** > **Connections]** en vervolgens op **[!UICONTROL Add a New Data Source]** . Klik op het pictogram van de integratie dat u wilt toevoegen en volg de instructies in Help-onderwerpen om de volgende zaken in te stellen:

* [ Veelgestelde vragen van de Integratie ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Beschikbaar ](../integrations/integrations.md)
* [Tabellen consolideren](../../../best-practices/consolidating-your-tables.md)
* [Toegang tot uw database beperken](../../../administrator/account-management/restrict-db-access.md)

**ziet geen integratie u wilt?** Sommige integraties moeten worden geactiveerd om zichtbaar te zijn in uw account. Als u iets als [!DNL Facebook] zoekt maar het niet vermeld is, [ voorlegt een steunkaartje ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL) voor.

**als u een foutenstatus voor een integratie** ziet, controleer de [ sectie van het Oplossen van problemen ](https://support.magento.com/hc/en-us/sections/360003078151) voor hulp.
