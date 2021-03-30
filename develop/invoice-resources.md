---
title: Zasoby faktury
description: Wiele zasobów związanych z fakturą jest dostępnych za pomocą interfejsów API Centrum partnerskiego. Te zasoby są powiązane z danymi faktury i elementów wiersza.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8977b3b649cd930bb517965572d0efe51d6985a0
ms.sourcegitcommit: 4ec053c56fd210b174fe657aa7b86faf4e2b5a7c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/29/2021
ms.locfileid: "105730216"
---
# <a name="invoice-resources"></a>Zasoby faktury

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Poniższe zasoby związane z fakturą są dostępne za pomocą interfejsów API Centrum partnerskiego.

## <a name="invoice"></a>Faktura

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| identyfikator | ciąg | Identyfikator faktury. |
| invoiceDate | ciąg w formacie daty i godziny UTC | Data wygenerowania faktury. |
| billingPeriodStartDate | ciąg w formacie daty i godziny UTC | Data rozpoczęcia okresu rozliczeniowego w formacie UTC. |
| billingPeriodEndDate | ciąg w formacie daty i godziny UTC   | Data końcowa okresu rozliczeniowego w formacie UTC. |
| totalCharges | liczba | Suma opłat. Obejmuje opłaty za transakcje i wszelkie zmiany.     |
| paidAmount | liczba  | Kwota zapłacona przez partnera. Wartość ujemna, jeśli płatność została odebrana.  |
| currencyCode | ciąg  | Kod, który wskazuje walutę używaną dla wszystkich kwot i sum elementu faktury. |
| currencySymbol  | ciąg | Symbol waluty używany dla wszystkich kwot i sum elementu faktury. |
| pdfDownloadLink | ciąg  | Link umożliwiający pobranie faktury w formacie PDF. Ten link nie jest zwracany jako część wyników wyszukiwania i jest wypełniany tylko wtedy, gdy dostęp do faktury odbywa się według identyfikatora. Ten link zostanie wygaśnie w ciągu 30 minut. |
| invoiceDetails  | Tablica obiektów [InvoiceDetail](#invoicedetail)  | Szczegóły faktury.  |
| zmianę      | Tablica obiektów [faktur](#invoice)   | Zmiany tej faktury.  |
| documentType    | ciąg | Typ dokumentu faktury: "Nota kredytowa", "faktura". |
| amendsOf        | ciąg | Numer referencyjny dokumentu, którego dotyczy zmiana.  |
| invoicetype     | ciąg  | Typ faktury: "cykliczne", "jednorazowe \_ ".   |
| linki           | [ResourceLinks](utility-resources.md#resourcelinks)  | Linki do zasobów.  |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.  |

## <a name="invoicedetail"></a>InvoiceDetail

Faktura zawiera kolekcję elementów rozliczanych, a każdy element jest reprezentowany przez zasób InvoiceDetail.

| Właściwość            | Typ                                                           | Opis                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | ciąg                                                         | Typ faktury szczegóły: "Brak", " \_ elementy linii użycia \_ ", " \_ elementy wiersza rozliczenia \_ ". |
| billingProvider     | ciąg                                                         | Dostawca rozliczeń: "none", "Office", "Azure" lub "Azure \_ Data \_ Market".         |
| linki               | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów.                                                               |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Każda opłata indywidualna w ramach faktury jest reprezentowana jako InvoiceLineItem.

| Właściwość            | Typ                                                           | Opis                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | ciąg                                                         | Typ elementu wiersza faktury: "Brak", " \_ elementy linii użycia \_ ", " \_ elementy wiersza rozliczenia \_ ". |
| billingProvider     | ciąg                                                         | Dostawca rozliczeń: "none", "Office", "Azure" lub "Azure \_ Data \_ Market".            |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Zawiera opis podsumowania salda i łącznego kosztu faktury.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | liczba                                                         | Saldo faktury. Jest to łączna liczba niepłatnych rachunków. |
| currencyCode             | ciąg                                                         | Kod, który wskazuje walutę używaną dla kwoty salda.       |
| currencySymbol           | ciąg                                                         | Używany symbol waluty.                                             |
| accountingDate           | ciąg w formacie daty i godziny UTC                                 | Data ostatniej aktualizacji salda.                         |
| firstInvoiceCreationDate | ciąg w formacie daty i godziny UTC                                 | Data utworzenia pierwszej faktury dla klienta.              |
| lastPaymentDate          | ciąg w formacie daty i godziny UTC                                 | Data ostatniej płatności.                                         |
| lastPaymentAmount        | liczba                                                         | Kwota ostatniej płatności.                                       |
| latestInvoiceDate        | ciąg w formacie daty i godziny UTC                                 | Data utworzenia ostatniej faktury dla klienta.               |
| uzyskać                  | Tablica obiektów [InvoiceSummaryDetail](#invoicesummarydetail) | Szczegóły podsumowania faktury.                                           |
| linki                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Linki do zasobów.                                                   |
| atrybuty               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Przedstawia podsumowanie szczegółowych informacji o typie faktury (na przykład cyklicznie, jeden \_ raz).

| Właściwość            | Typ                                                           | Opis                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoicetype         | ciąg                                                         | Typ faktury: "cykliczne", "jednorazowe \_ ".                                       |
| Podsumowanie             | Obiekt [InvoiceSummary](#invoicesummary)                       | Podsumowanie faktury dla typu faktury.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Reprezentuje kolekcję typu [InvoiceSummary](#invoicesummary) , która zawiera szczegółowe informacje o typie faktury na walutę.

| Właściwość            | Typ                                                           | Opis                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | Tablica obiektów [InvoiceSummary](#invoicesummary)             | Podsumowanie faktury według typu faktury na walutę.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Przedstawia element linii rozliczeniowej faktury dla subskrybowanych subskrypcji opartych na licencji.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| kwota                   | ciąg                                                         | Pobiera lub ustawia łączną kwotę. Łączna kwota = cena jednostkowa * ilość.  |
| atrybuty               | ciąg                                                         | Pobiera atrybuty.                                                  |
| billingCycleType         | ciąg                                                         | Pobiera lub ustawia typ cyklu rozliczeniowego.                                  |
| billingProvider          | ciąg                                                         | Pobiera dostawcę rozliczeń.                                            |
| chargeEndDate            | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia datę końcową opłaty.                             |
| chargeStartDate          | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia datę początkową dla opłaty.                           |
| chargeType               | ciąg                                                         | Pobiera lub ustawia typ opłaty.                                      |
| currency                 | ciąg                                                         | Pobiera lub ustawia walutę używaną dla tego elementu wiersza.                    |
| customerId               | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator klienta na platformie rozliczeń firmy Microsoft.  |
| customerName             | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia nazwę klienta.                                       |
| domainName               | ciąg                                                         | Pobiera lub ustawia nazwę domeny.                                             |
| durableOfferId           | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator oferty trwałej.                     |
| invoiceLineItemType      | ciąg                                                         | Pobiera typ elementu faktury.                                   |
| mpnId                    | liczba                                                         | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. W przypadku bezpośrednich odsprzedawców jest to identyfikator MPN odsprzedawcy. W przypadku pośrednich odsprzedawców jest to MPN identyfikator wartości dodanej Odsprzedawcy (VAR).                                   |
| offerId                  | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator oferty.                             |
| offerName                | ciąg                                                         | Pobiera lub ustawia nazwę oferty.                                          |
| Wartooć                  | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator kolejności.                             |
| partnerId                | ciąg                                                         | Pobiera lub ustawia identyfikator dzierżawy usługi Azure Active Directory partnera.            |
| quantity                 | liczba                                                         | Pobiera lub ustawia liczbę jednostek skojarzonych z tym elementem wiersza.      |
| subscriptionDescription  | ciąg                                                         | Pobiera lub ustawia opis subskrypcji.                            |
| subscriptionEndDate      | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia datę wygaśnięcia subskrypcji.                      |
| subscriptionId           | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator subskrypcji.                      |
| subscriptionName         | ciąg                                                         | Pobiera lub ustawia nazwę subskrypcji.                                   |
| subscriptionStartDate    | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia datę rozpoczęcia subskrypcji.                   |
| Suma częściowa                 | liczba                                                         | Pobiera lub ustawia kwotę po rabacie.                               |
| syndicationPartnerSubscriptionNumber | ciąg                                             | Pobiera lub ustawia numer subskrypcji partnera zespolonego.             |
| podatkowych                      | liczba                                                         | Pobiera lub ustawia opłaty za podatki.                                       |
| tier2MpnId               | liczba                                                         | Pobiera lub ustawia identyfikator MPN partnera warstwy 2 skojarzonego z tym elementem wiersza. |
| totalForCustomer         | liczba                                                         | Pobiera lub ustawia łączną kwotę po rabacie i podatku.                 |
| totalOtherDiscount       | liczba                                                         | Pobiera lub ustawia rabat skojarzony z tym zakupem.              |
| unitPrice                | liczba                                                         | Pobiera lub ustawia cenę jednostkową.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Przedstawia element wiersza rozliczenia faktury dla subskrypcji opartych na użyciu.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| atrybuty               | ciąg                                                         | Pobiera atrybuty.                                                  |
| billingCycleType         | ciąg                                                         | Pobiera lub ustawia typ cyklu rozliczeniowego.                                  |
| billingProvider          | ciąg                                                         | Pobiera dostawcę rozliczeń.                                            |
| chargeEndDate            | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia datę końcową opłaty.                             |
| chargeStartDate          | ciąg w formacie daty i godziny UTC                                 | Pobiera lub ustawia datę początkową dla opłaty.                           |
| chargeType               | ciąg                                                         | Pobiera lub ustawia typ opłaty.                                      |
| consumedQuantity         | liczba                                                         | Pobiera lub ustawia łączną liczbę zużytych jednostek.                                |
| consumptionDiscount      | ciąg                                                         | Pobiera lub ustawia rabat dla zużycia.                             |
| consumptionPrice         | ciąg                                                         | Pobiera lub ustawia cenę zużytej ilości.                          |
| currency                 | ciąg                                                         | Pobiera lub ustawia walutę skojarzoną z cenami.                 |
| customerName             | ciąg                                                         | Pobiera lub ustawia nazwę klienta.                                       |
| customerId               | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator klienta.                          |
| detailLineItemId         | liczba                                                         | Pobiera lub ustawia identyfikator elementu szczegółów wiersza. Jednoznacznie identyfikuje elementy wiersza dla przypadków, w których obliczenia różnią się w przypadku zużytych jednostek. Przykład: całkowita liczba zużytych = 1338, 1024 jest naliczana z jedną stawką, 314 jest naliczana przy użyciu innej stawki.        |
| domainName               | ciąg                                                         | Pobiera lub ustawia nazwę domeny.                                             |
| includedQuantity         | liczba                                                         | Pobiera lub ustawia jednostki uwzględnione w zamówieniu.                         |
| invoiceLineItemType      | ciąg                                                         | Pobiera typ elementu faktury.                                   |
| invoiceNumber            | ciąg                                                         | Pobiera lub ustawia numer faktury.                                      |
| listPrice                | liczba                                                         | Pobiera lub ustawia cenę każdej jednostki.                                  |
| mpnId                    | liczba                                                         | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. W przypadku bezpośrednich odsprzedawców jest to identyfikator MPN odsprzedawcy. W przypadku pośrednich odsprzedawców jest to MPN identyfikator wartości dodanej Odsprzedawcy (VAR).                                   |
| Wartooć                  | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator kolejności.                             |
| overageQuantity          | liczba                                                         | Pobiera lub ustawia ilość wykorzystaną powyżej dozwolonego użycia.               |
| partnerBillableAccountId | ciąg                                                         | Pobiera lub ustawia identyfikator konta do rozliczenia przez partnera.                         |
| partnerId                | ciąg                                                         | Pobiera lub ustawia identyfikator dzierżawy usługi Azure Active Directory partnera.            |
| partnerName              | ciąg                                                         | Pobiera lub ustawia nazwę partnera.                                      |
| postTaxEffectiveRate     | liczba                                                         | Pobiera lub ustawia obowiązującą cenę za podatki.                         |
| postTaxTotal             | liczba                                                         | Pobiera lub ustawia łączną opłatę za podatek. Opłaty za Pretaxy + kwota podatku |
| preTaxCharges            | liczba                                                         | Pobiera lub ustawia cenę naliczaną przed opodatkowaniem.                          |
| preTaxEffectiveRate      | liczba                                                         | Pobiera lub ustawia obowiązującą cenę przed opodatkowaniem.                        |
| region                   | ciąg                                                         | Pobiera lub ustawia region skojarzony z wystąpieniem zasobu.        |
| resourceGuid             | ciąg                                                         | Pobiera lub ustawia identyfikator zasobu.                                 |
| resourceName             | ciąg                                                         | Pobiera lub ustawia nazwę zasobu. Przykład: baza danych (GB/miesiąc).         |
| serviceName              | ciąg                                                         | Pobiera lub ustawia nazwę usługi. Przykład: Azure Data Service.           |
| Service              | ciąg                                                         | Pobiera lub ustawia typ usługi. Przykład: Azure SQL DB.           |
| sku                      | ciąg                                                         | Pobiera lub ustawia jednostkę SKU usługi.                                         |
| subscriptionDescription  | ciąg                                                         | Pobiera lub ustawia opis subskrypcji.                            |
| subscriptionId           | ciąg                                                         | Pobiera lub ustawia unikatowy identyfikator subskrypcji.                      |
| subscriptionName         | ciąg                                                         | Pobiera lub ustawia nazwę subskrypcji.                                   |
| taxAmount                | liczba                                                         | Pobiera lub ustawia kwotę naliczaną podatku.                               |
| tier2MpnId               | liczba                                                         | Pobiera lub ustawia identyfikator MPN partnera warstwy 2 skojarzonego z tym elementem wiersza. |
| unit                     | ciąg                                                         | Pobiera lub ustawia jednostkę miary dla użycia platformy Azure.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Reprezentuje operacje dostępne w instrukcji faktury w aplikacji/pliku PDF.

| Właściwość                 | Typ                                                           | Opis                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent z atrybutem ContentType = Application/PDF.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Przedstawia element wiersza rozliczenia faktury dla subskrypcji opartych na licencji.

| Właściwość | Typ | Opis |
| --- | --- | --- |
| PartnerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy partnera. |
| CustomerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy klienta. |
| CustomerName | ciąg | Pobiera lub ustawia nazwę klienta. |
| CustomerDomainName | ciąg | Pobiera lub ustawia nazwę domeny klienta. |
| CustomerCountry | ciąg | Pobiera lub ustawia kraj klienta. |
| InvoiceNumber | ciąg | Pobiera lub ustawia numer faktury. |
| MpnId | ciąg | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. |
| ResellerMpnId | int | Pobiera lub ustawia unikatowy identyfikator kolejności. |
| OrderDate (Data zamówienia) | DateTime | Pobiera lub ustawia datę utworzenia zamówienia. |
| ProductId | ciąg | Pobiera lub ustawia unikatowy identyfikator produktu. |
| Identyfikatora skuId | ciąg | Pobiera lub ustawia unikatowy identyfikator jednostki SKU. |
| AvailabilityId | ciąg | Pobiera lub ustawia unikatowy identyfikator dostępności. |
| ProductName | ciąg | Pobiera lub ustawia nazwę produktu. |
| SkuName | ciąg | Pobiera lub ustawia nazwę jednostki SKU. |
| ChargeType | ciąg | Pobiera lub ustawia typ opłaty. |
| UnitPrice | decimal | Pobiera lub ustawia cenę jednostkową. |
| EffectiveUnitPrice | decimal | Pobiera lub ustawia obowiązującą cenę jednostkową. |
| UnitType | ciąg | Pobiera lub ustawia typ jednostki. |
| Liczba | int | Pobiera lub ustawia liczbę jednostek skojarzonych z tym elementem wiersza. |
| Suma częściowa | decimal | Pobiera lub ustawia kwotę po rabacie. |
| TaxTotal | decimal | Pobiera lub ustawia opłaty za podatki. |
| TotalForCustomer | decimal | Pobiera lub ustawia łączną kwotę po rabacie i podatku. |
| Waluta | ciąg | Pobiera lub ustawia walutę używaną dla tego elementu wiersza. |
| PublisherName | ciąg | Pobiera lub ustawia nazwę wydawcy skojarzoną z tym zakupem. |
| PublisherId | ciąg | Pobiera lub ustawia identyfikator wydawcy skojarzony z tym zakupem. |
| SubscriptionDescription | ciąg | Pobiera lub ustawia opis subskrypcji skojarzony z tym zakupem. |
| SubscriptionId | ciąg | Pobiera lub ustawia identyfikator subskrypcji skojarzony z tym zakupem. |
| ChargeStartDate | DateTime | Pobiera lub ustawia datę rozpoczęcia opłaty skojarzonej z tym zakupem. |
| ChargeEndDate | DateTime | Pobiera lub ustawia datę końcową opłaty skojarzonej z tym zakupem. |
| TermAndBillingCycle | ciąg | Pobiera lub ustawia cykl rozliczeniowy związany z tym zakupem. |
| AlternateId | ciąg | Pobiera lub ustawia alternatywny identyfikator (identyfikator cudzysłowu). |
| PriceAdjustmentDescription | ciąg | Pobiera lub ustawia opis korekty ceny. |
| CreditReasonCode | ciąg | Pobiera lub ustawia kod przyczyny kredytu. |
| DiscountDetails | ciąg |  **Przestarzałe**. Pobiera lub ustawia szczegóły rabatu skojarzone z tym zakupem. |
| PricingCurrency | ciąg | Pobiera lub ustawia kod waluty cenowej. |
| PCToBCExchangeRate | decimal | Pobiera lub ustawia walutę cenową dla kursu wymiany waluty rozliczeniowej. |
| PCToBCExchangeRateDate | DateTime | Pobiera lub ustawia datę kursu wymiany, w którym określono walutę cenową dla kursu wymiany waluty rozliczeniowej. |
| BillableQuantity | decimal | Pobiera lub ustawia liczbę zakupionych jednostek. Dla każdej kolumny projektu o nazwie **BillableQuantity**. |
| MeterDescription | ciąg | Pobiera lub ustawia opis licznika dla elementu wiersza użycia. |
| ReservationOrderId | ciąg | Pobiera lub ustawia identyfikator zamówienia rezerwacji dla zakupu na platformie Azure. |
| BillingFrequency | ciąg | Pobiera lub ustawia częstotliwość rozliczeń. |
| InvoiceLineItemType | InvoiceLineItemType | Zwraca typ elementu wiersza faktury. |
| BillingProvider | BillingProvider | Zwraca dostawcę rozliczeń. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Reprezentuje pozycje rozliczane, rozliczane z rozliczeniami za codzienne użycie.

| Właściwość | Typ | Opis |
| --- | --- | --- |
| PartnerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy partnera. |
| PartnerName | ciąg | Pobiera lub ustawia nazwę partnera. |
| CustomerId | ciąg | Pobiera lub ustawia identyfikator dzierżawy klienta, do którego należy użycie. |
| CustomerName | ciąg | Pobiera lub ustawia nazwę firmy klienta, do której należy użycie. |
| CustomerDomainName | ciąg | Pobiera lub ustawia nazwę domeny klienta, do którego należy użycie. |
| InvoiceNumber | ciąg | Pobiera lub ustawia identyfikator faktury, do której należy użycie. |
| ProductId | ciąg | Pobiera lub ustawia unikatowy identyfikator produktu. |
| Identyfikatora skuId | ciąg | Pobiera lub ustawia unikatowy identyfikator jednostki SKU. |
| AvailabilityId | ciąg | Pobiera lub ustawia unikatowy identyfikator dostępności. |
| SkuName | ciąg | Pobiera lub ustawia nazwę jednostki SKU dla usługi. |
| ProductName | ciąg | Pobiera lub ustawia nazwę produktu. |
| PublisherName | ciąg | Pobiera lub ustawia nazwę wydawcy. |
| PublisherId | ciąg | Pobiera lub ustawia identyfikator wydawcy. |
| SubscriptionId | ciąg | Pobiera lub ustawia identyfikator subskrypcji. |
| SubscriptionDescription | ciąg | Pobiera lub ustawia opis subskrypcji. |
| ChargeStartDate | DateTime | Pobiera lub ustawia datę rozpoczęcia opłaty. |
| ChargeEndDate | DateTime | Pobiera lub ustawia datę zakończenia opłaty. |
| UsageDate | DateTime | Pobiera lub ustawia datę użycia. |
| Licznik mierników | ciąg | Pobiera lub ustawia typ miernika. |
| MeterCategory | ciąg | Pobiera lub ustawia kategorię miernika. |
| MeterId | ciąg | Pobiera lub ustawia identyfikator licznika (GUID). |
| MeterSubCategory | ciąg | Pobiera lub ustawia podkategorię miernika. |
| MeterName | ciąg | Pobiera lub ustawia nazwę miernika. |
| MeterRegion | ciąg | Pobiera lub ustawia region miernika. |
| UnitOfMeasure | ciąg | Pobiera lub ustawia jednostkę miary. |
| ResourceLocation | ciąg | Pobiera lub ustawia lokalizację zasobu. |
| ConsumedService | ciąg | Pobiera lub ustawia nazwę używanej usługi. |
| ResourceGroup | ciąg | Pobiera lub ustawia nazwę grupy zasobów. |
| ResourceUri | ciąg | Pobiera lub ustawia identyfikator URI wystąpienia zasobu, którego dotyczy użycie. |
| Tagi | ciąg | Pobiera lub ustawia Tagi dodane przez klienta. |
| AdditionalInfo | ciąg | Pobiera lub ustawia metadane dotyczące usługi. Na przykład typ obrazu dla maszyny wirtualnej. |
| ServiceInfo1 | ciąg | Pobiera lub ustawia wewnętrzne metadane usługi platformy Azure. |
| ServiceInfo2 | ciąg | Pobiera lub ustawia informacje o usłudze na przykład typ obrazu dla maszyny wirtualnej i nazwy usługodawcy internetowego dla ExpressRoute. |
| CustomerCountry | ciąg | Pobiera lub ustawia kraj klienta. |
| MpnId | ciąg | Pobiera lub ustawia identyfikator MPN skojarzony z tym elementem wiersza. |
| ResellerMpnId | ciąg | Pobiera lub ustawia identyfikator MPN odsprzedawcy w ramach partnera warstwy 2 skojarzonego z tym elementem wiersza. |
| ChargeType | ciąg | Pobiera lub ustawia typ opłaty. |
| UnitPrice | decimal | Pobiera lub ustawia cenę jednostki. |
| Liczba | decimal | Pobiera lub ustawia ilość użycia. |
| UnitType | ciąg | Pobiera lub ustawia typ jednostki (na przykład 1 godzina). |
| BillingPreTaxTotal | decimal | Pobiera lub ustawia koszt rozszerzony lub łączny koszt przed opodatkowaniem w walucie lokalnej klienta lub waluty rozliczeniowej. |
| BillingCurrency | ciąg | Pobiera lub ustawia walutę ISO, w której licznik jest naliczany w walucie lokalnej klienta lub waluty rozliczeniowej. |
| PricingPreTaxTotal | decimal | Pobiera lub ustawia koszt rozszerzony lub łączny koszt przed podatkiem w walucie USD lub walutą katalogu używaną do oceny. |
| PricingCurrency | ciąg | Pobiera lub ustawia walutę ISO, w której jest naliczana opłata za licznik USD lub walutę katalogu używaną do oceny. |
| EntitlementId | ciąg | Pobiera lub ustawia identyfikator uprawnienia (subskrypcja platformy Azure). |
| EntitlementDescription | ciąg | Pobiera lub ustawia opis uprawnienia (subskrypcja platformy Azure). |
| PCToBCExchangeRate | ciąg | Pobiera lub ustawia walutę cenową dla kursu wymiany waluty rozliczeniowej. |
| PCToBCExchangeRateDate | DateTime | Pobiera lub ustawia walutę cenową dla daty kursu wymiany waluty rozliczeniowej. |
| EffectiveUnitPrice | decimal | Pobiera lub ustawia obowiązującą cenę jednostkową. |
| RateOfPartnerEarnedCredit | decimal | Pobiera lub ustawia stawkę odsetek uzyskanych przez partnera. |
| HasPartnerEarnedCredit | bool | Pobiera lub ustawia środki dla partnerów. |
| RateOfCredit | decimal | Pobiera lub ustawia stawkę kredytu dla danego typu kredytu. |
| Kredyttype | ciąg | Pobiera lub ustawia typ kredytu. |
| InvoiceLineItemType | InvoiceLineItemType | Zwraca typ elementu wiersza faktury. |
| BillingProvider | BillingProvider | Zwraca dostawcę rozliczeń. |
