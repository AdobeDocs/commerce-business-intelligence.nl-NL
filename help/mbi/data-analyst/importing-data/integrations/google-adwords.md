---
title: Connect Google Adwords
description: Leer om campagne ROI te meten door uw reclamekosten en de waarde van de klantenlevensduur (CLV) van gebruikers te vergelijken die van uw campagnes worden verworven.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Verbinden [!DNL Google Adwords]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

U hebt uw onderzoek uitgevoerd, u hebt uw advertenties gemaakt, u hebt uw [!DNL Google] campagne. Nu is het tijd om uw advertentie-uitgaven te analyseren en te zien of wordt uw geld effectief besteed. Met behulp van uw advertentiefoutgegevens kunt u [maatregel campagne ROI door uw reclamekosten en de waarde van het klantenleven (CLV) te vergelijken](../../analysis/roi-ad-camp.md) van gebruikers die zijn aangeschaft via uw campagnes.

Ga aan de slag met je [!DNL Google Adwords] inloggegevens [!DNL Commerce Intelligence].

1. Ga naar de `Connections` pagina onder **Gegevens beheren > Integraties**.
1. Klikken **Integratie toevoegen**, rechtsboven in het scherm.
1. Klik op de knop **[!DNL Google Adwords]** pictogram. Hierdoor wordt het [!DNL Google Adwords] pagina met referenties.
1. Voer uw [!DNL Google Analytics] referenties. Nadat het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL Commerce Intelligence].
1. Een lijst met profiel-id&#39;s. Controleer de profielen waarmee u verbinding wilt maken [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. Wijzigingen worden automatisch opgeslagen, dus klik op **[!UICONTROL Back to Connections]** als u klaar bent.

Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de `Connecting Multiple Google Analytics profiles` hieronder.

## Meerdere verbindingen maken [!DNL Google Analytics] profielen

U hebt mogelijk meerdere websites verbonden met één [!DNL Google Analytics] eigen rekening [!DNL Google Analytics] Profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL Commerce Intelligence]. Controleer de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

**De profiel-id van een bepaalde Google Analytics van een website identificeren:**

1. Aanmelden [!DNL Google Analytics]
1. Ga naar de specifieke website [!DNL Google Analytics] dashboard
1. Kijk naar de URL. De profiel-id komt overeen met de volgende acht nummers `p` aan het einde van de regel:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Verbinding verbreken [!DNL Google Adwords]

1. Bezoek uw [!DNL Google] [accountinstellingen](https://www.google.com/account/about/?hl=en) pagina.
1. Onder de `Security` sectie, klikken **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klik op **[!UICONTROL revoke access]**.

## Verwante

* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Referentiebron voor bestelling volgen via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../../analysis/google-track-user-acq.md)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
* [Hoe werkt [!DNL Google Analytics] UTM-toewijzingswerk?](../../analysis/utm-attributes.md)
