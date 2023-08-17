---
title: Salesforce-gegevens verwacht
description: Leer over gesteunde en niet gesteunde voorwerpen in gegevens Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Verwacht [!DNL Salesforce] data

Na de [[!DNL Salesforce] instellen](../integrations/salesforce.md) is volledig, een lijst voor elk queryable [object](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - met naam `sf_/\{sobject-name}` - is gemaakt in uw Data Warehouse.

>[!NOTE]
>
>De structuur (kolommen) van elke tabel is afhankelijk van de velden in het object.

Raadpleeg de klasse [!DNL Salesforce] [Een lijst met objecten-documentatie ophalen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Als u een lijst met objecten hebt, checkt u de [Sectie Betrekkingsdiagram voor entiteiten (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) van [!DNL Salesforce] documentatie om te zien hoe de entiteiten op elkaar betrekking hebben.

## Niet-ondersteunde objecten

Momenteel [!DNL Salesforce] stelt momenteel de volgende objecten in hun API niet beschikbaar:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Wat is een extern object?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Verwante:

* [Verbinding maken [!DNL Salesforce]](../integrations/salesforce.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
