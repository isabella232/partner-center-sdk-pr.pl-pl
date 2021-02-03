---
title: Zasoby kosztów usługi
description: Opisuje zasoby związane z usługami zakupionymi przez klienta.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0236329d93d8ddc9019a15fb67a81a3af3e7620
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768006"
---
# <a name="service-costs-resources"></a>Zasoby kosztów usługi

**Dotyczy:**

- Centrum partnerskie

Opisuje zasoby związane z usługami zakupionymi przez klienta.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** zawiera podsumowanie, które agreguje wszystkie usługi zakupione przez określonego klienta w okresie rozliczeniowym.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| uzyskać | Tablica obiektów [ServiceCostsSummaryDetail](#servicecostssummarydetail) | Lista szczegółów podsumowania kosztu usługi, wyodrębniona według typu faktury.|
| linki | [ResourceLinks](utility-resources.md#resourcelinks) | Linki do zasobów. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |

> [!IMPORTANT]
> **Pola w poniższej tabeli są przestarzałe.** Aby pobrać podsumowanie kosztów usługi cyklicznej i jednorazowej, użyj pola **szczegóły** . Pole **szczegóły** jest opisane w poprzedniej tabeli. Zapoznaj się z odpowiednimi wartościami danych pola **szczegóły** , ale nie pól na poziomie głównym.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| billingStartDate | date | Początek okresu rozliczeniowego. |
| billingEndDate | date | Koniec okresu rozliczeniowego. |
| pretaxTotal | double | Suma przed opodatkowaniem wszystkich kosztów dla klienta. |
| podatkowych  | double | Łączny podatek związany ze wszystkimi elementami zakupionymi przez klienta. |
| afterTaxTotal | double | Łączny koszt netto wszystkich elementów zakupionych przez klienta. |
| currencyCode | ciąg | Reprezentuje walutę używaną w kosztach. |
| currencySymbol | ciąg | Symbol waluty używany do kosztów. |
| customerId | ciąg | Identyfikator klienta dokonującego zakupu. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** opisuje podsumowanie kosztu usługi, które agreguje wszystkie usługi zakupione przez określonego klienta w okresie rozliczeniowym (od cyklicznych lub jednorazowych faktur).

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| invoicetype | ciąg | Wartość invoicetype, która wygenerowała podsumowanie kosztów usług. |
| Podsumowanie | [ServiceCostsSummary](#servicecostssummary) | Podsumowanie kosztów usługi agregowane przez klienta w ramach jednego typu faktury. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** opisuje pojedynczy element zakupiony przez klienta.

> [!IMPORTANT]
> Następujące właściwości *dotyczą tylko* elementów wiersza kosztu usługi, w których produkt jest *jednorazowym zakupem*: **ProductID**, **ProductName**, **identyfikatora skuId**, **skuName**, **availabilityId**, **publisherId**, **PublisherName**, **termAndBillingCycle**, **discountDetails**. Te właściwości *nie dotyczą* elementów wiersza usługi, w przypadku których produkt jest *cyklicznym zakupem*. Na przykład te właściwości *nie mają zastosowania* do pakietu Office 365 i platformy Azure opartego na subskrypcjach.

| Właściwość                 | Typ                           | Opis                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | ciąg w formacie daty i godziny UTC | Data rozpoczęcia opłaty.                                       |
| endDate                  | ciąg w formacie daty i godziny UTC | Data końcowa opłaty.                                         |
| subscriptionFriendlyName | ciąg                         | Przyjazna nazwa subskrypcji.                              |
| subscriptionId           | ciąg                         | Identyfikator subskrypcji.                                         |
| Wartooć                  | ciąg                         | Identyfikator zamówienia.                                                |
| offerId                  | ciąg                         | Identyfikator oferty.                                                |
| offerName                | ciąg                         | Nazwa oferty.                                                      |
| resellerMPNId            | ciąg                         | Używane tylko w scenariuszach partnerskich dwóch warstw. Odwołuje się do identyfikatora MPN. |
| chargeType               | ciąg                         | Typ opłaty skojarzonej.                                          |
| quantity                 | liczba                         | Ilość używanych lub zakupionych jednostek.                             |
| unitPrice                | liczba                         | Cena za jednostkę.                                                  |
| pretaxTotal              | liczba                         | Łączna opłata za ten element przed opodatkowaniem.                         |
| podatkowych                      | liczba                         | Łączna opłata za podatek dla tego elementu.                         |
| afterTaxTotal            | liczba                         | Łączny koszt dla tego elementu netto.                                    |
| currencyCode             | ciąg                         | Reprezentuje walutę używaną w kosztach.                          |
| currencySymbol           | ciąg                         | Symbol waluty używany do kosztów.                              |
| customerId               | ciąg                         | Identyfikator klienta dokonującego zakupu.                          |
| customerName             | ciąg                         | Nazwa klienta dokonującego zakupu.                        |
| invoiceNumber            | ciąg                         | Numer faktury, do której należy ten element wiersza.                   |
| productId                | ciąg                         | Identyfikator produktu.                                              |
| Identyfikatora skuId                    | ciąg                         | Identyfikator jednostki SKU.                                                  |
| availabilityId           | ciąg                         | Identyfikator dostępności.                                         |
| productName              | ciąg                         | Nazwa produktu.                                                    |
| skuName                  | ciąg                         | Nazwa jednostki SKU.                                                        |
| publisherName            | ciąg                         | Nazwa wydawcy.                                                  |
| publisherId              | ciąg                         | Identyfikator wydawcy.                                            |
| termAndBillingCycle      | ciąg                         | Okres i cykl rozliczeniowy.                                          |
| discountDetails          | ciąg                         | Szczegóły rabatu.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Właściwość             | Typ                               | Opis                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Łącze](utility-resources.md#link) | Identyfikator URI do pobrania elementów wiersza. |
| automatycznej                 | [Łącze](utility-resources.md#link) | Własny identyfikator URI.                       |
