---
title: Salesforce-gegevens verwacht
description: Meer informatie over ondersteunde en niet-ondersteunde objecten in Salesforce-gegevens.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# [!DNL Salesforce] gegevens verwacht

Nadat de [[!DNL Salesforce]  opstelling &#x200B;](../integrations/salesforce.md) volledig is, wordt een lijst voor elk queryable [&#x200B; voorwerp &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - genoemd `sf_/\{sobject-name}` - gecreeerd in uw Data Warehouse.

>[!NOTE]
>
>De structuur (kolommen) van elke tabel is afhankelijk van de velden in het object.

Om een lijst van voorwerpen beschikbaar aan uw organisatie te krijgen, verwijs naar [!DNL Salesforce] [&#x200B; een Lijst van de documentatie van Objecten &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm) krijgt. Nadat u een lijst van voorwerpen hebt, controleer uit de [&#x200B; sectie van het Diagram van de Verhouding van de Entiteit (ERD) &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) van [!DNL Salesforce] documentatie om te zien hoe de entiteiten op elkaar betrekking hebben.

## Niet-ondersteunde objecten

Momenteel worden de volgende objecten in de API van [!DNL Salesforce] niet beschikbaar gemaakt:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [&#x200B; wat een Extern Voorwerp is?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

* [Verbinding maken  [!DNL Salesforce]](../integrations/salesforce.md)
* [&#x200B; Reauthenticating integrations &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
