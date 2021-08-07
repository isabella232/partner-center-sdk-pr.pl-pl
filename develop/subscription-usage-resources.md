---
title: Zasoby użycia subskrypcji
description: Zasoby użycia subskrypcji opisują subskrypcje z rozliczeniami opartymi na użyciu. Te subskrypcje mają dzienne i miesięczne rekordy użycia wraz z podsumowaniem użycia dla każdego okresu płatności.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8af4e9b8a4660b5bc9d287ece258dca9aa9ba7a749cfdc89e9c9b47e4af61b1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990277"
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
| CurrencyLocale   | ciąg             | Wartości regionalnych, w których została użyta subskrypcja, określają walutę do użycia na fakturze. |
| LastModifiedDate | ciąg             | Dzień w formacie daty i godziny ostatniej modyfikacji tego rekordu.                             |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

Zasób **SubscriptionMonthlyUsageRecord** opisuje, ile subskrypcji jest używanych w ciągu jednego miesiąca.

| Właściwość         | Typ               | Opis                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Stan           | ciąg             | Stan subskrypcji: "brak", "aktywny", "wstrzymany" lub "usunięty".                  |
| Rekord PartnerOnRecord  | ciąg             | "Identyfikator MPN zarejestrowanego partnera".                                                        |
| OfferId          | ciąg             | Identyfikator guid. Identyfikator oferty powiązanej z tą subskrypcją.                                       |
| Id               | ciąg             | Identyfikator guid. Identyfikator subskrypcji lub zasobu.                                                 |
| Nazwa             | ciąg             | Nazwa subskrypcji lub zasobu.                                                     |
| Łączny koszt        | decimal             | Szacowany całkowity koszt używania zasobów w subskrypcji w określonym miesiącu.   |
| CurrencyLocale   | ciąg             | Wartości regionalnych, w których została użyta subskrypcja, określają walutę do użycia na fakturze. Dostępne Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P). |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| USDTotalCost     | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla planów platformy Azure.                                         |
| LastModifiedDate | ciąg             | Dzień w formacie daty i godziny ostatniej modyfikacji tego rekordu.                             |
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
| CurrencyLocale   | ciąg             | Wartości regionalnych, w których została użyta subskrypcja, określają walutę do użycia na fakturze. Dostępne Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P). |
| CurrencyCode   | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.                                         |
| USDTotalCost   | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| LastModifiedDate | ciąg             | Dzień w formacie daty i godziny ostatniej modyfikacji tego rekordu.                                                      |
| Linki            | ResourceLinks      | Linki zasobów odpowiadające subskrypcji SubscriptionUsageSummary.                                                      |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające subscriptionUsageSummary.                                                 |
