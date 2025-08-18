---
title: QuickBooks-gegevens verwacht
description: Leer hoe u relevante gegevensvelden eenvoudig kunt bijhouden voor analyse.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# [!DNL QuickBooks] gegevens verwacht

Nadat [ u uw  [!DNL QuickBooks]  rekening ](../../../data-analyst/importing-data/integrations/quickbooks.md) hebt verbonden, kunt u de [ Manager van Data Warehouse ](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) gebruiken om relevante gegevensgebieden voor analyse gemakkelijk te volgen. De volgende tabellen worden gemaakt in uw Data Warehouse:

Als u alle velden wilt weergeven die u kunt bijhouden, klikt u op de koppelingen in de kolom Tabelnaam.

## Transactieentiteiten {#transactionentities}

| **Naam van de Lijst** | **Beschrijving** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | De tabel `bills` bevat informatie over AP-transacties of een betalingsaanvraag van een derde. Tot de kenmerken behoren het valutatype, de wisselkoers, het totale bedrag, de vervaldatum, het saldo en meer. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` -entiteiten zijn de laatste betalingstransactie van rekeningen die van een leverancier zijn ontvangen. Deze tabel bevat de informatie van de leverancier, het type betaling, het totale bedrag, de transactiedatum en meer. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | In de tabel `creditmemos` worden transacties vastgelegd die terugbetalingen of crediteringen van zowel volledige als gedeeltelijke betalingen zijn. Sommige kenmerken zijn onder andere de naam van de klant, de facturerings- en verzendgegevens van de klant, het bedrag en de datum. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` omvat directe deposito&#39;s en betalingen van klanten die naar de Asset Account worden verplaatst nadat ze op de `Undeposited Funds` -rekening zijn aangehouden. Kenmerken omvatten het bedrag, de deposito-id en de datum. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` zijn transacties die worden gegeven aan klanten die voorgestelde prijzen voor een goed of service bevatten. Deze lijst registreert het bedrag, om het even welke kortingsinformatie, klanteninformatie, en datum. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` zijn verkoopformulieren die een klant later betaalt. In de tabel met facturen worden alle aanbetalingsgegevens, de datum, de posten, de belastinggegevens en de klantgegevens vastgelegd. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | In de `journalentries` -tabel worden AR- en AP-accountgegevens vastgelegd, waaronder de journaal-entry-id, de transactiedatum en de informatie over lijstitems. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Een `payment` -record bevat kenmerken zoals de betalings-id, toegepaste en niet-toegepaste bedragen, de transactiedatum, het transactietype en de verwerkingsstatus. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | De tabel `purchases` geeft uw kosten weer en bevat de aankoop-id, het type betaling, het bedrag en alle informatie over lijnobjecten. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | De tabel `purchaseorders` bevat aanvragen voor goederen die naar leveranciers zijn verzonden. Deze tabel bevat de informatie van de leverancier, de inkooporder-id, de transactiedatum, de informatie over het lijstitem, het totale bedrag en AP-accountgegevens. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | In de tabel `refundreceipts` worden terugbetalingen aan klanten vastgelegd. Kenmerken zijn onder andere de kwitantie-id, de itemgegevens van de regel, het totale bedrag, de klantgegevens en het saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | In de tabel van `salesreceipts` wordt informatie vastgelegd over de verkoopopbrengsten die aan klanten worden gegeven, zoals de kwitantie-id, de gegevens van het lijnitem, het totale bedrag, de klantgegevens, de transactiedatum en eventuele deposito&#39;s. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | De tabel `timeactivities` bevat tijdrecords voor leveranciers en/of werknemers en bevat de id van de tijdactiviteit, werknemers-/leveranciersinformatie, geregistreerde tijd, beschrijving van de activiteit en opgenomen datum. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | In de tabel `transfers` wordt informatie vastgelegd over fondsen die tussen accounts zijn verplaatst. Tot de kenmerken behoren de overdrachtsidentiteitskaart, het bedrag, de accountgegevens en de datum. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Kredieten van leveranciers zijn AP-transacties die terugbetalingen of kredieten zijn die aan leveranciers worden gegeven. De tabel `vendorcredits` bevat de krediet-id van de leverancier, informatie over regelitems, informatie over de leverancier, AP-account, totaal bedrag en datum. |

{style="table-layout:auto"}

## Naamlijstentiteiten {#namelistentities}

| **Naam van de Lijst** | **Beschrijving** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Deze tabel bevat de account-id, naam, status, type, saldo, valuta en aanmaaktijd. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | In deze tabel worden alle gegevens met betrekking tot bedrijfsbudgetten vastgelegd, waaronder de budgettaire id, naam, begin- en einddatum, type, status en details. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | De klassen, die op detaillijnen van transacties worden toegepast, staan u toe om segmenten te volgen die niet aan een cliënt of een project gebonden zijn. In deze tabel worden de klasse-id, de naam, de subklasse en de status vastgelegd. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | De tabel `customers` bevat alle informatie over uw klanten, zoals de id, naam, facturerings- en verzendadressen, het telefoonnummer en het e-mailadres van de klant. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | De tabel `departments` bevat de afdelings-id, naam en type (subafdeling versus afdeling op hoofdniveau). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | De tabel `employees` bevat informatie over de personen die voor uw bedrijf werken. De attributen omvatten werknemersidentiteitskaart, naam, adres, telefoonaantal, en factureerbare informatie, als het bedrijf loon-toegelaten is. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | De tabel `items` bevat gegevens over producten of services die uw bedrijf verkoopt. Deze tabel bevat de item-id, naam, beschrijving, eenheidsprijs, type, aankoopinformatie, hoeveelheid aan de hand en informatie over de inkomsten- en activaberekening. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | In de tabel `paymentmethods` wordt de wijze van betaling vastgelegd die voor goederen en services is ontvangen. Deze bevat de betalings-id, het type en de naam. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Deze tabel bevat informatie over belastingdiensten, waaronder de ID van het belastingkantoor, en informatie over belastingen voor aankopen en verkopen. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Belastingcodes worden gebruikt om de fiscale status (belastbaar of niet-belastbaar) van producten, diensten en klanten te volgen. De tabel `taxcodes` bevat de fiscaal nummer, naam, beschrijving, status, belastbare status, belastingtarief en belastinggroep. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Belastingtarieven worden gebruikt om belastingverplichtingen te berekenen. Deze tabel bevat de ID van het belastingtarief, de naam, de beschrijving, het tarief, de belastingdienst, en meer. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Deze entiteit vertegenwoordigt de voorwaarden waaronder verkopen plaatsvinden. In de tabel met termen staan de term ID, naam, type, kortingspercentage en dagen met vervaldatum. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | De tabel met leveranciers bevat informatie over de leveranciers die u koopt. Tot de tabelkenmerken behoren de leverancier-id, de bedrijfsnaam, het rekeningnummer, de rekeningsaldo, de status van 1099, het factuuradres, het telefoonnummer, het e-mailadres en het webadres. |

{style="table-layout:auto"}

## Verwante:

* [Verbinding maken  [!DNL QuickBooks]](../integrations/quickbooks.md)
* [ Reauthenticating integrations ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
