---
title: Salesforce-gegevens verwacht
description: Meer informatie over ondersteunde en niet-ondersteunde objecten in Salesforce-gegevens.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Verwacht [!DNL Salesforce] data

[Na de [!DNL Salesforce] installatie is voltooid](../integrations/salesforce.md), een lijst voor elk queryable [object](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - met naam `sf_/\{sobject-name}` - wordt gemaakt in uw gegevensopslagruimte.

>[!NOTE]
>
>De structuur (kolommen) van elke tabel is afhankelijk van de velden in het object.

Als u een lijst met objecten beschikbaar wilt maken voor uw organisatie, raadpleegt u de [!DNL Salesforce] [Een lijst met objecten-documentatie ophalen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Als u een lijst met objecten hebt, checkt u de [Sectie Betrekkingsdiagram voor entiteiten (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) van [!DNL Salesforce] documentatie om te zien hoe de entiteiten op elkaar betrekking hebben.

## Niet-ondersteunde objecten

Op dit moment [!DNL Salesforce] stelt momenteel de volgende objecten in hun API niet beschikbaar:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Wat is een extern object?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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
