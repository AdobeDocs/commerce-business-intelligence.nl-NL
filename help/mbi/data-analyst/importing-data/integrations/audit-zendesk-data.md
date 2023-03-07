---
title: Audit Zendesk-gegevens
description: Leer de stappen voor het exporteren van uw Zendesk-gegevens.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Audit Zendesk-gegevens

Iets vreemds gevonden in je [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? Om de kwestie te identificeren, moet u uw gegevens onderzoeken. Dit kan worden gedaan door uw [!DNL Zendesk] gegevens naar een downloadbaar bestand.

## Gegevens exporteren inschakelen

Het exporteren van gegevens is momenteel niet voor alle toepassingen ingeschakeld [!DNL Zendesk] rekeningen. U activeert deze functie als volgt: [een ondersteuningsticket indienen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), met vermelding van uw [!DNL Zendesk] subdomeinnaam.

>[!NOTE]
>
>Alleen `Enterprise` en `Plus` plannen hebben momenteel toegang tot deze functie .

Nadat het exporteren van gegevens is ingeschakeld, kunnen alleen beheerders in een specifiek e-maildomein gegevens van uw [!DNL Zendesk] account. Dit e-maildomein is doorgaans hetzelfde e-maildomein als uw [!DNL Zendesk]. Het e-maildomein van de eigenaar van de account wordt als standaard gebruikt, maar u kunt het domein desgewenst wijzigen.

## Exporteren naar een downloadbaar bestand

1. Klik op het pictogram Beheerder (tandwiellogo) op de zijbalk en kies **[!UICONTROL Manage** > **Reports]**.
1. Klik op de knop **[!UICONTROL Export]** tab.
1. Klikken **[!UICONTROL Request file]** naast Volledige XML exporteren, zoals in de onderstaande afbeelding wordt getoond.

   Op dit punt, begint een bouwstijl; u wordt via e-mail op de hoogte gesteld wanneer het voltooit.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Klik op de koppeling in uw e-mailbericht om een ZIP-bestand met het rapport te downloaden.

   Deze downloadkoppeling is ten minste drie dagen geldig.

Tijdens dit proces wordt een XML-bestand gemaakt dat alle informatie bevat die in de huidige [!DNL Zendesk] -account, inclusief kaartgegevens (met opmerkingen), gebruikersgegevens en accountgegevens. U kunt nu [een ondersteuningsticket indienen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (zorg dat u dit bestand bijvoegt!) zodat u uw gegevens nader kunt bekijken. Als het bestand te groot is, deelt u het met de [!DNL MBI] team via [!DNL Dropbox] of [!DNL Google Drive].

Meer informatie over [!DNL Zendesk] bestand export, raadpleeg de officiële [[!DNL Zendesk] exportdocumentatie](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
