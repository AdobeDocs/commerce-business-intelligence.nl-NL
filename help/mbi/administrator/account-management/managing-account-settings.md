---
title: Uw accountinstellingen beheren
description: Leer hoe u uw accountinstellingen kunt aanpassen voor uw Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Uw accountinstellingen aanpassen

>[!NOTE]
>
>Vereist [ toestemmingen Admin.](../../administrator/user-management/user-management.md)

In uw [!DNL Commerce Intelligence] -account kunt u uw accountinstellingen aanpassen voor uw Data Warehouse. U kunt deze openen door de naam van uw organisatie te selecteren in de rechterbovenhoek van een scherm en vervolgens **[!UICONTROL Account Settings]** te kiezen in het vervolgkeuzemenu.

* **[!UICONTROL Client Name:]** Deze instelling wordt in de rechterbovenhoek van alle dashboards en elders in uw account weergegeven. Als u **[!UICONTROL "Vandelay Industries Co., Ltd]** wilt wijzigen in **[!UICONTROL "Vandelay]** , doet u dat op deze manier.

* **[!UICONTROL Currency:]** Dit is de *standaardmunt* voor alle monetaire waarden in uw rekening. Telkens wanneer een decimale of valutawaarde in uw Data Warehouse wordt gesynchroniseerd, bepaalt deze instelling het symbool dat voor die waarde in uw rapporten wordt geplaatst.

* **[!UICONTROL Blackout Hours:]** Met deze instelling zorgt u ervoor dat uw Data Warehouse tijdens de geselecteerde uren van de dag geen toegang heeft tot uw verbonden databases. Alle uren worden uitgedrukt bij nul-uur en in Oost StandaardTijd (EST). Bijvoorbeeld, als u uw productiegegevensbestand niet tussen de uren van 9 :00 EST en 1 :00 p.m. EST wilt worden betreden, zou u de volgende serie van cijfers moeten typen: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Dit het plaatsen zorgt ervoor dat een update van Data Warehouse automatisch in uw rekening *tijdens de uren* begint u hebt gespecificeerd. Net als bij de zwartwerktijden zijn deze ook in ET. Bijvoorbeeld, als u de updates van Data Warehouse automatisch bij **middernacht** en **Midden** EST wilt beginnen, zou u de volgende serie van cijfers moeten typen: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Deze optie beheert situaties wanneer een e-mailsamenvatting *moet verzenden alvorens de gegevens in één van zijn rapporten* worden verfrist. Als u **Nr** kiest, slaat uw rekening het verzenden van e-mail op zijn geplande tijd over. In plaats daarvan verzendt uw account de gegevens nadat deze zijn bijgewerkt. Als u **[!UICONTROL Yes]** kiest, verzendt uw account de e-mail, bevat het een bericht waarin wordt uitgelegd dat de gegevens niet zijn opgeslagen en wordt een e-mail verzonden zodra uw gegevens zijn bijgewerkt.

* **[!UICONTROL Enable data updates:]** Met deze optie zorgt u ervoor dat gegevensupdates op uw account worden uitgevoerd. Als u de instelling wijzigt in **[!UICONTROL No]** , worden de gegevenssynchronisatie en de kolomberekeningen gestopt in uw account.

>[!NOTE]
>
>Selecteer **[!UICONTROL Save Customizations]** nadat u wijzigingen hebt aangebracht.
