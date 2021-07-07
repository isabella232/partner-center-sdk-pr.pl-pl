---
title: Zasoby użycia subskrypcji
description: Zasoby użycia subskrypcji opisują subskrypcje z rozliczeniami opartymi na użyciu. Te subskrypcje mają dzienne i miesięczne rekordy użycia wraz z podsumowaniem użycia dla każdego okresu płatności.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcb24dcf5ca8165ec23c4b187def38d05772e1de
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547380"
---
# <a name="subscription-usage-resources"></a>Zasoby użycia subskrypcji

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Możesz użyć następujących zasobów użycia subskrypcji, aby uzyskać informacje o użyciu dla określonej subskrypcji z rozliczeniami opartymi na użyciu. Te subskrypcje mają dzienne i miesięczne rekordy użycia wraz z podsumowaniem użycia dla każdego okresu płatności.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*Zasób **SubscriptionDailyUsageRecord** jest przestarzały i może dawać niedokładne wyniki. Zalecamy zaktualizowanie aplikacji w celu używania interfejsów API opisanych w tematach [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md) (Uzyskiwanie rekordów wykorzystania platformy Azure przez klienta) i Get prices for [Microsoft Azure](get-prices-for-microsoft-azure.md) instead (Uzyskiwanie cen dla maszyn wirtualnych).*

Zasób **SubscriptionDailyUsageRecord** opisuje, ile subskrypcji jest używanych w ciągu jednego dnia.

| Właściwość         | Typ               | Opis                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | ciąg             | Dzień, w formacie data/godzina, w przypadku których została użyta subskrypcja.                                 |
| ResourceId       | ciąg             | Identyfikator guid. Unikatowy identyfikator zasobu.                                                          |
| ResourceName     | ciąg             | Nazwa zasobu.                                                                     |
| Łączny koszt        | decimal             | Szacowany łączny koszt używania zasobów w subskrypcji w określonym dniu.     |
| CurrencyLocale   | ciąg             | Lokalne wartości, w których została użyta subskrypcja, określają walutę do użycia na fakturze. |
| LastModifiedDate | ciąg             | Dzień, w formacie data/godzina, ostatniej modyfikacji tego rekordu.                             |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

Zasób **SubscriptionMonthlyUsageRecord opisuje,** ile subskrypcji jest używanych w ciągu jednego miesiąca.

| Właściwość         | Typ               | Opis                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Stan           | ciąg             | Stan subskrypcji: "brak", "aktywny", "wstrzymany" lub "usunięty".                  |
| Rekord PartnerOnRecord  | ciąg             | "Identyfikator MPN zarejestrowanego partnera".                                                        |
| OfferId          | ciąg             | Identyfikator guid. Identyfikator oferty powiązanej z tą subskrypcją.                                       |
| Id               | ciąg             | Identyfikator guid. Identyfikator subskrypcji lub zasobu.                                                 |
| Nazwa             | ciąg             | Nazwa subskrypcji lub zasobu.                                                     |
| Łączny koszt        | decimal             | Szacowany całkowity koszt używania zasobów w subskrypcji w określonym miesiącu.   |
| CurrencyLocale   | ciąg             | Lokalne wartości, w których została użyta subskrypcja, określają walutę do użycia na fakturze. Dostępne Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P). |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| USDTotalCost     | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla planów platformy Azure.                                         |
| LastModifiedDate | ciąg             | Dzień, w formacie data/godzina, ostatniej modyfikacji tego rekordu.                             |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

Zasób **SubscriptionUsageSummary** opisuje, ile określonej subskrypcji zostało użyte w bieżącym okresie rozliczeniowym.

| Właściwość         | Typ               | Opis                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | ciąg             | Identyfikator guid. Identyfikator subskrypcji lub zasobu. W kontekście rekordu CustomerMonthlyUsageRecord ten identyfikator jest identyfikatorem klienta. |
| ResourceName     | ciąg             | Nazwa subskrypcji lub zasobu. W kontekście rekordu CustomerMonthlyUsageRecord ta nazwa jest nazwą klienta. |
| BillingStartDate | data               | Data rozpoczęcia bieżącego okresu rozliczeniowego w formacie data/godzina.                                                     |
| BillingEndDate   | data               | Data zakończenia bieżącego okresu rozliczeniowego w formacie data/godzina.                                                       |
| Łączny koszt        | double             | Szacowany całkowity koszt używania zasobów w ramach subskrypcji w określonym okresie rozliczeniowym.               |
| CurrencyLocale   | ciąg             | Lokalne wartości, w których została użyta subskrypcja, określają walutę do użycia na fakturze. Dostępne Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P). |
| CurrencyCode   | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.                                         |
| USDTotalCost   | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| LastModifiedDate | ciąg             | Dzień, w formacie data/godzina, ostatniej modyfikacji tego rekordu.                                                      |
| Linki            | ResourceLinks      | Linki zasobów odpowiadające subskrypcji SubscriptionUsageSummary.                                                      |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające subscriptionUsageSummary.                                                 |
