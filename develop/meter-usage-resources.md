---
title: Zasób rekordu użycia zliczania
description: Zasobu MeterUsageRecord można użyć do opisania szacowanego kosztu pieniężnego użycia poziomu miernika subskrypcji w bieżącym cyklu rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbc8d1bd2cd3f9a9c1a657d88f3fe4899676e9df
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274652"
---
# <a name="meter-usage-record-resource"></a>Zasób rekordu użycia zliczania

**Dotyczy:**

- Centrum partnerskie

Zasobu **MeterUsageRecord** można użyć do opisania szacowanego kosztu pieniężnego użycia poziomu miernika subskrypcji w bieżącym cyklu rozliczeniowym.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Właściwość         | Typ               | Opis                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId   | ciąg             | Identyfikator GUID odpowiadający identyfikatorowi [zasobu subskrypcji](subscription-resources.md#subscription)Centrum partnerskiego, który reprezentuje subskrypcję Microsoft Azure (MS-AZR-0145P) lub plan platformy Azure. W przypadku subskrypcji Microsoft Azure (MS-AZR-0145P), ta wartość jest identyfikatorem subskrypcji commerce. W przypadku zasobów subskrypcji planu platformy Azure ta wartość jest identyfikatorem planu platformy Azure. |
| MeterId          | ciąg             | Pobiera lub ustawia identyfikator licznika.                                                                                                                                                                                                                                                                                                                                                                  |
| MeterName        | ciąg             | Pobiera lub ustawia nazwę miernika.                                                                                                                                                                                                                                                                                                                                                                        |
| Kategoria         | ciąg             | Pobiera lub ustawia kategorię zasobów platformy Azure.                                                                                                                                                                                                                                                                                                                                                           |
| Subcategory (Podkategoria)      | ciąg             | Pobiera lub ustawia podrzędną podkategorię zasobów platformy Azure.                                                                                                                                                                                                                                                                                                                                                       |
| QuantityUsed     | decimal            | Pobiera lub ustawia liczbę używanych zasobów platformy Azure.                                                                                                                                                                                                                                                                                                                                               |
| Jednostka             | ciąg             | Pobiera lub ustawia jednostkę miary dla zasobu platformy Azure.                                                                                                                                                                                                                                                                                                                                            |
| TotalCost        | decimal            | Pobiera lub ustawia Szacowany łączny koszt użycia.                                                                                                                                                                                                                                                                                                                                                     |
| CurrencyLocale   | ciąg             | Ustawienia regionalne, w których była używana subskrypcja. Ta właściwość określa walutę używaną na fakturze. Ta właściwość jest dostępna dla subskrypcji Microsoft Azure (MS-AZR-0145P).                                                                                                                                                                                                      |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Ta właściwość jest dostępna dla planów platformy Azure.                                                                                                                                                                                                                                                                                                                         |
| USDTotalCost     | decimal            | Pobiera lub ustawia Szacowany łączny koszt w USD. Ta właściwość jest dostępna dla planów platformy Azure.                                                                                                                                                                                                                                                                                                           |
| LastModifiedDate | ciąg             | Dzień (w formacie daty i godziny), w którym ten rekord został ostatnio zmodyfikowany.                                                                                                                                                                                                                                                                                                                                   |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                                                                                                                                                                                                                                                                                                                              |
