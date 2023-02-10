---
title: Breedtegraad van dashboard
description: Leer hoe u bulksgewijs alle rapporten op een specifiek dashboard kunt bewerken.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Breedtegraad van dashboard

Met het brede filtreren van het dashboard, kunt u bulksgewijs van alle rapporten op een specifiek dashboard uitgeven. U kunt dezelfde analyse snel bekijken over verschillende tijdsperiodes of voor verschillende winkels. U kunt de prestaties van een vorig jaar, maand, of week per opslag gemakkelijk vergelijken. Bovendien kunt u een volledig dashboard bijwerken om een nieuw gestarte campagne te kunnen plaatsen.

## Datumfilters

Als u het datumbereik of interval van rapporten op een dashboard wilt wijzigen, klikt u op het kalenderpictogram in de rechterbovenhoek (![kalender](../../assets/calendar-button.png)).

U kunt ervoor kiezen om gegevens weer te geven met een `Fixed Date Range` of een variëteit van vooraf berekend `Moving Date Ranges`:

![datumbereiken verplaatsen](../../assets/moving_date_ranges.png)

De `Last Full...` verplaatsingsbereikopties vertegenwoordigen het laatst voltooide bereik, terwijl `This...` wordt het huidige bereik in uitvoering. Als het bijvoorbeeld in juni is, wordt `Last Full Month` is _1 mei - 31 mei_, terwijl `This Month` is _1 juni - Nu_.

Of maak uw eigen `Custom Moving Range`\:

![aangepast bewegingsbereik](../../assets/custom-moving-range.png)

Kies ervoor het interval ook te wijzigen. De standaardknop selecteren (![tijdinterval standaard](../../assets/time_interval_default.png)) betekent dat alleen het datumbereik wordt gewijzigd:

![tijdsinterval](../../assets/time_interval.png)

Als u het begindatumbereik en interval van alle rapporten wilt herstellen, klikt u op **[!UICONTROL Restore Defaults]** of klik op **[!UICONTROL Cancel]**.

Wanneer u een datumfilter voor een dashboard opgeeft, wordt dat filter alleen op dat dashboard toegepast. Deze wordt niet toegepast wanneer u naar andere dashboards navigeert.

>[!NOTE]
>
>Op dit moment `Cohort Reports` en `SQL Reports` zijn niet inbegrepen wanneer het toepassen van veranderingen op een dashboardniveau.

## Filters opslaan

Als u wilt analyseren hoe een bepaalde winkel het doet, klikt u op het pictogram Opslagbestanden in de rechterbovenhoek (![Winkelfilter](../../assets/store-filter.png)). Standaard, `Store Filter` is ingesteld op `All Stores`, die de gegevens van alle [winkelweergaven](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) beschikbaar op je website Handel.

>[!NOTE]
>
>Een opslagfilter wordt in- of uitgeschakeld voor een gehele [!DNL MBI] account. Als een dashboard rapporten bevat die niet door de filter worden beïnvloed, zoals rapporten die niet op om het even welke gegevens van de Handel worden voortgebouwd, werken die rapporten niet bij wanneer de archieffilter wordt toegepast. U kunt [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) als u van mening bent dat een rapport moet worden bijgewerkt op basis van de keuze van de winkel of als u van mening bent dat het filter van uw accountwinkel per ongeluk is uitgeschakeld.

Wanneer u een winkel in het menu `Store Filter`blijft de selectie behouden wanneer u tussen dashboards navigeert. Door uw selectie te behouden, kunt u overal gegevens voor de geselecteerde winkel zien totdat u `All Stores`.

## Filters voor gedeelde dashboards

Voor gedeelde dashboards, als één gebruiker de datumfilter vormt, zullen andere gebruikers met toegang tot het dashboard zien dat de zelfde toegepaste filter. In dit geval is het opslagfilter echter niet van toepassing. Als de dashboardeigenaar het opslagfilter configureert en het dashboard deelt, zal het gevormde opslagfilter niet aan een andere gebruiker blijven. Een gebruiker moet beschikken over [toegang bewerken](../../data-user/dashboards/share-dashboard-with-users.md) naar een dashboard om de dashboardfilters aan te passen.
