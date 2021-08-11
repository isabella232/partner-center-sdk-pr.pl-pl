---
title: Zasoby kosztów usług
description: Opisuje zasoby związane z usługami zakupionymi przez klienta.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c1e3a05be89eee12d708a3a37e008ec7fa42358eaec7e1f020aaa47e44b452c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996142"
---
# <a name="service-costs-resources"></a>Zasoby kosztów usług

Opisuje zasoby związane z usługami zakupionymi przez klienta.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** zawiera podsumowanie, które agreguje wszystkie usługi zakupione przez określonego klienta w okresie rozliczeniowym.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| Szczegóły | tablica [obiektów ServiceCostsSummaryDetail](#servicecostssummarydetail) | Lista szczegółów podsumowania kosztów usług z rozróżnianą według typu faktury.|
| Linki | [ResourceLinks](utility-resources.md#resourcelinks) | Link do zasobu. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |

> [!IMPORTANT]
> **Pola w poniższej tabeli są przestarzałe.** Aby pobrać cykliczne i jednorazowych podsumowań kosztów usługi, zamiast tego **użyj pola** szczegółów. Pole **szczegółów** jest opisane w poprzedniej tabeli. Zapoznaj się z **odpowiednimi** wartościami danych pola szczegółów, ale nie polami na poziomie głównym.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| billingStartDate | data | Początek okresu rozliczeniowego. |
| billingEndDate | data | Koniec okresu rozliczeniowego. |
| pretaxTotal | double | Suma przed opodatkowaniem wszystkich kosztów dla klienta. |
| Podatku  | double | Łączny podatek od wszystkich pozycji zakupionych przez klienta. |
| afterTaxTotal | double | Łączny koszt netto wszystkich elementów zakupionych przez klienta. |
| currencyCode | ciąg | Reprezentuje walutę używaną dla kosztów. |
| currencySymbol | ciąg | Symbol waluty używany na kosztach. |
| customerId | ciąg | Identyfikator klienta dokonującego zakupu. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**Temat ServiceCostsSummaryDetail** opisuje podsumowanie kosztów usługi, które agreguje wszystkie usługi zakupione przez określonego klienta w okresie rozliczeniowym (z faktur cyklicznych lub jednorazowych).

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| invoiceType (typ faktury) | ciąg | InvoiceType, który został wygenerowany w podsumowaniu kosztów usługi. |
| Podsumowanie | [ServiceCostsSummary](#servicecostssummary) | Podsumowanie kosztów usług zagregowane według klienta w ramach jednego typu faktury. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**Element ServiceCostLineItem** opisuje pojedynczy element zakupiony przez klienta.

> [!IMPORTANT]
> Następujące właściwości  dotyczą tylko elementów wiersza kosztu usługi, w przypadku których produkt jest zakupem tylko *raz:* **productId,** **productName,** **skuId,** **skuName,** **availabilityId,** **publisherId,** **publisherName,** **termAndBillingCycle,** **discountDetails.** Te właściwości *nie dotyczą pozycji usług,* w przypadku których produkt jest *cyklicznym zakupem.* Na przykład te właściwości *nie mają zastosowania do zasobów* opartych na Office 365 i platformy Azure.

| Właściwość                 | Typ                           | Opis                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| Startdate                | ciąg w formacie daty i czasu UTC | Data rozpoczęcia opłaty.                                       |
| Enddate                  | ciąg w formacie daty i czasu UTC | Data zakończenia opłaty.                                         |
| subscriptionFriendlyName | ciąg                         | Przyjazna nazwa subskrypcji.                              |
| subscriptionId           | ciąg                         | Identyfikator subskrypcji.                                         |
| Idzamówienia                  | ciąg                         | Identyfikator zamówienia.                                                |
| offerId                  | ciąg                         | Identyfikator oferty.                                                |
| offerName (nazwa oferty)                | ciąg                         | Nazwa oferty.                                                      |
| resellerMPNId            | ciąg                         | Używana tylko w scenariuszach z partnerami dwuwarstwowych. Odwołuje się do identyfikatora MPN. |
| chargeType               | ciąg                         | Skojarzony typ opłaty.                                          |
| quantity                 | liczba                         | Ilość użytych lub zakupionych jednostek.                             |
| unitPrice                | liczba                         | Cena za jednostkę.                                                  |
| pretaxTotal              | liczba                         | Łączna opłata za tę pozycję przed opodatkowaniem.                         |
| Podatku                      | liczba                         | Łączna opłata podatku naliczana dla tego elementu.                         |
| afterTaxTotal            | liczba                         | Łączny koszt netto dla tego elementu.                                    |
| currencyCode             | ciąg                         | Reprezentuje walutę używaną dla kosztów.                          |
| currencySymbol           | ciąg                         | Symbol waluty używany na kosztach.                              |
| customerId               | ciąg                         | Identyfikator klienta dokonującego zakupu.                          |
| Customername             | ciąg                         | Nazwa klienta dokonującego zakupu.                        |
| invoiceNumber            | ciąg                         | Numer faktury, do której należy ten element wiersza.                   |
| productId                | ciąg                         | Identyfikator produktu.                                              |
| skuId                    | ciąg                         | Identyfikator jednostki SKU.                                                  |
| availabilityId           | ciąg                         | Identyfikator dostępności.                                         |
| Productname              | ciąg                         | Nazwa produktu.                                                    |
| skuName                  | ciąg                         | Nazwa sku.                                                        |
| publisherName            | ciąg                         | Nazwa wydawcy.                                                  |
| publisherId              | ciąg                         | Identyfikator wydawcy.                                            |
| termAndBillingCycle      | ciąg                         | Okres i cykl rozliczeniowy.                                          |
| discountDetails          | ciąg                         | Szczegóły rabatu.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Właściwość             | Typ                               | Opis                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Link](utility-resources.md#link) | URI do pobierania elementów wiersza. |
| Własny                 | [Link](utility-resources.md#link) | Własny URI.                       |
