---
title: QuickBooks-gegevens verwacht
description: Leer hoe u relevante gegevensvelden eenvoudig kunt bijhouden voor analyse.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Verwacht [!DNL QuickBooks] data

![](../../../assets/Quickbooks.png)

Na [u hebt verbinding gemaakt met uw [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen. De volgende lijsten worden gecreeerd in uw Data Warehouse:

Als u alle velden wilt weergeven die u kunt bijhouden, klikt u op de koppelingen in de kolom Tabelnaam.

## Transactieentiteiten {#transactionentities}

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | De rekeningentabel bevat informatie over AP-transacties of een betalingsverzoek van een derde. Tot de kenmerken behoren het valutatype, de wisselkoers, het totale bedrag, de vervaldatum, het saldo en meer. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | Betalingsentiteiten zijn de laatste betalingstransactie van rekeningen die van een verkoper zijn ontvangen. Deze tabel bevat de informatie van de leverancier, het type betaling, het totale bedrag, de transactiedatum en meer. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | In de tabel met creditcards worden transacties geregistreerd die terugbetalingen of kredieten van zowel volledige als gedeeltelijke betalingen zijn. Sommige kenmerken zijn onder andere de naam van de klant, de facturerings- en verzendgegevens van de klant, het bedrag en de datum. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | Deposito&#39;s omvatten directe deposito&#39;s en betalingen aan cli??nten die naar de vermogensoverdrachtenrekening worden overgeboekt nadat ze in de `Undeposited Funds` account. Kenmerken zijn het bedrag, de aanbetaling-id en de datum. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | Schattingen zijn transacties die aan klanten worden gegeven en die de voorgestelde prijs voor een goed of een dienst omvatten. Deze lijst registreert het bedrag, om het even welke kortingsinformatie, klanteninformatie, en datum. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | Facturen zijn verkoopvormen die een klant later betaalt. In de tabel met facturen worden alle aanbetalingsgegevens, de datum, de posten, de belastinggegevens en de klantgegevens vastgelegd. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | De de lijstverslagen van de journaliste AR en AP rekeningsinformatie, met inbegrip van het dagboekingang identiteitskaart, de transactiedatum, en de informatie van het lijnpunt. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Een betalingsrecord bevat kenmerken zoals de betalings-id, toegepaste en niet-toegepaste bedragen, de transactiedatum, het transactietype en de verwerkingsstatus. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | In de tabel met aankopen worden uw kosten weergegeven. Deze tabel bevat de aankoop-id, het type betaling, het bedrag en alle gegevens van het lijstitem. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | Aankooporders zijn aanvragen voor goederen die naar verkopers worden verzonden. Deze tabel bevat de informatie van de leverancier, de inkooporder-id, de transactiedatum, de informatie over het lijstitem, het totale bedrag en AP-accountgegevens. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | In deze tabel worden terugbetalingen aan klanten geregistreerd. Kenmerken zijn onder andere de kwitantie-id, de itemgegevens van de regel, het totale bedrag, de klantgegevens en het saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | In de tabel met verkoopontvangstbewijzen wordt informatie opgenomen in de verkoopopbrengsten die aan klanten worden verstrekt, waaronder de verkoopkwitantie-id, de informatie over de posten, het totale bedrag, de klantgegevens, de transactiedatum en eventuele deposito&#39;s. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | Tijdsactiviteiten zijn tijdrecords voor leveranciers en/of werknemers. De tijdactiviteitstabel bevat de tijd-activiteit-id, de werknemer/leverancier-informatie, de geregistreerde tijd, de beschrijving van de activiteit en de opgenomen datum. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | In de overboekingstabel wordt informatie vastgelegd over de tussen de rekeningen verplaatste middelen. Tot de kenmerken behoren de overdrachtsidentiteitskaart, het bedrag, de accountgegevens en de datum. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Kredieten van leveranciers zijn AP-transacties die terugbetalingen of kredieten zijn die aan leveranciers worden gegeven. De `vendorcredits` de tabel bevat de krediet-id van de leverancier, de informatie over het regelitem, de leverancier, het AP-account, het totale bedrag en de datum. |

{style="table-layout:auto"}

## Naamlijstentiteiten {#namelistentities}

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Deze tabel bevat de account-id, naam, status, type, saldo, valuta en aanmaaktijd. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | In deze tabel worden alle gegevens met betrekking tot bedrijfsbudgetten vastgelegd, waaronder de budgettaire id, naam, begin- en einddatum, type, status en details. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | De klassen, die op detaillijnen van transacties worden toegepast, staan u toe om segmenten te volgen die niet aan een cli??nt of een project gebonden zijn. In deze tabel worden de klasse-id, de naam, de subklasse en de status vastgelegd. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | De tabel met klanten bevat alle informatie met betrekking tot uw klanten, waaronder de id, naam, facturerings- en verzendadressen, het telefoonnummer en het e-mailadres van de klant. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | De afdelings lijst omvat afdelings identiteitskaart, naam, en type (subdepartement vs top-level afdeling). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | De werknemerslijst registreert informatie over de mensen die voor uw bedrijf werken. De attributen omvatten werknemersidentiteitskaart, naam, adres, telefoonaantal, en factureerbare informatie, als het bedrijf loon-toegelaten is. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | De lijst van punten bevat details over producten of de diensten die uw bedrijf verkoopt. Deze tabel bevat de item-id, naam, beschrijving, eenheidsprijs, type, aankoopinformatie, hoeveelheid aan de hand en informatie over de inkomsten- en activaberekening. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | In de tabel met betalingsmethoden wordt de wijze van betaling vastgelegd die voor goederen en diensten is ontvangen. Deze bevat de betalings-id, het type en de naam. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Deze tabel bevat informatie over belastingdiensten, waaronder de ID van het belastingkantoor, en informatie over belastingen voor aankopen en verkopen. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Belastingcodes worden gebruikt om de fiscale status (belastbaar of niet-belastbaar) van producten, diensten en klanten te volgen. De tabel met belastingcodes bevat de fiscaal nummer, naam, beschrijving, status, belastbare status, belastingtarief en belastinggroep. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Belastingtarieven worden gebruikt om belastingverplichtingen te berekenen. Deze tabel bevat de ID van het belastingtarief, de naam, de beschrijving, het tarief, de belastingdienst, en meer. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Deze entiteit vertegenwoordigt de voorwaarden waaronder verkopen plaatsvinden. In de tabel met termen staan de term ID, naam, type, kortingspercentage en dagen met vervaldatum. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | De tabel met leveranciers bevat informatie over de leveranciers die u koopt. Tot de tabelkenmerken behoren de leverancier-id, de bedrijfsnaam, het rekeningnummer, de rekeningsaldo, de status van 1099, het factuuradres, het telefoonnummer, het e-mailadres en het webadres. |

{style="table-layout:auto"}

## Verwante:

* [Verbinding maken [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Integraties opnieuw verifi??ren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
