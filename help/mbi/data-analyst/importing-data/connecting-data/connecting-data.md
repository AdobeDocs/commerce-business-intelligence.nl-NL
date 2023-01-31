---
title: Uw gegevens verbinden
description: Leer hoe u in Data Warehouse Manager door de tabellen kunt bladeren die u kunt synchroniseren.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Uw gegevens verbinden

In [!DNL MBI], worden gegevensbronnen aangeroepen `integrations`. Na een `integration` is verbonden, kunt u door de tabellen bladeren die beschikbaar zijn voor synchronisatie in Beheer Data Warehouse.

Integraties worden toegevoegd en beheerd met behulp van de `Connections` pagina, die u kunt openen door te klikken **[!UICONTROL Manage Data** > **Connections]**. Hier ziet u een lijst met alle integraties die met uw account zijn verbonden, het integratietype, de status ([!DNL Google Analytics] en [!DNL Data Import API] verbindingen zullen lege statusgebieden hebben), en de laatste tijd een verbindingstest (`Last Connection` Gestart kolom) is uitgevoerd.

![Gegevens\_Bronnen\_Tabel.png](../../../assets/Data_Sources_Table.png)

## Typen integraties

Er zijn vier manieren om uw gegevens in te voeren [!DNL MBI]: een database verbinden, een SaaS-integratie verbinden, een database uploaden `.csv` of gebruik onze API.

## Database-integratie

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] ondersteunt SQL- en NoSQL-databases zoals [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), en [PostgreSQL](../integrations/postgresql.md).

Terwijl u direct uw gegevensbestand kunt verbinden met [!DNL MBI] gebruikend gegevensbestandgeloofsbrieven, adviseren wij u een bewezen encryptiemethode zoals een tunnel van SSH gebruiken. Dit zal ervoor zorgen dat uw gegevens veilig en veilig blijven aangezien het zijn weg in uw gegevenspakhuis maakt.

Afhankelijk van de verbindingsmethode en het type van gegevensbestand, zou wat technische deskundigheid kunnen worden vereist om de opstelling te voltooien.

## `SaaS` Integraties

![](../../../assets/SaaS_icons.jpg)

`SaaS` integratie is diensten zoals [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), en [[!DNL Zendesk]](../integrations/zendesk.md). Het is belangrijk om op te merken dat aangezien de gegevens van derde op de server van de verkoper leven, u niet tot het kunt direct toegang hebben zoals u met de gegevens in uw gegevensbestand kunt.

In de meeste gevallen, vestiging een integratie in [!DNL MBI] is even eenvoudig als het invoeren van uw accountgegevens. Voor sommige services is mogelijk een API-sleutel vereist om de autorisatie te voltooien. [integratiesectie](../integrations/integrations.md) voor instructies over het produceren van om het even welke geloofsbrieven u nodig hebt.

## Bestand uploaden

Weet u niet zeker hoe u gegevens van een aanvullende bron in uw gegevenspakhuis kunt ophalen? [Met de `File Upload` functie](../connecting-data/using-file-uploader.md) is een goede manier om gegevens in te zamelen die u niet nodig hebt voor de dagelijkse besluitvorming. Na het volgen van de opmaakregels kunt u snel uploaden `.csv` dossiers in uw gegevenspakje en sluit zich bij hen met andere gegevensbronnen aan.

## [!DNL MBI] `Import API`

Als u het ophalen van gegevens uit een van uw eigen bronnen liever wilt automatiseren, kunt u de opdracht [!DNL MBI] `Import API`. In feite: als het niet in een database of een `SaaS` integratie, de `Import API` function is jouw beste weddenschap.

Het gebruik van de API vereist een beetje technische expertise - iemand die het schrijven en onderhouden van een klein Ruby- of PHP-script leuk vindt, zal meer dan gekwalificeerd zijn.

Meer informatie over het aan de slag gaan met de `Import API`, bekijk de [Ontwikkelaarssite](https://developer.adobe.com/commerce/services/reporting/) en [hoe te om een API sleutel te produceren](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Integratie toevoegen

Als u een integratie wilt toevoegen, klikt u op **[!UICONTROL Manage Data** > **Connections]** en klik vervolgens op **[!UICONTROL Add a New Data Source]**. Klik op het pictogram van de integratie die u wilt toevoegen en volg de instructies in onze Help-artikelen om de volgende zaken in te stellen:

* [Veelgestelde vragen over integratie](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Beschikbaar ](../integrations/integrations.md)
* [Tabellen consolideren](../../../best-practices/consolidating-your-tables.md)
* [Toegang tot uw database beperken](../../../administrator/account-management/restrict-db-access.md)

**Ziet u niet een gewenste integratie?** Sommige integraties moeten worden geactiveerd om zichtbaar te zijn in uw account. Als u bijvoorbeeld iets zoekt, [!DNL Facebook] - maar niet in de lijst opgenomen, [een ondersteuningsticket indienen](../../../guide-overview.md).

**Als er een foutstatus voor een integratie wordt weergegeven**, niet paniek maken - controleer de [Sectie Problemen oplossen](https://support.magento.com/hc/en-us/sections/360003078151) voor hulp.
