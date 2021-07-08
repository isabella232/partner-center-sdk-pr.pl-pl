---
title: Zasoby faktur
description: Wiele zasobów związanych z fakturami jest dostępnych za pośrednictwem Partner Center API. Te zasoby są powiązane ze szczegółami faktur i pozycji.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b07b7ad14c136eac988eeb12391c24a6cf996b39
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548433"
---
# <a name="invoice-resources"></a>Zasoby faktur

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Następujące zasoby związane z fakturami są dostępne za pośrednictwem Partner Center API.

## <a name="invoice"></a>Faktura

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| identyfikator | ciąg | Identyfikator faktury. |
| invoiceDate | ciąg w formacie daty i czasu UTC | Data wygenerowania faktury. |
| billingPeriodStartDate | ciąg w formacie daty i czasu UTC | Data rozpoczęcia okresu rozliczeniowego w czasie UTC. |
| billingPeriodEndDate | ciąg w formacie daty i czasu UTC   | Data zakończenia okresu rozliczeniowego w czasie UTC. |
| totalCharges | liczba | Łączne opłaty. Obejmuje opłaty za transakcje i wszelkie korekty.     |
| paidAmount | liczba  | Kwota zapłacona przez partnera. Ujemna, jeśli otrzymano płatność.  |
| currencyCode | ciąg  | Kod, który wskazuje walutę używaną dla wszystkich kwot i sum elementów faktury. |
| currencySymbol  | ciąg | Symbol waluty używany dla wszystkich kwot i sum na fakturze. |
| pdfDownloadLink | ciąg  | Link do pobierania faktury w formacie PDF. Ten link nie jest zwracany jako część wyników wyszukiwania i jest wypełniany tylko wtedy, gdy dostęp do faktury jest uzyskiwany za pomocą identyfikatora. Ten link automatycznie wygasa po 30 minutach. |
| invoiceDetails  | tablica [obiektów InvoiceDetail](#invoicedetail)  | Szczegóły faktury.  |
| Zmiany      | tablica [obiektów](#invoice) faktur   | Zmiany w tej fakturze.  |
| Documenttype    | ciąg | Typ dokumentu faktury: "Uwaga kredytowa", "Faktura". |
| nie zmieniaOf        | ciąg | Numer referencyjny dokumentu, którego dokument jest poprawką.  |
| invoiceType     | ciąg  | Typ faktury: "cykliczne", \_ "jednorazowo".   |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks)  | Link do zasobu.  |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.  |

## <a name="invoicedetail"></a>InvoiceDetail

Faktura zawiera kolekcję rozlicznych elementów, a każdy element jest reprezentowany przez zasób InvoiceDetail.

| Właściwość            | Typ                                                           | Opis                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | ciąg                                                         | Typ szczegółów faktury: "brak", "pozycje \_ \_ użycia", "pozycje \_ \_ rozliczeniowe". |
| billingProvider     | ciąg                                                         | Dostawca rozliczeń: "none", "office", "azure" lub "azure \_ data \_ market".         |
| Linki               | [ResourceLinks](utility-resources.md#resourcelinks)           | Link do zasobu.                                                               |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Każda indywidualna opłata na fakturze jest reprezentowana jako InvoiceLineItem.

| Właściwość            | Typ                                                           | Opis                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | ciąg                                                         | Typ pozycji faktury: "brak", "pozycje \_ \_ użycia", "pozycje \_ \_ rozliczeniowe". |
| billingProvider     | ciąg                                                         | Dostawca rozliczeń: "none", "office", "azure" lub "azure \_ data \_ market".            |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Opisuje podsumowanie salda i łącznych opłat na fakturze.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| BalanceAmount            | liczba                                                         | Saldo faktury. Jest to łączna kwota niezapłaconych faktur. |
| currencyCode             | ciąg                                                         | Kod, który wskazuje walutę używaną dla kwoty salda.       |
| currencySymbol           | ciąg                                                         | Użyty symbol waluty.                                             |
| accountingDate           | ciąg w formacie daty i godzin UTC                                 | Data ostatniej aktualizacji kwoty salda.                         |
| firstInvoiceCreationDate | ciąg w formacie daty i godzin UTC                                 | Data utworzenia pierwszej faktury dla klienta.              |
| lastPaymentDate          | ciąg w formacie daty i godzin UTC                                 | Data ostatniej płatności.                                         |
| lastPaymentAmount        | liczba                                                         | Kwota ostatniej płatności.                                       |
| latestInvoiceDate        | ciąg w formacie daty i godzin UTC                                 | Data utworzenia ostatniej faktury dla klienta.               |
| Szczegóły                  | tablica [obiektów InvoiceSummaryDetail](#invoicesummarydetail) | Szczegóły podsumowania faktury.                                           |
| Linki                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Link do zasobu.                                                   |
| atrybuty               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Reprezentuje podsumowanie poszczególnych szczegółów dla typu faktury (na przykład cykliczne, \_ jednorazowo).

| Właściwość            | Typ                                                           | Opis                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | ciąg                                                         | Typ faktury: "cykliczne", \_ "jednorazowo".                                       |
| Podsumowanie             | [InvoiceSummary,](#invoicesummary) obiekt                       | Podsumowanie faktury na typ faktury.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Reprezentuje kolekcję typu [InvoiceSummary,](#invoicesummary) która zawiera szczegółowe informacje dotyczące typu faktury na walutę.

| Właściwość            | Typ                                                           | Opis                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | tablica [obiektów InvoiceSummary](#invoicesummary)             | Podsumowanie faktury na typ faktury na walutę.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Reprezentuje element wiersza rozliczeń faktury dla subskrypcji opartych na licencjach.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| kwota                   | ciąg                                                         | Pobiera lub ustawia łączną kwotę. Łączna kwota = cena jednostkowa * ilość.  |
| atrybuty               | ciąg                                                         | Pobiera atrybuty.                                                  |
| billingCycleType         | ciąg                                                         | Pobiera lub ustawia typ cyklu rozliczeniowego.                                  |
| billingProvider          | ciąg                                                         | Pobiera dostawcę rozliczeń.                                            |
| chargeEndDate            | ciąg w formacie daty i godzin UTC                                 | Pobiera lub ustawia datę zakończenia opłaty.                             |
| chargeStartDate          | ciąg w formacie daty i godzin UTC                                 | Pobiera lub ustawia datę rozpoczęcia opłaty.                           |
| chargeType               | ciąg                                                         | Pobiera lub ustawia typ opłaty.                                      |
| currency                 | ciąg                                                         | Pobiera lub ustawia walutę używaną dla tego elementu wiersza.                    |
| customerId               | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator klienta na platformie rozliczeniowej firmy Microsoft.  |
| Customername             | ciąg w formacie daty i godzin UTC                                 | Pobiera lub ustawia nazwę klienta.                                       |
| Nazwa_domeny               | ciąg                                                         | Pobiera lub ustawia nazwę domeny.                                             |
| durableOfferId           | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator oferty trwałej.                     |
| invoiceLineItemType      | ciąg                                                         | Pobiera typ elementu wiersza faktury.                                   |
| mpnId                    | liczba                                                         | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. W przypadku odsprzedawców bezpośrednich jest to identyfikator MPN odsprzedawcy. W przypadku odsprzedawców pośrednich jest to identyfikator MPN odsprzedawcy dodanej wartości (VAR).                                   |
| offerId                  | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator oferty.                             |
| offerName (nazwa oferty)                | ciąg                                                         | Pobiera lub ustawia nazwę oferty.                                          |
| Idzamówienia                  | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator zamówienia.                             |
| partnerId                | ciąg                                                         | Pobiera lub ustawia identyfikator dzierżawy usługi Azure Active Directory partnera.            |
| quantity                 | liczba                                                         | Pobiera lub ustawia liczbę jednostek skojarzonych z tym elementem wiersza.      |
| subscriptionDescription  | ciąg                                                         | Pobiera lub ustawia opis subskrypcji.                            |
| subscriptionEndDate      | ciąg w formacie daty i czasu UTC                                 | Pobiera lub ustawia datę wygaśnięcia subskrypcji.                      |
| subscriptionId           | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator subskrypcji.                      |
| subscriptionName         | ciąg                                                         | Pobiera lub ustawia nazwę subskrypcji.                                   |
| subscriptionStartDate    | ciąg w formacie daty i czasu UTC                                 | Pobiera lub ustawia datę rozpoczęcia subskrypcji.                   |
| Suma częściowa                 | liczba                                                         | Pobiera lub ustawia kwotę po rabatie.                               |
| syndykacjaPartnerSubscriptionNumber | ciąg                                             | Pobiera lub ustawia numer subskrypcji partnera syndykacji.             |
| Podatku                      | liczba                                                         | Pobiera lub ustawia naliczane podatki.                                       |
| tier2MpnId               | liczba                                                         | Pobiera lub ustawia identyfikator MPN partnera warstwy 2 skojarzonego z tym elementem wiersza. |
| totalForCustomer         | liczba                                                         | Pobiera lub ustawia łączną kwotę po rabatach i podatku.                 |
| totalOtherDiscount       | liczba                                                         | Pobiera lub ustawia rabat skojarzony z tym zakupem.              |
| unitPrice                | liczba                                                         | Pobiera lub ustawia cenę jednostkową.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Reprezentuje element wiersza rozliczeń faktury dla subskrypcji opartych na użyciu.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| atrybuty               | ciąg                                                         | Pobiera atrybuty.                                                  |
| billingCycleType         | ciąg                                                         | Pobiera lub ustawia typ cyklu rozliczeniowego.                                  |
| billingProvider          | ciąg                                                         | Pobiera dostawcę rozliczeń.                                            |
| chargeEndDate            | ciąg w formacie daty i czasu UTC                                 | Pobiera lub ustawia datę zakończenia opłaty.                             |
| chargeStartDate          | ciąg w formacie daty i czasu UTC                                 | Pobiera lub ustawia datę rozpoczęcia opłaty.                           |
| chargeType               | ciąg                                                         | Pobiera lub ustawia typ opłaty.                                      |
| consumedQuantity         | liczba                                                         | Pobiera lub ustawia łączną liczbę zużytych jednostek.                                |
| consumptionDiscount      | ciąg                                                         | Pobiera lub ustawia rabat na zużycie.                             |
| consumptionPrice         | ciąg                                                         | Pobiera lub ustawia cenę zużytej ilości.                          |
| currency                 | ciąg                                                         | Pobiera lub ustawia walutę skojarzoną z cenami.                 |
| Customername             | ciąg                                                         | Pobiera lub ustawia nazwę klienta.                                       |
| customerId               | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator klienta.                          |
| detailLineItemId         | liczba                                                         | Pobiera lub ustawia identyfikator elementu wiersza szczegółów. Jednoznacznie identyfikuje elementy wiersza w przypadkach, w których obliczenie różni się dla zużytych jednostek. Przykład: Opłata za łączną liczbę zużytych zasobów = 1338, 1024 jest naliczana za jedną stawkę, a opłata 314 z inną stawką.        |
| Nazwa_domeny               | ciąg                                                         | Pobiera lub ustawia nazwę domeny.                                             |
| includedQuantity         | liczba                                                         | Pobiera lub ustawia jednostki uwzględnione w kolejności.                         |
| invoiceLineItemType      | ciąg                                                         | Pobiera typ elementu wiersza faktury.                                   |
| invoiceNumber            | ciąg                                                         | Pobiera lub ustawia numer faktury.                                      |
| Listprice                | liczba                                                         | Pobiera lub ustawia cenę każdej jednostki.                                  |
| mpnId                    | liczba                                                         | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. W przypadku odsprzedawców bezpośrednich jest to identyfikator MPN odsprzedawcy. W przypadku odsprzedawców pośrednich jest to identyfikator MPN odsprzedawcy dodanej wartości (VAR).                                   |
| Idzamówienia                  | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator zamówienia.                             |
| overageQuantity          | liczba                                                         | Pobiera lub ustawia ilość zużytą powyżej dozwolonego użycia.               |
| partnerBillableAccountId | ciąg                                                         | Pobiera lub ustawia identyfikator rozliczanego konta partnera.                         |
| partnerId                | ciąg                                                         | Pobiera lub ustawia identyfikator dzierżawy usługi Azure Active Directory partnera.            |
| partnerName              | ciąg                                                         | Pobiera lub ustawia nazwę partnera.                                      |
| postTaxEffectiveRate     | liczba                                                         | Pobiera lub ustawia efektywną cenę po podatkach.                         |
| postTaxTotal             | liczba                                                         | Pobiera lub ustawia łączne opłaty po opodatkowaniu. Opłaty przed opodatkowaniem + kwota podatku |
| preTaxCharges            | liczba                                                         | Pobiera lub ustawia cenę naliczaną przed podatkami.                          |
| preTaxEffectiveRate      | liczba                                                         | Pobiera lub ustawia efektywną cenę przed podatkami.                        |
| region                   | ciąg                                                         | Pobiera lub ustawia region skojarzony z wystąpieniem zasobu.        |
| resourceGuid             | ciąg                                                         | Pobiera lub ustawia identyfikator zasobu.                                 |
| resourceName             | ciąg                                                         | Pobiera lub ustawia nazwę zasobu. Przykład: Baza danych (GB/miesiąc).         |
| Servicename              | ciąg                                                         | Pobiera lub ustawia nazwę usługi. Przykład: Azure Data Service.           |
| Servicetype              | ciąg                                                         | Pobiera lub ustawia typ usługi. Przykład: Azure Usługi SQL Azure DB.           |
| sku                      | ciąg                                                         | Pobiera lub ustawia sku usługi.                                         |
| subscriptionDescription  | ciąg                                                         | Pobiera lub ustawia opis subskrypcji.                            |
| subscriptionId           | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator subskrypcji.                      |
| subscriptionName         | ciąg                                                         | Pobiera lub ustawia nazwę subskrypcji.                                   |
| taxAmount                | liczba                                                         | Pobiera lub ustawia kwotę naliczonego podatku.                               |
| tier2MpnId               | liczba                                                         | Pobiera lub ustawia identyfikator MPN partnera warstwy 2 skojarzonego z tym elementem wiersza. |
| unit                     | ciąg                                                         | Pobiera lub ustawia jednostkę miary dla użycia platformy Azure.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Reprezentuje operacje dostępne na fakturze w pliku application/pdf.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent z contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Reprezentuje element wiersza faktury dla subskrypcji opartych na licencjach.

| Właściwość | Typ | Opis |
| --- | --- | --- |
| PartnerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy partnera. |
| CustomerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy klienta. |
| CustomerName | ciąg | Pobiera lub ustawia nazwę klienta. |
| CustomerDomainName | ciąg | Pobiera lub ustawia nazwę domeny klienta. |
| CustomerCountry | ciąg | Pobiera lub ustawia kraj klienta. |
| InvoiceNumber | ciąg | Pobiera lub ustawia numer faktury. |
| MpnId | ciąg | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. |
| ResellerMpnId | int | Pobiera lub ustawia unikatowy identyfikator zamówienia. |
| OrderDate (Data zamówienia) | DateTime | Pobiera lub ustawia datę utworzenia zamówienia. |
| ProductId | ciąg | Pobiera lub ustawia unikatowy identyfikator produktu. |
| SkuId | ciąg | Pobiera lub ustawia unikatowy identyfikator jednostki SKU. |
| AvailabilityId | ciąg | Pobiera lub ustawia unikatowy identyfikator dostępności. |
| ProductName | ciąg | Pobiera lub ustawia nazwę produktu. |
| SkuName | ciąg | Pobiera lub ustawia nazwę SKU. |
| ChargeType | ciąg | Pobiera lub ustawia typ opłaty. |
| UnitPrice | decimal | Pobiera lub ustawia cenę jednostkową. |
| EffectiveUnitPrice | decimal | Pobiera lub ustawia efektywną cenę jednostkową. |
| Unittype | ciąg | Pobiera lub ustawia typ jednostki. |
| Liczba | int | Pobiera lub ustawia liczbę jednostek skojarzonych z tym elementem wiersza. |
| Suma częściowa | decimal | Pobiera lub ustawia kwotę po rabatie. |
| TaxTotal | decimal | Pobiera lub ustawia naliczane podatki. |
| TotalForCustomer | decimal | Pobiera lub ustawia łączną kwotę po rabatach i podatku. |
| Waluta | ciąg | Pobiera lub ustawia walutę używaną dla tego elementu wiersza. |
| PublisherName | ciąg | Pobiera lub ustawia nazwę wydawcy skojarzoną z tym zakupem. |
| PublisherId | ciąg | Pobiera lub ustawia identyfikator wydawcy skojarzony z tym zakupem. |
| SubscriptionDescription | ciąg | Pobiera lub ustawia opis subskrypcji skojarzony z tym zakupem. |
| SubscriptionId | ciąg | Pobiera lub ustawia identyfikator subskrypcji skojarzony z tym zakupem. |
| ChargeStartDate | DateTime | Pobiera lub ustawia datę rozpoczęcia opłaty skojarzoną z tym zakupem. |
| ChargeEndDate | DateTime | Pobiera lub ustawia datę zakończenia opłaty skojarzoną z tym zakupem. |
| TermAndBillingCycle | ciąg | Pobiera lub ustawia okres i cykl rozliczeniowy skojarzony z tym zakupem. |
| AlternateId | ciąg | Pobiera lub ustawia alternatywny identyfikator (identyfikator oferty). |
| PriceAdjustmentDescription | ciąg | Pobiera lub ustawia opis korekty ceny. |
| CreditReasonCode | ciąg | Pobiera lub ustawia kod przyczyny środków. |
| DiscountDetails | ciąg |  **Przestarzałe .** Pobiera lub ustawia szczegóły rabatu skojarzone z tym zakupem. |
| PricingCurrency | ciąg | Pobiera lub ustawia kod waluty cennika. |
| PCToBCExchangeRate | decimal | Pobiera lub ustawia walutę cennika na kurs wymiany waluty rozliczeniowej. |
| PCToBCExchangeRateDate | DateTime | Pobiera lub ustawia datę kursu wymiany, w którym waluta cenowa została określona na kurs wymiany waluty rozliczeniowej. |
| Ilość rozliczana | decimal | Pobiera lub ustawia zakupione jednostki. Dla każdej kolumny projektu o nazwie **BillableQuantity**. |
| MeterDescription | ciąg | Pobiera lub ustawia opis miernika dla elementu wiersza zużycie. |
| ReservationOrderId | ciąg | Pobiera lub ustawia identyfikator zamówienia rezerwacji dla zakupu wystąpi błądowych platformy Azure. |
| BillingFrequency | ciąg | Pobiera lub ustawia częstotliwość rozliczeń. |
| InvoiceLineItemType | InvoiceLineItemType | Zwraca typ elementu wiersza faktury. |
| BillingProvider | BillingProvider | Zwraca dostawcę rozliczeń. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Reprezentuje nienalizane, rozliczane pozycje uzgodnień dla dziennego użycia ocenianego.

| Właściwość | Typ | Opis |
| --- | --- | --- |
| PartnerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy partnera. |
| PartnerName | ciąg | Pobiera lub ustawia nazwę partnera. |
| CustomerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy klienta, do którego należy użycie. |
| CustomerName | ciąg | Pobiera lub ustawia nazwę firmy klienta, do której należy użycie. |
| CustomerDomainName | ciąg | Pobiera lub ustawia nazwę domeny klienta, do której należy użycie. |
| InvoiceNumber | ciąg | Pobiera lub ustawia identyfikator faktury, do której należy użycie. |
| ProductId | ciąg | Pobiera lub ustawia unikatowy identyfikator produktu. |
| SkuId | ciąg | Pobiera lub ustawia unikatowy identyfikator jednostki SKU. |
| AvailabilityId | ciąg | Pobiera lub ustawia unikatowy identyfikator dostępności. |
| SkuName | ciąg | Pobiera lub ustawia nazwę SKU dla usługi. |
| ProductName | ciąg | Pobiera lub ustawia nazwę produktu. |
| PublisherName | ciąg | Pobiera lub ustawia nazwę wydawcy. |
| PublisherId | ciąg | Pobiera lub ustawia identyfikator wydawcy. |
| SubscriptionId | ciąg | Pobiera lub ustawia identyfikator subskrypcji. |
| SubscriptionDescription | ciąg | Pobiera lub ustawia opis subskrypcji. |
| ChargeStartDate | DateTime | Pobiera lub ustawia datę rozpoczęcia opłaty. |
| ChargeEndDate | DateTime | Pobiera lub ustawia datę zakończenia opłaty. |
| UsageDate | DateTime | Pobiera lub ustawia datę użycia. |
| MeterType (Typ miernika) | ciąg | Pobiera lub ustawia typ miernika. |
| MeterCategory | ciąg | Pobiera lub ustawia kategorię miernika. |
| MeterId | ciąg | Pobiera lub ustawia identyfikator miernika (GUID). |
| MeterSubCategory | ciąg | Pobiera lub ustawia podkategorię miernika. |
| MeterName | ciąg | Pobiera lub ustawia nazwę miernika. |
| MeterRegion | ciąg | Pobiera lub ustawia region miernika. |
| UnitOfMeasure | ciąg | Pobiera lub ustawia jednostkę miary. |
| ResourceLocation | ciąg | Pobiera lub ustawia lokalizację zasobu. |
| ConsumedService | ciąg | Pobiera lub ustawia nazwę używanej usługi. |
| ResourceGroup | ciąg | Pobiera lub ustawia nazwę grupy zasobów. |
| ResourceUri | ciąg | Pobiera lub ustawia URI wystąpienia zasobu, o które chodzi użycie. |
| Tagi | ciąg | Pobiera lub ustawia tagi dodane przez klienta. |
| AdditionalInfo | ciąg | Pobiera lub ustawia metadane specyficzne dla usługi. Na przykład typ obrazu dla maszyny wirtualnej. |
| ServiceInfo1 | ciąg | Pobiera lub ustawia wewnętrzne metadane usługi platformy Azure. |
| ServiceInfo2 | ciąg | Pobiera lub ustawia informacje o usłudze, na przykład typ obrazu dla maszyny wirtualnej i nazwę usługodawcy internetowego dla usługi ExpressRoute. |
| CustomerCountry | ciąg | Pobiera lub ustawia kraj klienta. |
| MpnId | ciąg | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. |
| ResellerMpnId | ciąg | Pobiera lub ustawia identyfikator MPN odsprzedawcy partnera warstwy 2 skojarzonego z tym elementem wiersza. |
| ChargeType | ciąg | Pobiera lub ustawia typ opłaty. |
| UnitPrice | decimal | Pobiera lub ustawia cenę jednostki. |
| Liczba | decimal | Pobiera lub ustawia ilość użycia. |
| Unittype | ciąg | Pobiera lub ustawia typ jednostki (na przykład 1 godzina). |
| BillingPreTaxTotal | decimal | Pobiera lub ustawia rozszerzony koszt lub całkowity koszt przed opodatkowaniem w lokalnej walucie klienta lub waluty rozliczeniowej. |
| BillingCurrency | ciąg | Pobiera lub ustawia walutę ISO, w której miernik jest naliczany w lokalnej walucie klienta lub walucie rozliczeniowej. |
| PricingPreTaxTotal | decimal | Pobiera lub ustawia rozszerzony koszt lub całkowity koszt przed opodatkowaniem w USD lub walucie katalogu używanej do oceny. |
| PricingCurrency | ciąg | Pobiera lub ustawia walutę ISO, w której miernik jest obciążany opłatą w USD lub walucie katalogu używanej do oceny. |
| EntitlementId | ciąg | Pobiera lub ustawia identyfikator uprawnienia (subskrypcji platformy Azure). |
| EntitlementDescription | ciąg | Pobiera lub ustawia opis uprawnienia (subskrypcja platformy Azure). |
| PCToBCExchangeRate | ciąg | Pobiera lub ustawia walutę cennika na kurs wymiany waluty rozliczeniowej. |
| PCToBCExchangeRateDate | DateTime | Pobiera lub ustawia walutę cennika na datę kursu wymiany waluty rozliczeniowej. |
| EffectiveUnitPrice | decimal | Pobiera lub ustawia efektywną cenę jednostkową. |
| RateOfPartnerEarnedCredit | decimal | Pobiera lub ustawia stawkę środków uzyskane przez partnerów. |
| HasPartnerEarnedCredit | bool | Pobiera lub ustawia są stosowane środków uzyskane przez partnera. |
| RateOfCredit | decimal | Pobiera lub ustawia stawkę środków dla danego typu środków. |
| CreditType | ciąg | Pobiera lub ustawia typ środków. |
| InvoiceLineItemType | InvoiceLineItemType | Zwraca typ pozycji faktury. |
| BillingProvider | BillingProvider | Zwraca dostawcę rozliczeń. |
