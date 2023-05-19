---
title: QuickBooks-gegevens verwacht
description: Leer hoe u relevante gegevensvelden eenvoudig kunt bijhouden voor analyse.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# Verwacht [!DNL QuickBooks] data

Na [u hebt verbinding gemaakt met uw [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md)kunt u de [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) relevante gegevensvelden voor analyse gemakkelijk te volgen. De volgende lijsten worden gecreeerd in uw Data Warehouse:

Als u alle velden wilt weergeven die u kunt bijhouden, klikt u op de koppelingen in de kolom Tabelnaam.

## Transactieentiteiten {#transactionentities}

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | De `bills` de tabel bevat informatie over AP-transacties of een betalingsverzoek van een derde. Tot de kenmerken behoren het valutatype, de wisselkoers, het totale bedrag, de vervaldatum, het saldo en meer. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` entiteiten zijn de laatste betalingstransactie van rekeningen die van een verkoper zijn ontvangen. Deze tabel bevat de informatie van de leverancier, het type betaling, het totale bedrag, de transactiedatum en meer. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | De `creditmemos` in een tabel worden transacties geregistreerd die terugbetalingen of kredieten van zowel volledige als gedeeltelijke betalingen zijn. Sommige kenmerken zijn onder andere de naam van de klant, de facturerings- en verzendgegevens van de klant, het bedrag en de datum. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` omvat directe deposito&#39;s en betalingen aan klanten die naar de vermogensoverdrachtenrekening worden overgeboekt nadat zij in de `Undeposited Funds` account. Kenmerken omvatten het bedrag, de deposito-id en de datum. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` zijn transacties die aan klanten worden gegeven die voorgestelde prijzen voor een goed of een dienst omvatten. Deze lijst registreert het bedrag, om het even welke kortingsinformatie, klanteninformatie, en datum. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` zijn verkoopvormen die een klant later betaalt. In de tabel met facturen worden alle aanbetalingsgegevens, de datum, de posten, de belastinggegevens en de klantgegevens vastgelegd. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | De `journalentries` de lijstverslagen AR en AP rekeningsinformatie, met inbegrip van het dagboekingang identiteitskaart, de transactiedatum, en de informatie van het lijnpunt. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | A `payment` record bevat kenmerken zoals de betalings-id, toegepaste en niet-toegepaste bedragen, de transactiedatum, het transactietype en de verwerkingsstatus. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | De `purchases` de tabel geeft uw uitgaven weer en bevat de aankoop-id, het type betaling, het bedrag en eventuele informatie over lijstitems. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | De `purchaseorders` de tabel bevat aanvragen voor goederen die aan verkopers worden verzonden . Deze tabel bevat de informatie van de leverancier, de inkooporder-id, de transactiedatum, de informatie over het lijstitem, het totale bedrag en AP-accountgegevens. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | De `refundreceipts` een tabel met terugbetalingen aan klanten. Kenmerken zijn onder andere de kwitantie-id, de itemgegevens van de regel, het totale bedrag, de klantgegevens en het saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | De `salesreceipts` de tabel bevat informatie over de verkoopopbrengsten die aan klanten worden verstrekt, waaronder de ontvangstbewijzen-ID, de gegevens over de posten, het totaalbedrag, de klantgegevens, de transactiedatum en eventuele deposito&#39;s. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | De `timeactivities` de lijst houdt tijdverslagen voor verkopers en/of werknemers en omvat de tijd identiteitskaart van de activiteit, werknemer/verkopersinformatie, geregistreerde tijd, activiteitenbeschrijving, en geregistreerde datum. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | De `transfers` de tabel bevat gegevens over de tussen de rekeningen verplaatste middelen. Tot de kenmerken behoren de overdrachtsidentiteitskaart, het bedrag, de accountgegevens en de datum. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Kredieten van leveranciers zijn AP-transacties die terugbetalingen of kredieten zijn die aan leveranciers worden gegeven. De `vendorcredits` de tabel bevat de krediet-id van de leverancier, de informatie over het regelitem, de leverancier, het AP-account, het totale bedrag en de datum. |

{style="table-layout:auto"}

## Naamlijstentiteiten {#namelistentities}

| **Tabelnaam** | **Beschrijving** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Deze tabel bevat de account-id, naam, status, type, saldo, valuta en aanmaaktijd. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | In deze tabel worden alle gegevens met betrekking tot bedrijfsbudgetten vastgelegd, waaronder de budgettaire id, naam, begin- en einddatum, type, status en details. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | De klassen, die op detaillijnen van transacties worden toegepast, staan u toe om segmenten te volgen die niet aan een cliënt of een project gebonden zijn. In deze tabel worden de klasse-id, de naam, de subklasse en de status vastgelegd. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | De `customers` de tabel bevat alle informatie met betrekking tot uw klanten, waaronder de id, naam, facturerings- en verzendadressen, het telefoonnummer en het e-mailadres van de klant. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | De `departments` de lijst omvat afdelings identiteitskaart, naam, en type (subdepartment vs top-level afdeling). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | De `employees` de lijst registreert informatie over de mensen die voor uw bedrijf werken. De attributen omvatten werknemersidentiteitskaart, naam, adres, telefoonaantal, en factureerbare informatie, als het bedrijf loon-toegelaten is. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | De `items` de lijst bevat details over producten of de diensten die uw bedrijf verkoopt. Deze tabel bevat de item-id, naam, beschrijving, eenheidsprijs, type, aankoopinformatie, hoeveelheid aan de hand en informatie over de inkomsten- en activaberekening. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | De `paymentmethods` in de tabel wordt de wijze van betaling voor goederen en diensten vermeld . Deze bevat de betalings-id, het type en de naam. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Deze tabel bevat informatie over belastingdiensten, waaronder de ID van het belastingkantoor, en informatie over belastingen voor aankopen en verkopen. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Belastingcodes worden gebruikt om de fiscale status (belastbaar of niet-belastbaar) van producten, diensten en klanten te volgen. De `taxcodes` de tabel bevat de fiscaal nummer ID, naam, beschrijving, status, belastbare status, belastingtarief en belastinggroep. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Belastingtarieven worden gebruikt om belastingverplichtingen te berekenen. Deze tabel bevat de ID van het belastingtarief, de naam, de beschrijving, het tarief, de belastingdienst, en meer. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Deze entiteit vertegenwoordigt de voorwaarden waaronder verkopen plaatsvinden. In de tabel met termen staan de term ID, naam, type, kortingspercentage en dagen met vervaldatum. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | De tabel met leveranciers bevat informatie over de leveranciers die u koopt. Tot de tabelkenmerken behoren de leverancier-id, de bedrijfsnaam, het rekeningnummer, de rekeningsaldo, de status van 1099, het factuuradres, het telefoonnummer, het e-mailadres en het webadres. |

{style="table-layout:auto"}

## Verwante:

* [Verbinding maken [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Integraties opnieuw verifiëren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
