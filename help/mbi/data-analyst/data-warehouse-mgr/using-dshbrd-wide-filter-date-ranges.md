---
title: Filteren in dashboard-breed
description: Leer hoe u bulksgewijs alle rapporten op een specifiek dashboard kunt bewerken.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Filteren in dashboard-breed

Met het filter voor het hele dashboard kunt u bulkbewerkingen uitvoeren van alle rapporten op een specifiek dashboard. U kunt dezelfde analyse snel bekijken over verschillende tijdsperiodes of voor verschillende winkels. U kunt de prestaties van een vorig jaar, een maand, of een week per opslag gemakkelijk vergelijken. U kunt een volledig dashboard bijwerken om een nieuw gelanceerde campagne aan te passen.

## Datumfilters

Om de datumwaaier of het interval van rapporten over een dashboard te veranderen, klik het kalenderpictogram in de hoger-juiste hoek (![ kalender ](../../assets/calendar-button.png)).

U kunt gegevens weergeven met een `Fixed Date Range` of verschillende vooraf berekende `Moving Date Ranges` :

![ bewegende datumwaaiers ](../../assets/moving_date_ranges.png)

De opties voor het `Last Full...` bewegende bereik vertegenwoordigen het laatst voltooide bereik, terwijl `This...` het huidige, actieve bereik is. Bijvoorbeeld, als het Juni is, is `Last Full Month` _1 Mei - 31 Mei_, terwijl `This Month` 1 van juni is - nu _._

Of maak uw eigen `Custom Moving Range`\:

![ douane bewegende waaier ](../../assets/custom-moving-range.png)

Kies ervoor het interval ook te wijzigen. Het selecteren van de standaardknoop (![ gebrek van het tijdinterval ](../../assets/time_interval_default.png)) betekent dat slechts de datumwaaier verandert:

![ tijdinterval ](../../assets/time_interval.png)

Als u het begindatumbereik en interval van alle rapporten wilt herstellen, klikt u op **[!UICONTROL Restore Defaults]** of op **[!UICONTROL Cancel]** .

Wanneer u een datumfilter voor een dashboard opgeeft, wordt dat filter alleen op dat dashboard toegepast. Deze wordt niet toegepast wanneer u naar andere dashboards navigeert.

>[!NOTE]
>
>`Cohort Reports` en `SQL Reports` worden momenteel niet opgenomen wanneer u wijzigingen op dashboardniveau toepast.

## Filters opslaan

Om te analyseren hoe een specifieke opslag uitvoert, klik het opslagpictogram in de hoger-juiste hoek (![ Filter van de Opslag ](../../assets/store-filter.png)). Door gebrek, `Store Filter` wordt geplaatst aan `All Stores`, die de gegevens van alle [ opslagmeningen ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) beschikbaar in uw plaats van Commerce toont.

>[!NOTE]
>
>Een opslagfilter wordt in- of uitgeschakeld voor een volledige [!DNL Commerce Intelligence] -account. Als een dashboard rapporten bevat die niet door het filter worden beïnvloed (zoals rapporten die niet op om het even welke [!DNL Adobe Commerce] gegevens worden voortgebouwd), werken die rapporten niet bij wanneer de archieffilter wordt toegepast. U kunt [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) als u gelooft dat een rapport zou moeten bijwerken gebaseerd op archiefselectie of als u gelooft dat uw filter van de rekeningsopslag incorrect gehandicapt is.

Wanneer u een winkel selecteert in de `Store Filter` , behoudt het filter uw selectie wanneer u tussen dashboards navigeert. Door uw selectie te behouden, kunt u overal gegevens voor de geselecteerde winkel zien totdat u `All Stores` selecteert.

## Filters voor gedeelde dashboards

Voor gedeelde dashboards, als één gebruiker de datumfilter vormt, zien andere gebruikers met toegang tot het dashboard dat de zelfde toegepaste filter. In dit geval is het opslagfilter echter niet van toepassing. Als de eigenaar van het dashboard het opslagfilter configureert en het dashboard deelt, blijft het geconfigureerde opslagfilter niet beschikbaar voor een andere gebruiker. Een gebruiker moet [ hebben toegang ](../../data-user/dashboards/share-dashboard-with-users.md) tot een dashboard uitgeven om de dashboardfilters aan te passen.
