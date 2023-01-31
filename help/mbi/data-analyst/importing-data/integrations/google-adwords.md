---
title: Connect Google Adwords
description: Leer om campagne ROI te meten door uw reclamekosten en de waarde van de klantenlevensduur (CLV) van gebruikers te vergelijken die van uw campagnes worden verworven.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Verbinden [!DNL Google Adwords]

>[!NOTE]
>
>Vereisten [Beheerdersmachtigingen](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Je deed je onderzoek, je creëerde je advertenties, je lanceerde je campagne. Nu is het tijd om uw advertentie-uitgaven te analyseren en te zien of wordt uw geld effectief besteed. Met behulp van uw advertentiefoutgegevens kunt u [maatregel campagne ROI door uw reclamekosten en de waarde van het klantenleven (CLV) te vergelijken](../../analysis/roi-ad-camp.md) van gebruikers die zijn aangeschaft via uw campagnes.

Laten we beginnen met het invoeren van onze [!DNL Google Adwords] inloggegevens [!DNL MBI]:

1. Ga naar de pagina Verbindingen onder **Gegevens beheren > Integraties**.
1. Klikken **Integratie toevoegen**, rechtsboven in het scherm.
1. Klik op de knop **[!DNL Google Adwords]** pictogram. Hierdoor wordt de [!DNL Google Adwords] aanmeldingspagina.
1. Voer uw [!DNL Google Analytics] referenties. Als het autorisatieproces is voltooid, wordt u teruggeleid naar [!DNL MBI].
1. Er wordt een lijst met profiel-id&#39;s weergegeven. Controleer de profielen waarmee u verbinding wilt maken [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. Wijzigingen worden automatisch opgeslagen, dus klik op **[!UICONTROL Back to Connections]** als u klaar bent.

Als u meerdere profielen hebt en hulp nodig hebt bij het identificeren van welke profielen, raadpleegt u de `Connecting Multiple Google Analytics profiles` hieronder.

## `Connecting multiple Google Analytics profiles`

U hebt mogelijk meerdere websites verbonden met één [!DNL Google Analytics] eigen rekening [!DNL Google Analytics] Profiel-id. In dit geval kunt u al uw profiel-id&#39;s opnemen in [!DNL MBI]. Controleer gewoon de profiel-id&#39;s die u wilt opnemen tijdens de stap voor profielselectie.

**De Google Analytics-id van een bepaalde website identificeren:**

1. Aanmelden [!DNL Google Analytics]
1. Ga naar de specifieke website [!DNL Google Analytics] dashboard
1. Kijk naar de URL. De profiel-id komt overeen met de volgende 8 nummers `p` aan het einde van de regel:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Verbinding verbreken [!DNL Google Adwords]

1. Bezoek uw [!DNL Google] [accountinstellingen](https://www.google.com/accounts/) pagina.
1. Onder de `Security` en klik op **[!UICONTROL edit]** naast `Authorizing` toepassingen en sites.
1. Klikken **[!UICONTROL revoke access]** naast [!DNL MBI].

## Verwante

* [Integraties opnieuw verifiëren](https://support.magento.com/hc/en-us/articles/360016733151)
* [Referentiebron voor bestelling volgen via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Bron van gebruikersverwijzing bijhouden in uw database](../../analysis/google-track-user-acq.md)
* [Gebruikersapparaat, browser en besturingssysteemgegevens bijhouden in uw database](https://support.magento.com/hc/en-us/articles/360016732911)
* [Ontdek uw meest waardevolle aanschafbronnen en kanalen](../../analysis/most-value-source-channel.md)
* [ROI verhogen in uw reclamecampagnes](../../analysis/roi-ad-camp.md)
* [Hoe werkt [!DNL Google Analytics] UTM-toewijzingswerk?](../../analysis/utm-attributes.md)
