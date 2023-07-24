---
title: Begrijp uw [!DNL Commerce Intelligence] Omgeving
description: Meer informatie over het werken met en het verbeteren van uw [!DNL Commerce Intelligence] milieu.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Uw [!DNL Adobe Commerce Intelligence] Omgeving

Terwijl u uw handelsgegevens analyseert, dient u rekening te houden met deze factoren en algemene misvattingen. Als u hulp nodig hebt om ervoor te zorgen dat u uw schema van de Handel correct gebruikt, aarzel niet om [contactondersteuning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

Veel van uw tabellen bevatten een kolom met de naam `entity\_id`. In elke tabel die een `entity\_id`, wordt die kolom gebruikt om unieke rijen te identificeren.

Elke rij in de `sales\_order` tabel is een unieke volgorde. De primaire sleutel in deze tabel wordt aangeroepen `entity\_id`. Deze kolom kan worden beschouwd als `order\_id`. In een afzonderlijke tabel: `customer\_entity`, vertegenwoordigt elke rij een unieke klant. De primaire sleutel in deze tabel wordt ook wel `entity\_id`, die als `customer\_id`.

In die tabellen: `sales\_order.entity\_id` is niet gelijk aan `customer\_entity.entity\_id`. Dit geldt voor alle sets tabellen die `entity\_id`: `table\_A.entity\_id` is niet gelijk aan `table\_B.entity\_id`.

## [!DNL Guest orders]

Als u klanten toestaat om van uw plaats tot opdracht te geven zonder een rekening (gastorden) te hebben, bevolken die klanten niet als rij in uw `customer\_entity` tabel. Ook, heeft elke orde die door een gast wordt geplaatst ongeldig `customer\_id` waarde op de `sales\_order` tabel.

Daarom als u wenst om het gedrag van uw gasten in tijd te volgen, moeten alle klant-vlakke kolommen op de `sales\_order` tabel, met een klant-id, zoals `customer\_email`.

Als u het `sales\_order` lijst als klantenlijst, moet u dan zorgvuldig zijn wanneer het creëren van klant-vlakke metriek. Bijvoorbeeld, overweeg een metrische gemiddelde levenopbrengst. Dit metrisch wordt gebruikt om de gemiddelde levenopbrengst over uw klantenbasis te identificeren. Dit vereist eerst een nieuwe kolom die, voor elke klant, hun levenopbrengst terugkeert. Dan moet u deze kolom gemiddelde om de gemiddelde levenopbrengst van uw klanten te verkrijgen.

Als u de `customer\_entity` tabel, is elke rij één klant, en elke klant bestaat slechts één keer in die tabel. Daarom wanneer u de kolom van de levenopbrengst hebt, allen moet u gemiddelde metrisch tot stand brengen. Als u echter de opdracht `sales\_order` tabel als uw klantentabel, kan een klant potentieel in talrijke rijen bestaan. Na vestiging zal de kolom van de levenopbrengst, elke orde (rij) die door een bepaalde klant wordt geplaatst tonen dat de levenopbrengst van die klant; maar u wilt slechts die klant eens in uw algemeen gemiddelde metrisch omvatten.

De truc hier is dat u een filter aan metrisch moet toevoegen die u verzekert slechts elke klant één keer omvat. Adobe raadt u aan een filterset met de naam **Klanten die we tellen** dat filtert voor **bestelnummer van de klant = 1** (Bij andere filters moet u mogelijk ongewenste klanten uitsluiten). Het toevoegen van dit filter verzekert u slechts elke klant één keer in klant-vlakke metrisch omvat.

## Producten en categorieën

Producten kunnen meerdere categorieën hebben en categorieën kunnen voor meerdere producten worden gebruikt. Bij het instellen van analyses op categorieniveau moet u dus oppassen dat u de juiste definities gebruikt. Wilt u de topcategorie? Tweede categorie? Wat als het product in veelvoudige top-level categorieën kan vallen?

Stel je een spijkerbroek voor die in drie verschillende categorieniveaus valt, zoals gedefinieerd in een implementatie van Commerce: &#39;Kleding&#39; (hoogste niveau), &#39;Buitendgoedkleding&#39; (tweede niveau) en &#39;Kant&#39; (derde niveau). Je kunt de rubriekprestaties analyseren op basis van het aantal verkochte eenheden. Metrisch u voor deze analyse nodig hebt is _Objecten verkocht_, die op de `sales\_order\_item` tabel. Daarom moet u op categorieniveau informatie op de puntlijst bewegen. Elke rij op de `sales\_order\_item` tabel heeft een koppeling `product\_id`Als u dus weet welke categorieën aan een product zijn gekoppeld, kunt u die gegevens overbrengen naar de gewenste tabel.

Voordat u gegevens kunt verplaatsen, moet u eerst de juiste verbindingen en filters weten om te controleren of u de juiste categorie hebt gekozen. Voor sommige analyses moet u misschien &#39;Kant&#39; weten, maar in andere analyses is &#39;Koud&#39; wellicht geschikter. Dit zijn afzonderlijke categorieën die afzonderlijk worden geïdentificeerd. Als u weet hoe elk categorieniveau is gedefinieerd, kunt u de verkoop per eenheid toewijzen aan de juiste categorie voor uw specifieke analyse.

Stel je voor dat je ook een `Our Favorites` categorie op hoofdniveau op de homepage van uw website. Misschien hebt u uw winkel voor Koophandel geïmplementeerd om deze jeans op te nemen in beide `Clothing` en de `Our Favorites` categorie. Zo ja, dan heeft dit spijkerbroek meer dan één topcategorie. In dat geval verplaatst u één categorie op hoofdniveau naar de `sales\_order\_item` tabel is niet helemaal logisch , omdat er meerdere opties zijn . Om dit te verklaren, stelt Adobe voor ja/neen kolommen te creëren die voor specifieke categorieën controleren. Bijvoorbeeld: `Is product in Clothing category?` en `Is product in Our Favorites category?` kunt u controleren of een product onder die specifieke categorieën valt.
