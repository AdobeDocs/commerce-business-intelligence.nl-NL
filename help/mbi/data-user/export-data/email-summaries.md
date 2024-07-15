---
title: Geautomatiseerde e-mailoverzichten maken
description: Leer hoe u geautomatiseerde e-mailoverzichten kunt maken.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Geautomatiseerde e-mailoverzichten maken

E-mailoverzichten zijn een krachtig communicatiemiddel waarmee u de status en trends van uw bedrijf kunt delen met belangrijke betrokkenen. Met e-mailoverzichten kunt u:

* Grafische overzichten e-mailen die rapporten bevatten
* De auteur van het e-mailoverzicht toevoegen aan of uitsluiten van het ontvangen van het e-mailbericht
* Plan wanneer de e-mail wordt verzonden
* Bestaande geplande e-mailsamenvattingen bewerken, verwijderen en pauzeren

## Nieuwe e-mailsamenvatting maken

1. Klik op **[!DNL Manage Data]** en vervolgens op **[!UICONTROL Email Summary]** in het zijpaneel.

   Als dit de eerste keer is dat u een e-mailoverzicht maakt, worden op deze pagina geen opgeslagen samenvattingen weergegeven.

1. Klik op **[!UICONTROL Create New Email Summary]** in de rechterbovenhoek.

1. Voer een naam in voor het overzicht.

   Kies een naam die aangeeft wat in het overzicht staat. Bijvoorbeeld `AOV Comparison` .

1. Selecteer in de sectie `Choose Content` de rapporten die u in het overzicht wilt opnemen.

   U kunt maximaal tien rapporten selecteren die u bezit. Nadat u een rapport hebt geselecteerd, gebruikt u de pictogrammen die worden weergegeven om te selecteren of u dat rapport als een tabel of grafiek wilt verzenden. Als u het rapport hebt opgeslagen als een getal, kunt u het alleen als een getal verzenden. Voor informatie over het verzenden van een e-mailsamenvatting die een rapport met stapelgegevens bevat, zie [ het Leiden uw rekeningsmontages ](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` -rapporten zijn alleen beschikbaar als u de nieuwe architectuur gebruikt.

1. (Optioneel) Selecteer `Send Email To Me` als u het e-mailbericht wilt ontvangen.

1. Als u andere gebruikers in de e-mail wilt opnemen, voert u hun e-mailadressen in het veld `Add Email Recipients` in, gescheiden door komma&#39;s, spaties, tabs of puntkomma&#39;s.

## E-mailoverzicht plannen

In het veld `Set when to send the Email Summary` kunt u opgeven wanneer de e-mailsamenvattingen moeten worden verzonden. De opties zijn:

* `Manual`
* `Once`
* `Repeating`

### E-mailoverzicht opslaan om op een latere datum te worden verzonden

1. Selecteer `Manual` in het veld `Set when to send the Email Summary` .

1. Klik op **[!UICONTROL Save]**.

   Hiermee slaat u de samenvatting op in de lijst met e-mailoverzichten.

1. Als u klaar bent om de samenvatting te verzenden, klikt u op het tandwielpictogram en selecteert u `Send Now` .

### E-mailoverzicht eenmaal verzenden

1. Selecteer `Once` in het veld `Set when to send the Email Summary` .

1. Geef de begindatum op in de `Select Start Date` -kalender.

1. Geef in het veld `Select time to send` de tijd op om de e-mail te verzenden.

### Herhalingsschema maken

1. Selecteer `Repeating` in het veld `Set when to send the Email Summary` .

1. Selecteer `Daily` , `Weekly` of `Monthly` in het veld `Set Frequency` .

1. Geef de begindatum op in de `Select Start Date` -kalender.

1. Geef in het veld `Select time to send` de tijd op om de e-mail te verzenden.

1. (Optioneel) Als u een einddatum wilt opgeven, selecteert u `End Date` en selecteert u de einddatum in de kalender.

## Bestaande e-mailoverzicht wijzigen

Nadat u een e-mailoverzicht hebt gemaakt en opgeslagen, wordt op de pagina `Email Summaries` een lijst met alle opgeslagen samenvattingen weergegeven. U kunt (`+`) elke rij voor meer informatie uitbreiden. De kolommen in deze weergave zijn:

* `Email Name` - Naam van het e-mailoverzicht
* `Content` - Type inhoud in het overzicht, zoals de namen van rapporten. Voor informatie over het verzenden van een e-mailsamenvatting die een rapport met stapelgegevens bevat, zie [ het Leiden uw rekeningsmontages ](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Frequentie, datum en tijd waarop de e-mailsamenvatting wordt verzonden
* `Recipients` - Ontvangers van de e-mailsamenvatting
* `Created Date` - De datum waarop het e-mailoverzicht is gemaakt
* `Status` - `Paused` of `Active`

Klik op het tandwielpictogram rechts van elke rij naar:

* `Send Now` - Hiermee verzendt u het e-mailoverzicht direct naar alle opgegeven ontvangers
* `Edit` - Hiermee kunt u de details van het e-mailoverzicht wijzigen
* `Pause/Active` - Hiermee kunt u de e-mailsamenvatting onderbreken zodat deze niet wordt bezorgd of kunt u de samenvatting inschakelen op basis van de configuratie ervan
* `Delete` - Verwijdert het e-mailoverzicht
