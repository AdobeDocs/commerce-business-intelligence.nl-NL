---
title: Zendesk-gegevens verwacht
description: Leer de belangrijkste gegevenstabellen die u van Zendesk in de Intelligentie van de Handel kunt invoeren, met inbegrip van verbindingen aan extra documentatie over gegevens Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Verwacht [!DNL Zendesk] data

Na [u hebt verbinding gemaakt met uw [!DNL Zendesk] account](../integrations/zendesk.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen.

Dit onderwerp verkent de belangrijkste gegevenslijsten die u van kunt invoeren [!DNL Zendesk] in [!DNL Adobe Commerce Intelligence], inclusief koppelingen naar aanvullende documentatie over [!DNL Zendesk] gegevens.

| Tabelnaam | Beschrijving |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | De `Audits` de lijstarchiefactiviteit verbonden aan een kaartje, met inbegrip van statusveranderingen en zowel klant als agentenreacties. Deze lijst omvat kaartje identiteitskaart die terug naar `Tickets` tabel, waarin u de tijd tot eerste reactie en tijd tot resolutie voor elk ticket kunt analyseren. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | De `audit_~\_events` table is het kind van `audits` tabel en registreert aanvullende details van een ticketgebeurtenis. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | De `Organizations` de lijst registreert bedrijfsinformatie over uw eind - gebruikers zoals de naam, identiteitskaart, bijbehorende domeinnamen, markeringen, en om het even welke douanevelden. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | De `Tickets` de tabel registreert alle kaartgegevens, met inbegrip van de `created_at` tijdstempel en de `requester\_id` en `assignee\_id`, waardoor u een ticket kunt koppelen aan een eindgebruiker en een agent in het dialoogvenster `Users` respectievelijk tabel. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | De `ticket fields` de tabel bevat informatie over de basistekstvelden en aangepaste kaartvelden in uw account. De kenmerken van deze tabel bevatten het veld `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, agent- en specifieke informatie voor de eindgebruiker en informatie over het maken en bijwerken van bestanden. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | De `Users` de tabel bevat alle gegevens over eindgebruikers en agents, inclusief de naam en het e-mailadres van de betrokkene. Hierdoor kunt u zowel de betrokkenheid van uw eindgebruikers als de prestaties van uw medewerkers analyseren. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | De groepen zijn hoe de agenten in uw rekening van Zendesk worden georganiseerd. De `Groups` tabelrecordgegevens zoals `group ID`, `URL`, `name`en gegevens maken en bijwerken. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Macro&#39;s zijn acties die door u worden bepaald die de waarden van de gebieden van een kaartje wijzigen. Deze tabel bevat kenmerken zoals de titel, id, handelingen, beperkingen en het maken en bijwerken van gegevens van de macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | De `Tags` de tabel bevat een lijst met alle tags in uw account. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Deze lijst bevat gegevens over kaartenmetriek. Velden bevatten de `ticket ID`, `URL`en het aantal groepen, toewijzers, heropent, antwoorden, antwoordtijd (in notulen), volledige resolutietijd, en laatste update (bijvoorbeeld, status, toegewezen, of aanvrager) informatie. |

{style="table-layout:auto"}

## Verwante

* [Zendesk verbinden](../integrations/zendesk.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
