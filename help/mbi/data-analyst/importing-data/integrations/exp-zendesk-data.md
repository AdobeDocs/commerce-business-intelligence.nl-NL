---
title: Zendesk-gegevens verwacht
description: Leer de belangrijkste gegevenstabellen die u van Zendesk in Commerce Intelligence kunt invoeren, met inbegrip van verbindingen aan extra documentatie over gegevens Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!DNL Zendesk] gegevens verwacht

Nadat [ u uw  [!DNL Zendesk]  rekening ](../integrations/zendesk.md) hebt verbonden, kunt u de [ Manager van Data Warehouse ](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen.

In dit onderwerp worden de belangrijkste gegevenstabellen besproken die u vanuit [!DNL Zendesk] kunt importeren in [!DNL Adobe Commerce Intelligence] , inclusief koppelingen naar aanvullende documentatie over [!DNL Zendesk] -gegevens.

| Tabelnaam | Beschrijving |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | De `Audits` lijst registreert activiteit verbonden aan een kaartje, met inbegrip van statusveranderingen en zowel klant als agentenreacties. Deze tabel bevat een ticket-id die terugkoppelt naar de tabel `Tickets` , waarmee u de tijd tot de eerste reactie en de tijd tot de resolutie voor elk ticket kunt analyseren. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | De `audit_~\_events` -tabel is het onderliggende element van de `audits` -tabel en bevat aanvullende gegevens over een ticketgebeurtenis. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | In de tabel `Organizations` worden bedrijfsgegevens vastgelegd over uw eindgebruikers, zoals de naam, id, gekoppelde domeinnamen, tags en aangepaste velden. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | De tabel `Tickets` bevat alle kaartgegevens, inclusief de `created_at` timestamp en de `requester\_id` and `assignee\_id` , waarmee u een ticket kunt koppelen aan een eindgebruiker en agent in de tabel `Users` . |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | De tabel `ticket fields` bevat informatie over de standaardtekstvelden en aangepaste kaartvelden in uw account. Kenmerken van deze tabel zijn onder andere het veld `ID` , `URL` , `type` , `title` , `description` , `position` , `requirement setting` , informatie die specifiek is voor de agent en de eindgebruiker, en informatie over het maken en bijwerken. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | De tabel `Users` bevat alle gegevens over eindgebruikers en agents, inclusief de naam en het e-mailadres van de persoon. Hierdoor kunt u zowel de betrokkenheid van uw eindgebruikers als de prestaties van uw medewerkers analyseren. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | De groepen zijn hoe de agenten in uw rekening van Zendesk worden georganiseerd. In de tabel `Groups` worden gegevens vastgelegd zoals de gegevens `group ID` , `URL` , `name` en het maken en bijwerken van gegevens. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Macro&#39;s zijn acties die door u worden bepaald die de waarden van de gebieden van een kaartje wijzigen. Deze tabel bevat kenmerken zoals de titel, id, handelingen, beperkingen en het maken en bijwerken van gegevens van de macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | De tabel `Tags` bevat een lijst met alle tags in uw account. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Deze lijst bevat gegevens over kaartenmetriek. Velden bevatten de gegevens `ticket ID` , `URL` en het aantal groepen, toewijzingen, heropent, antwoorden, reactietijd (in minuten), volledige resolutietijd en laatste update (bijvoorbeeld status, toegewezen of aanvrager). |

{style="table-layout:auto"}

## Verwante

* [Zendesk verbinden](../integrations/zendesk.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=nl-NL)
