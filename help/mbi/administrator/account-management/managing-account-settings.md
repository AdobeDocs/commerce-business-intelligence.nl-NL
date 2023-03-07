---
title: Uw accountinstellingen beheren
description: Leer hoe u uw accountinstellingen voor uw Data Warehouse kunt aanpassen.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Uw accountinstellingen aanpassen

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen.](../../administrator/user-management/user-management.md)

In uw [!DNL MBI] -account, kunt u uw accountinstellingen aanpassen voor uw Data Warehouse. U kunt deze openen door de naam van uw organisatie te selecteren in de rechterbovenhoek van een scherm en vervolgens **[!UICONTROL Account Settings]** in de vervolgkeuzelijst.

* **[!UICONTROL Client Name:]** Deze instelling wordt in de rechterbovenhoek van alle dashboards en elders in uw account weergegeven. Als u wilt wijzigen **[!UICONTROL "Vandelay Industries Co., Ltd]** alleen **[!UICONTROL "Vandelay]** Dat is de juiste weg.

* **[!UICONTROL Currency:]** Dit is het *standaardvaluta* voor alle monetaire waarden in uw account. Telkens wanneer een decimale of valutawaarde in uw Data Warehouse wordt gesynchroniseerd, bepaalt deze instelling het symbool dat voor die waarde in uw rapporten wordt geplaatst.

* **[!UICONTROL Blackout Hours:]** Deze instelling zorgt ervoor dat uw Data Warehouse tijdens de geselecteerde uren van de dag geen toegang heeft tot de verbonden databases. Alle uren worden uitgedrukt bij nul-uur en in Oost StandaardTijd (EST). Als u bijvoorbeeld niet wilt dat uw productiedatabase wordt geopend tussen de uren 9:00 uur EST en 1:00 uur EST, moet u de volgende array met cijfers typen: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Deze instelling zorgt ervoor dat er automatisch een update van de Data Warehouse in uw account wordt gestart *gedurende de uren* u hebt opgegeven. Net als bij de zwartwerktijden zijn deze ook in ET. Als u bijvoorbeeld wilt dat updates van de Data Warehouse automatisch beginnen bij **middernacht** en **middag** EST, zou u de volgende serie van cijfers moeten typen: **0,12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Met deze optie worden situaties beheerd waarin een e-mailoverzicht wordt verzonden *vóór de gegevens in een van haar verslagen* wordt vernieuwd. Als u **Nee**, uw account slaat het verzenden van het e-mailbericht op het geplande tijdstip over. In plaats daarvan verzendt uw account de gegevens nadat deze zijn bijgewerkt. Als u **[!UICONTROL Yes]**, verzendt uw account de e-mail, bevat een bericht waarin wordt uitgelegd dat de gegevens niet zijn opgeslagen en verzendt een andere e-mail zodra uw gegevens zijn bijgewerkt.

* **[!UICONTROL Enable data updates:]** Met deze optie zorgt u ervoor dat gegevensupdates op uw account worden uitgevoerd. Als u de instelling wijzigt in **[!UICONTROL No]**, gegevenssyncs en kolomberekeningen worden gestopt in uw account.

>[!NOTE]
>
>Zorg ervoor dat u **[!UICONTROL Save Customizations]** nadat u wijzigingen hebt aangebracht.
