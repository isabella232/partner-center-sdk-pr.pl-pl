---
title: Zasoby użycia subskrypcji
description: Zasoby użycia subskrypcji opisują subskrypcje dotyczące rozliczeń opartych na użyciu. Te subskrypcje mają dzienne i miesięczne rekordy użycia wraz z podsumowaniem użycia dla każdego okresu rozliczeniowego.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8e23287d80f19084860f4597754448e81c01049f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767837"
---
# <a name="subscription-usage-resources"></a>Zasoby użycia subskrypcji

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Poniższe zasoby użycia subskrypcji umożliwiają uzyskanie informacji o użyciu określonej subskrypcji za pomocą rozliczeń opartych na użyciu. Te subskrypcje mają dzienne i miesięczne rekordy użycia wraz z podsumowaniem użycia dla każdego okresu rozliczeniowego.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*Zasób **SubscriptionDailyUsageRecord** jest przestarzały i może generować niedokładne wyniki. Zalecamy zaktualizowanie aplikacji w taki sposób, aby korzystały z interfejsów API opisanych w artykule [pobieranie rekordów użycia klienta na platformie Azure](get-a-customer-s-utilization-record-for-azure.md) i [Uzyskiwanie cen dla Microsoft Azure](get-prices-for-microsoft-azure.md) .*

Zasób **SubscriptionDailyUsageRecord** opisuje, jak dużo subskrypcja jest używana w jednym dniu.

| Właściwość         | Typ               | Opis                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | ciąg             | Dzień w formacie daty i godziny, że subskrypcja została użyta.                                 |
| ResourceId       | ciąg             | Ident. Unikatowy identyfikator zasobu.                                                          |
| ResourceName     | ciąg             | Nazwa zasobu.                                                                     |
| TotalCost        | decimal             | Szacowany łączny koszt używania zasobów w subskrypcji w określonym dniu.     |
| CurrencyLocale   | ciąg             | Ustawienia regionalne, w których została użyta subskrypcja, określają walutę używaną na fakturze. |
| LastModifiedDate | ciąg             | Dzień w formacie daty i godziny, że ten rekord został ostatnio zmodyfikowany.                             |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

Zasób **SubscriptionMonthlyUsageRecord** opisuje, jak dużo subskrypcja jest używana w jednym miesiącu.

| Właściwość         | Typ               | Opis                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Stan           | ciąg             | Stan subskrypcji: "none", "Active", "SUSPENDED" lub "deleted".                  |
| PartnerOnRecord  | ciąg             | "Identyfikator MPN partnera w rekordzie".                                                        |
| OfferId          | ciąg             | Ident. Identyfikator oferty związanej z tą subskrypcją.                                       |
| Id               | ciąg             | Ident. Identyfikator subskrypcji lub zasobu.                                                 |
| Nazwa             | ciąg             | Nazwa subskrypcji lub zasobu.                                                     |
| TotalCost        | decimal             | Szacowany łączny koszt używania zasobów w subskrypcji w określonym miesiącu.   |
| CurrencyLocale   | ciąg             | Ustawienia regionalne, w których została użyta subskrypcja, określają walutę używaną na fakturze. Dostępne dla subskrypcji Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| USDTotalCost     | decimal             | Pobiera lub ustawia Szacowany łączny koszt w USD. Dostępne dla planów platformy Azure.                                         |
| LastModifiedDate | ciąg             | Dzień w formacie daty i godziny, że ten rekord został ostatnio zmodyfikowany.                             |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

Zasób **SubscriptionUsageSummary** opisuje, jak wiele określonej subskrypcji zostało użytych w bieżącym okresie rozliczeniowym.

| Właściwość         | Typ               | Opis                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | ciąg             | Ident. Identyfikator subskrypcji lub zasobu. W kontekście CustomerMonthlyUsageRecord tego identyfikatora jest identyfikator klienta. |
| ResourceName     | ciąg             | Nazwa subskrypcji lub zasobu. W kontekście CustomerMonthlyUsageRecord ta nazwa to nazwa klienta. |
| BillingStartDate | date               | Data rozpoczęcia bieżącego okresu rozliczeniowego w formacie daty i godziny.                                                     |
| BillingEndDate   | date               | Data końcowa bieżącego okresu rozliczeniowego w formacie daty i godziny.                                                       |
| TotalCost        | double             | Szacowany łączny koszt używania zasobów w subskrypcji w określonym okresie rozliczeniowym.               |
| CurrencyLocale   | ciąg             | Ustawienia regionalne, w których została użyta subskrypcja, określają walutę używaną na fakturze. Dostępne dla subskrypcji Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode   | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.                                         |
| USDTotalCost   | decimal             | Pobiera lub ustawia Szacowany łączny koszt w USD. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| LastModifiedDate | ciąg             | Dzień w formacie daty i godziny, że ten rekord został ostatnio zmodyfikowany.                                                      |
| Linki            | ResourceLinks      | Linki do zasobów odpowiadające SubscriptionUsageSummary.                                                      |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające SubscriptionUsageSummary.                                                 |
