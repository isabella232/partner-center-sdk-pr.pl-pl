---
title: Zasoby kosztów usług
description: Opisuje zasoby związane z usługami zakupionymi przez klienta.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbddc1973dd9a904cedd549c1772cd4c74c69a60
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547414"
---
# <a name="service-costs-resources"></a>Zasoby kosztów usług

Opisuje zasoby związane z usługami zakupionymi przez klienta.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** zawiera podsumowanie, które agreguje wszystkie usługi zakupione przez określonego klienta w okresie rozliczeniowym.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| Szczegóły | tablica [obiektów ServiceCostsSummaryDetail](#servicecostssummarydetail) | Lista szczegółów podsumowania kosztów usługi z rozróżnieniem według typu faktury.|
| Linki | [ResourceLinks](utility-resources.md#resourcelinks) | Link do zasobu. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |

> [!IMPORTANT]
> **Pola w poniższej tabeli są przestarzałe.** Aby pobrać cykliczne i jednorazowych podsumowań kosztów usługi, zamiast tego użyj **pola** szczegółów. Pole **szczegółów** jest opisane w poprzedniej tabeli. Zapoznaj się z **odpowiednimi** wartościami danych pola szczegółów, ale nie polami na poziomie głównym.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| billingStartDate | data | Początek okresu rozliczeniowego. |
| billingEndDate | data | Koniec okresu rozliczeniowego. |
| pretaxTotal | double | Suma wszystkich kosztów dla klienta przed opodatkowaniem. |
| Podatku  | double | Łączny podatek od wszystkich elementów zakupionych przez klienta. |
| afterTaxTotal | double | Łączny koszt netto wszystkich elementów zakupionych przez klienta. |
| currencyCode | ciąg | Reprezentuje walutę używaną dla kosztów. |
| currencySymbol | ciąg | Symbol waluty używany na kosztach. |
| customerId | ciąg | Identyfikator klienta dokonującego zakupu. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**Temat ServiceCostsSummaryDetail** zawiera podsumowanie kosztów usługi, które agreguje wszystkie usługi zakupione przez określonego klienta w okresie rozliczeniowym (na podstawie faktur cyklicznych lub jednorazowych).

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| invoiceType | ciąg | InvoiceType, że zostało wygenerowane podsumowanie kosztów usługi. |
| Podsumowanie | [ServiceCostsSummary](#servicecostssummary) | Podsumowanie kosztów usług zagregowane według klienta w ramach jednego typu faktury. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**Temat ServiceCostLineItem opisuje** pojedynczy element zakupiony przez klienta.

> [!IMPORTANT]
> Następujące właściwości  dotyczą tylko elementów wiersza kosztu usługi, w przypadku których produkt jest zakupem tylko *raz:* **productId,** **productName,** **skuId,** **skuName,** **availabilityId,** **publisherId,** **publisherName,** **termAndBillingCycle,** **discountDetails.** Te właściwości *nie dotyczą pozycji* usług, w przypadku których produkt jest *cyklicznym zakupem.* Na przykład te właściwości *nie dotyczą subskrypcji* opartych Office 365 platformie Azure.

| Właściwość                 | Typ                           | Opis                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| Startdate                | ciąg w formacie daty i godzin UTC | Data rozpoczęcia opłaty.                                       |
| Enddate                  | ciąg w formacie daty i godzin UTC | Data zakończenia opłaty.                                         |
| subscriptionFriendlyName | ciąg                         | Przyjazna nazwa subskrypcji.                              |
| subscriptionId           | ciąg                         | Identyfikator subskrypcji.                                         |
| Idzamówienia                  | ciąg                         | Identyfikator zamówienia.                                                |
| offerId                  | ciąg                         | Identyfikator oferty.                                                |
| nazwa_oferty                | ciąg                         | Nazwa oferty.                                                      |
| resellerMPNId            | ciąg                         | Używany tylko w scenariuszach z partnerami dwuwarstwowych. Odwołuje się do identyfikatora MPN. |
| chargeType               | ciąg                         | Skojarzony typ opłaty.                                          |
| quantity                 | liczba                         | Ilość jednostek używanych lub zakupionych.                             |
| unitPrice                | liczba                         | Cena za jednostkę.                                                  |
| pretaxTotal              | liczba                         | Łączna opłata za tę pozycję przed podatkami.                         |
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
| Własny                 | [Link](utility-resources.md#link) | Samodzielnego URI.                       |
