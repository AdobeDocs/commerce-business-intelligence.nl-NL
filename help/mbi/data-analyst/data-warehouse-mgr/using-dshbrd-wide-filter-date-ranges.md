---
title: Filteren in dashboard-breed
description: Leer hoe u bulksgewijs alle rapporten op een specifiek dashboard kunt bewerken.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Filteren in dashboard-breed

Met het filter voor het hele dashboard kunt u bulkbewerkingen uitvoeren van alle rapporten op een specifiek dashboard. U kunt dezelfde analyse snel bekijken over verschillende tijdsperiodes of voor verschillende winkels. U kunt de prestaties van een vorig jaar, een maand, of een week per opslag gemakkelijk vergelijken. U kunt een volledig dashboard bijwerken om een nieuw gelanceerde campagne aan te passen.

## Datumfilters

Als u het datumbereik of interval van rapporten op een dashboard wilt wijzigen, klikt u op het kalenderpictogram in de rechterbovenhoek (![kalender](../../assets/calendar-button.png)).

U kunt ervoor kiezen om gegevens weer te geven met een `Fixed Date Range` of diverse vooraf berekende `Moving Date Ranges`:

![bewegende datumbereiken](../../assets/moving_date_ranges.png)

De `Last Full...` verplaatsingsbereikopties vertegenwoordigen het laatst voltooide bereik, terwijl `This...` Dit is het huidige bereik dat wordt uitgevoerd. Als het bijvoorbeeld juni is, wordt de `Last Full Month` is _1 mei - 31 mei_, terwijl `This Month` is _1 juni - Nu_.

Of maak uw eigen `Custom Moving Range`\:

![aangepast bewegingsbereik](../../assets/custom-moving-range.png)

Kies ervoor het interval ook te wijzigen. De standaardknop selecteren (![tijdinterval standaard](../../assets/time_interval_default.png)) betekent dat alleen het datumbereik wordt gewijzigd:

![tijdsinterval](../../assets/time_interval.png)

Als u het begindatumbereik en interval van alle rapporten wilt herstellen, klikt u op **[!UICONTROL Restore Defaults]** of klik op **[!UICONTROL Cancel]**.

Wanneer u een datumfilter voor een dashboard opgeeft, wordt dat filter alleen op dat dashboard toegepast. Deze wordt niet toegepast wanneer u naar andere dashboards navigeert.

>[!NOTE]
>
>Momenteel `Cohort Reports` en `SQL Reports` zijn niet inbegrepen wanneer het toepassen van veranderingen op een dashboardniveau.

## Filters opslaan

Als u wilt analyseren hoe een bepaalde winkel het doet, klikt u op het pictogram Opslagbestanden in de rechterbovenhoek (![Winkelfilter](../../assets/store-filter.png)). Standaard, `Store Filter` is ingesteld op `All Stores`, die de gegevens van alle [winkelweergaven](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) beschikbaar op je website Handel.

>[!NOTE]
>
>Een opslagfilter wordt in- of uitgeschakeld voor een gehele [!DNL Commerce Intelligence] account. Als een dashboard rapporten bevat die niet door de filter worden beïnvloed (zoals rapporten die niet op om het even welk worden gebouwd [!DNL Adobe Commerce] gegevens), worden deze rapporten niet bijgewerkt wanneer het opslagfilter wordt toegepast. U kunt [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) als u van mening bent dat een rapport moet worden bijgewerkt op basis van de keuze van de winkel of als u van mening bent dat het filter van uw accountwinkel per ongeluk is uitgeschakeld.

Wanneer u een winkel in het menu `Store Filter`blijft de selectie behouden wanneer u tussen dashboards navigeert. Door uw selectie te behouden, kunt u overal gegevens voor de geselecteerde winkel zien totdat u `All Stores`.

## Filters voor gedeelde dashboards

Voor gedeelde dashboards, als één gebruiker de datumfilter vormt, zien andere gebruikers met toegang tot het dashboard dat de zelfde toegepaste filter. In dit geval is het opslagfilter echter niet van toepassing. Als de eigenaar van het dashboard het opslagfilter configureert en het dashboard deelt, blijft het geconfigureerde opslagfilter niet beschikbaar voor een andere gebruiker. Een gebruiker moet [toegang bewerken](../../data-user/dashboards/share-dashboard-with-users.md) naar een dashboard om de dashboardfilters aan te passen.
