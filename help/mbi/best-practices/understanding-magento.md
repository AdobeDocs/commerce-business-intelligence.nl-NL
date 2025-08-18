---
title: Begrijp uw  [!DNL Commerce Intelligence]  Milieu
description: Leer over het werken met en het verbeteren van uw  [!DNL Commerce Intelligence]  milieu.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Uw [!DNL Adobe Commerce Intelligence] -omgeving

Terwijl u uw handelsgegevens analyseert, dient u rekening te houden met deze factoren en algemene misvattingen. Als u hulp met het ervoor zorgen nodig hebt u uw schema van Commerce correct gebruikt, aarzel niet aan [ contactsteun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=nl-NL).

## [!DNL entity\_id]

Veel van uw tabellen bevatten een kolom met de naam `entity\_id` . In elke tabel die een `entity\_id` bevat, wordt die kolom gebruikt om unieke rijen te identificeren.

Elke rij in de tabel `sales\_order` is bijvoorbeeld een unieke volgorde. De primaire sleutel in deze tabel wordt `entity\_id` genoemd. Deze kolom kan worden beschouwd als `order\_id` . In een afzonderlijke tabel, `customer\_entity` , vertegenwoordigt elke rij een unieke klant. De primaire sleutel in deze tabel wordt ook `entity\_id` genoemd, wat als `customer\_id` kan worden beschouwd.

In deze tabellen is `sales\_order.entity\_id` niet gelijk aan `customer\_entity.entity\_id` . Dit geldt voor alle sets tabellen die `entity\_id` bevatten: `table\_A.entity\_id` is niet gelijk aan `table\_B.entity\_id` .

## [!DNL Guest orders]

Als u klanten toestaat om van uw plaats tot opdracht te geven zonder een rekening (gastorden) te hebben, bevolken die klanten niet als rij in uw `customer\_entity` lijst. Elke volgorde die door een gast wordt geplaatst, heeft bovendien de waarde null `customer\_id` in de `sales\_order` -tabel.

Daarom als u het gedrag van uw gasten in tijd wilt volgen, moeten alle klant-vlakke kolommen op de `sales\_order` lijst worden berekend, gebruikend een klant herkenningsteken zoals `customer\_email`.

Als u de `sales\_order` lijst als klantenlijst gebruikt, moet u dan zorgvuldig zijn wanneer het creëren van klant-vlakke metriek. Bijvoorbeeld, overweeg een metrische gemiddelde levenopbrengst. Dit metrisch wordt gebruikt om de gemiddelde levenopbrengst over uw klantenbasis te identificeren. Dit vereist eerst een nieuwe kolom die, voor elke klant, hun levenopbrengst terugkeert. Dan moet u deze kolom gemiddelde om de gemiddelde levenopbrengst van uw klanten te verkrijgen.

Als u de tabel `customer\_entity` kunt gebruiken, is elke rij één klant en bestaat elke klant slechts één keer in die tabel. Daarom wanneer u de kolom van de levenopbrengst hebt, allen moet u gemiddelde metrisch tot stand brengen. Als u de tabel `sales\_order` echter gebruikt als uw klantentabel, kan een klant mogelijk in meerdere rijen bestaan. Na vestiging zal de kolom van de levenopbrengst, elke orde (rij) die door een bepaalde klant wordt geplaatst tonen dat de levenopbrengst van die klant; maar u wilt slechts die klant één keer in uw algemeen gemiddelde metrisch omvatten.

De truc hier is dat u een filter aan metrisch moet toevoegen die u verzekert slechts elke klant één keer omvat. Adobe moedigt u aan om een genoemde filterreeks **Klanten tot stand te brengen en te gebruiken wij** tellen die filters voor **de ordeaantal van de Klant = 1** (onder andere filters u ongewenste klanten kunt moeten uitsluiten). Het toevoegen van dit filter verzekert u slechts elke klant één keer in klant-vlakke metrisch omvat.

## Producten en categorieën

Producten kunnen meerdere categorieën hebben en categorieën kunnen voor meerdere producten worden gebruikt. Bij het instellen van analyses op categorieniveau moet u dus oppassen dat u de juiste definities gebruikt. Wilt u de topcategorie? Tweede categorie? Wat als het product in veelvoudige top-level categorieën kan vallen?

Stel je een spijkerbroek voor die in drie verschillende categorieniveaus valt, zoals gedefinieerd in een Commerce-implementatie: &#39;Kleding&#39; (hoogste niveau), &#39;Buitendgoedkleding&#39; (tweede niveau) en &#39;Kant&#39; (derde niveau). Je kunt de rubriekprestaties analyseren op basis van het aantal verkochte eenheden. Metrisch u voor deze analyse nodig hebt is _Verkochte Punten_, die op de `sales\_order\_item` lijst wordt voortgebouwd. Daarom moet u op categorieniveau informatie op de puntlijst bewegen. Aan elke rij in de tabel `sales\_order\_item` is een `product\_id` gekoppeld. Als u dus weet welke categorieën aan een product zijn gekoppeld, kunt u die informatie overbrengen naar de gewenste tabel.

Voordat u gegevens kunt verplaatsen, moet u eerst de juiste verbindingen en filters weten om te controleren of u de juiste categorie hebt gekozen. Voor sommige analyses moet u misschien &#39;Kant&#39; weten, maar in andere analyses is &#39;Koud&#39; wellicht geschikter. Dit zijn afzonderlijke categorieën die afzonderlijk worden geïdentificeerd. Als u weet hoe elk categorieniveau is gedefinieerd, kunt u de verkoop per eenheid toewijzen aan de juiste categorie voor uw specifieke analyse.

Stel nu dat u ook een categorie op hoofdniveau `Our Favorites` op de homepage van uw website hebt. Mogelijk hebt u uw Commerce-winkel geïmplementeerd om deze jeans op te nemen in de categorie `Clothing` en `Our Favorites` . Zo ja, dan heeft dit spijkerbroek meer dan één topcategorie. In dat geval heeft het niet echt zin één categorie op hoofdniveau naar de tabel `sales\_order\_item` te verplaatsen, omdat er meerdere opties zijn. Om dit te verantwoorden, stelt Adobe voor ja/nee-kolommen te maken die voor specifieke categorieën controleren. Met de kolommen `Is product in Clothing category?` en `Is product in Our Favorites category?` kunt u bijvoorbeeld controleren of een product in die specifieke categorieën valt.
