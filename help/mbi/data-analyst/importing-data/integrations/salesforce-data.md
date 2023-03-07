---
title: Salesforce-gegevens verwacht
description: Meer informatie over ondersteunde en niet-ondersteunde objecten in Salesforce-gegevens.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Verwacht [!DNL Salesforce] data

[Na de [!DNL Salesforce] installatie is voltooid](../integrations/salesforce.md), een lijst voor elk queryable [object](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - met naam `sf_/\{sobject-name}` - is gemaakt in uw Data Warehouse.

>[!NOTE]
>
>De structuur (kolommen) van elke tabel is afhankelijk van de velden in het object.

Als u een lijst met objecten beschikbaar wilt maken voor uw organisatie, raadpleegt u de [!DNL Salesforce] [Een lijst met objecten-documentatie ophalen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Als u een lijst met objecten hebt, checkt u de [Sectie Betrekkingsdiagram voor entiteiten (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) van [!DNL Salesforce] documentatie om te zien hoe de entiteiten op elkaar betrekking hebben.

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
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
