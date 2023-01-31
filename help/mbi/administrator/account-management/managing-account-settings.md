---
title: Uw accountinstellingen beheren
description: Leer hoe te om een aantal rekeningsmontages voor uw gegevenspakhuis aan te passen.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Uw accountinstellingen aanpassen

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen.](../../administrator/user-management/user-management.md)

In uw [!DNL MBI] account, kunt u een aantal accountinstellingen voor uw gegevensopslagruimte aanpassen. U kunt deze openen door de naam van uw organisatie te selecteren in de rechterbovenhoek van een scherm en vervolgens **[!UICONTROL Account Settings]** in de vervolgkeuzelijst.

* **[!UICONTROL Client Name:]** Deze instelling wordt in de rechterbovenhoek van alle dashboards en elders in uw account weergegeven. Als u wilt wijzigen **[!UICONTROL "Vandelay Industries Co., Ltd]** alleen **[!UICONTROL "Vandelay]** Dat is de juiste weg.

* **[!UICONTROL Currency:]** Dit is het *standaardvaluta* voor alle monetaire waarden in uw account. Telkens wanneer een decimale of valutawaarde in uw gegevenspakje wordt gesynchroniseerd, bepaalt deze instelling het symbool dat vóór die waarde in uw rapporten wordt geplaatst.

* **[!UICONTROL Blackout Hours:]** Dit het plaatsen zorgt ervoor dat, tijdens de geselecteerde uren van de dag, uw gegevenspakhuis geen toegang tot uw verbonden gegevensbestanden heeft. Alle uren worden uitgedrukt bij nul-uur en in Oost StandaardTijd (EST). Als u bijvoorbeeld niet wilt dat uw productiedatabase wordt geopend tussen de uren 9:00 uur EST en 1:00 uur EST, moet u de volgende array met cijfers typen: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Deze instelling zorgt ervoor dat een update voor een gegevenspaket automatisch in uw account wordt gestart *op het uur* u hebt opgegeven. Net als bij de zwartwerktijden zijn deze ook in ET. Bijvoorbeeld, als u de updates van het gegevenspakhuis automatisch wilt beginnen bij **middernacht** en **middag** EST, zou u de volgende serie van cijfers moeten typen: **0,12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Deze optie vertelt het systeem wat te doen in situaties waar een e-mailsamenvatting gepland is te verzenden *vóór de gegevens in een van haar verslagen* wordt vernieuwd tot aan het heden. Als u **Nee**, verzendt uw account het verzenden van de e-mail op het geplande tijdstip en verzendt het in plaats daarvan zodra uw gegevens zijn bijgewerkt. Als u **[!UICONTROL Yes]**, verzendt uw account het e-mailbericht, voegt een bericht toe waarin wordt uitgelegd dat de gegevens niet zijn opgeslagen en verzendt een e-mail zodra uw gegevens zijn bijgewerkt.

* **[!UICONTROL Enable data updates:]** Met deze optie zorgt u ervoor dat gegevensupdates op uw account worden uitgevoerd. Als u de instelling wijzigt in **[!UICONTROL No]**, worden de gegevenssyncs en de kolomberekeningen volledig stopgezet in uw account.

>[!NOTE]
>
>Zorg ervoor dat u **[!UICONTROL Save Customizations]** nadat u wijzigingen hebt aangebracht.
