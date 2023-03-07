---
title: Doelstellingen bijhouden op basis van cijfers
description: Leer hoe u een dashboard instelt waarmee u uw bedrijfsdoelstellingen kunt bijhouden op basis van uw feitelijke gegevens, zoals inkomsten, nieuwe geregistreerde gebruikers en bestellingen in de loop der tijd.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Doelstellingen bijhouden op basis van prestatiemetriek

De meeste klanten willen hun **bedrijfsdoelstellingen**, maar dit is niet mogelijk in [!DNL MBI]. In dit artikel ziet u hoe u een dashboard kunt instellen waarmee u uw bedrijfsdoelstellingen kunt bijhouden op basis van uw feitelijke gegevens, waaronder inkomsten, nieuwe geregistreerde gebruikers en bestellingen in de loop der tijd. U leert ook hoe u de prestaties van jaar tot jaar kunt vergelijken, allemaal in een dashboard als dit:

![](../../assets/Goals-_dashboard_2.png)

Voordat u aan de slag gaat, wilt u zich vertrouwd maken met de [uploader bestand](../importing-data/connecting-data/using-file-uploader.md) en zorg ervoor u uw bedrijfsdoelstellingen voor een bepaalde periode hebt bepaald.

## Aan de slag

U moet eerst een bestand uploaden dat specifieke dagelijkse/maandelijkse/driemaandelijkse doelstellingen voor uw bedrijf bevat.

U kunt de [uploader bestand](../importing-data/connecting-data/using-file-uploader.md) en de afbeelding hieronder om het bestand op te maken. De gemeenschappelijkste doelstellingen die de cliënten binnen volgen [!DNL MBI] inclusief bestellingen, inkomsten en nieuwe geregistreerde accounts.

![](../../assets/Goals-_Excel.png)

## Metrisch

Creeer één nieuwe metrisch voor elk doel. Als u bijvoorbeeld doelstellingen voor maandelijkse inkomsten en bestellingen uploadt, moet u twee nieuwe metriek maken:

* **Maandelijkse inkomstendoelstelling**
* In de **`Monthly goals`** table
* Deze maatstaf voert een **Som**
* Op de **`Revenue target`** kolom
* Besteld door de **`Month`** tijdstempel

* **Doel van maandelijkse bestellingen**
* In de **`Monthly goals`** table
* Deze maatstaf voert een **Som**
* Op de **`Orders target`** kolom
* Besteld door de **`Month`** tijdstempel

* **Doel van maandelijkse nieuwe geregistreerde accounts**
* In de **`Monthly goals`** table
* Deze maatstaf voert een **Som**
* Op de **`New registered accounts target`** kolom
* Besteld door de **`Month`** tijdstempel

## Rapporten

Zoals altijd, is het nuttig om een mengeling van statische waarden en visuele grafieken te hebben wanneer het analyseren van uw doelstellingen. Hieronder staan drie voorbeeldrapporten waarmee u uw inkomstenprestaties kunt gaan volgen.

* **Resterende inkomsten om doel te bereiken**
* Metrisch `A`: `Revenue`
* 

   [!UICONTROL Metric]: `Revenue`

* Metrisch `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!UICONTROL-formule]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (Welke relevante tijdsperiode u wilt gebruiken)
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Inkomstendoelstellingen**
* Metrisch `A`: `Revenue`
* 

   [!UICONTROL Metric]: `Revenue`

* Metrisch `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Metrisch `C`: `Revenue (amount change since previous year)` (verbergen)
* 
   [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Deze maand vorig jaar)
* 
   [!UICONTROL-formule]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* Uitschakelen `Multiple Y-Axes`
* [!UICONTROL Time period]: (Welke relevante tijdsperiode u wilt gebruiken)*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Zodra u de bovengenoemde rapporten voor opbrengstdoelstellingen hebt voltooid, kunt u identieke rapporten voor doelstellingen rond orden, geregistreerde rekeningen, of om het even welke andere waarden tot stand brengen u in uw doelstellingen uploadt dossier hebt omvat.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat ziet er mogelijk uit als de afbeelding boven aan deze pagina.
