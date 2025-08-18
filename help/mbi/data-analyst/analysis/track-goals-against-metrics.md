---
title: Doelstellingen bijhouden op basis van cijfers
description: Leer hoe u een dashboard instelt waarmee u uw bedrijfsdoelstellingen kunt bijhouden op basis van uw feitelijke gegevens, zoals inkomsten, nieuwe geregistreerde gebruikers en bestellingen in de loop der tijd.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Doelstellingen bijhouden op basis van prestatiewaarden

De meeste cliënten zouden hun **bedrijfsdoelstellingen** willen volgen, maar realiseren niet dit in [!DNL Adobe Commerce Intelligence] mogelijk is. Dit onderwerp toont aan hoe te opstelling een dashboard dat u zal helpen uw bedrijfsdoelstellingen tegen uw daadwerkelijke gegevens volgen - met inbegrip van opbrengst, nieuwe geregistreerde gebruikers, en orden in tijd. U leert ook hoe u de prestaties van jaar tot jaar kunt vergelijken, allemaal in een dashboard als dit:

![](../../assets/Goals-_dashboard_2.png)

Alvorens begonnen te worden, zou u [ dossier uploader ](../importing-data/connecting-data/using-file-uploader.md) moeten herzien en ervoor zorgen u uw bedrijfsdoelstellingen voor een bepaalde periode hebt bepaald.

## Aan de slag

U moet eerst een bestand uploaden dat specifieke dagelijkse/maandelijkse/driemaandelijkse doelstellingen voor uw bedrijf bevat.

U kunt [ dossier uploader ](../importing-data/connecting-data/using-file-uploader.md) en het beeld gebruiken hieronder om uw dossier te formatteren. De gemeenschappelijkste doelstellingen die cliënten in [!DNL Commerce Intelligence] volgen omvatten Orders, Ontvangsten, en Nieuwe geregistreerde rekeningen.

![](../../assets/Goals-_Excel.png)

## Metrisch

Creeer één nieuwe metrisch voor elk doel. Als u bijvoorbeeld doelstellingen voor maandelijkse inkomsten en bestellingen uploadt, moet u twee nieuwe metriek maken:

* **Maandelijks opbrengstdoel**
* In de tabel **`Monthly goals`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`Revenue target`**
* Besteld door de **`Month`** timestamp

* **Maandelijks doel van orden**
* In de tabel **`Monthly goals`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`Orders target`**
* Besteld door de **`Month`** timestamp

* **Maandelijks nieuw geregistreerd rekeningendoel**
* In de tabel **`Monthly goals`**
* Deze metrisch voert a **Som** uit
* Op de kolom **`New registered accounts target`**
* Besteld door de **`Month`** timestamp

## Rapporten

Het is nuttig om een mengeling van statische waarden en visuele grafieken te hebben wanneer het analyseren van uw doelstellingen. Hieronder staan drie voorbeeldrapporten waarmee u uw inkomstenprestaties kunt gaan volgen.

* **Ontvangsten verlaten om doel** te bereiken
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

* [!UICONTROL Time period]: (Welke relevante tijdsperiode u ook wilt)
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **de doelstellingen van de Inkomsten**
* Metrisch `A`: `Revenue`
* 
  [!UICONTROL Metric]: `Revenue`

* Metrisch `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Metrisch `C`: `Revenue (amount change since previous year)` (hide)
* 
  [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Deze maand vorig jaar)
* 
  [!UICONTROL-formule]: `(A-C)`
* 
  [!UICONTROL Format]: `Currency`

* `Multiple Y-Axes` uitschakelen
* [!UICONTROL Time period]: (Welke relevante tijdsperiode u wilt)*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Zodra u de bovengenoemde rapporten voor opbrengstdoelstellingen hebt voltooid, kunt u identieke rapporten voor doelstellingen rond orden, geregistreerde rekeningen, of om het even welke andere waarden tot stand brengen u in uw doelstellingen uploadt dossier hebt omvat.

Nadat u alle rapporten hebt gecompileerd, kunt u deze naar wens op het dashboard ordenen. Het resultaat ziet er mogelijk uit als de afbeelding boven aan deze pagina.
