---
title: Zasoby dotyczące użycia przez klientów
description: Zasoby dla klientów z subskrypcjami opartymi na użyciu i budżetami użycia miesięcznego (w tym CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary i SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eae516e2f759dfc2e8f80e946a835d70760c5c9e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973047"
---
# <a name="customer-usage-resources"></a>Zasoby dotyczące użycia przez klientów

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Klienci z subskrypcjami opartymi na użyciu mogą mieć miesięczny budżet użycia. Ten budżet określa limit maksymalnego użycia klienta i umożliwia partnerowi śledzenie użycia w czasie.

> [!NOTE]
> Numery użycia klientów to oszacowania (a nie wartości końcowe), których nie należy używać do celów rozliczeniowych.

## <a name="customermonthlyusagerecord"></a>Rekord CustomerMonthlyUsageRecord

**Rekord CustomerMonthlyUsageRecord** reprezentuje szacowany koszt pieniężny użycia klienta w bieżącym miesiącu.

| Właściwość         | Typ               | Opis                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budżet           | WydatkiBudget     | Budżet wydatków przydzielony dla klienta.                          |
| PercentUsed      | decimal             | Wartość procentowa wykorzystana z przydzielonego budżetu.                        |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu.                                   |
| ResourceName     | ciąg             | Nazwa zasobu.                                                |
| Łączny koszt        | decimal             | Szacowany całkowity koszt użycia zasobów w subskrypcji.|
| CurrencyLocale   | ciąg             | Waluty klienta. Dostępne dla Microsoft Azure subskrypcji (MS-AZR-0145P).            |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.           |
| USDTotalCost     | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla planów platformy Azure.                                         |
| IsUpgraded       | bool             | Pobiera lub ustawia wartość wskazującą, czy subskrypcja platformy Azure klienta jest uaktualniana. Wartość true **reprezentuje** klientów, którzy mają plan platformy Azure.                         |
| LastModifiedDate | data               | Data ostatniej modyfikacji danych użycia.                               |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające rekordowi użycia.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** reprezentuje podsumowanie użycia klienta w całym okresie rozliczeniowym.

| Właściwość         | Typ               | Opis                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budżet           | WydatkiBudget     | Budżet wydatków przydzielony dla klienta.                                                                  |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu. W kontekście rekordu CustomerMonthlyUsageRecord ten identyfikator jest identyfikatorem klienta. |
| ResourceName     | ciąg             | Nazwa zasobu. W kontekście rekordu CustomerMonthlyUsageRecord jest to nazwa klienta.               |
| BillingStartDate | data               | Data rozpoczęcia bieżącego okresu rozliczeniowego.                                                                    |
| BillingEndDate   | data               | Data zakończenia bieżącego okresu rozliczeniowego.                                                                      |
| Łączny koszt        | decimal             | Szacowany całkowity koszt użycia zasobów w subskrypcji.                                         |
| CurrencyLocale   | ciąg             | Waluty klienta. Dostępne dla Microsoft Azure subskrypcji (MS-AZR-0145P).                                         |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.                                         |
| USDTotalCost     | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| LastModifiedDate | data               | Data ostatniej modyfikacji danych użycia.                                                                       |
| Linki            | ResourceLinks      | Linki zasobów odpowiadające podsumowaniu użycia.                                                           |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające podsumowaniu użycia.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** reprezentuje podsumowanie budżetu użycia na poziomie partnera dla wszystkich klientów.

| Właściwość         | Typ               | Opis                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailToNotify   | tablica ciągów   | Lista adresów e-mail dla powiadomień.                                                                   |
| CustomerOverBudget | liczba całkowita          | Liczba klientów, którzy przemkną budżet.                                                                    |
| CustomersTrendingOver | liczba całkowita       | Liczba klientów, którzy są blisko przesunić budżet.                                                     |
| CustomersWithUsageBasedSubscriptions  | liczba całkowita | Liczba klientów z subskrypcją opartą na użyciu.                                               |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu. W kontekście rekordu CustomerMonthlyUsageRecord ten identyfikator jest identyfikatorem klienta. |
| ResourceName     | ciąg             | Nazwa zasobu. W kontekście rekordu CustomerMonthlyUsageRecord jest to nazwa klienta.               |
| BillingStartDate | data               | Data rozpoczęcia bieżącego okresu rozliczeniowego.                                                                    |
| BillingEndDate   | data               | Data zakończenia bieżącego okresu rozliczeniowego.                                                                      |
| Łączny koszt        | decimal             | Szacowany łączny koszt użycia całego klienta na podstawie bieżącego użycia od początku okresu rozliczeniowego.      |
| CurrencyLocale   | ciąg             | Wartości regionalnych waluty.                                                                                             |
| LastModifiedDate | data               | Data ostatniej modyfikacji danych użycia.                                                                       |
| Linki            | ResourceLinks      | Linki zasobów odpowiadające podsumowaniu użycia.                                                           |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające podsumowaniu użycia.                                                      |

## <a name="spendingbudget"></a>Budżet wydatków

**Budżet Wydatki reprezentuje** budżet przydzielony do tego klienta dla subskrypcji opartych na użyciu.

| Właściwość   | Typ               | Opis                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Kwota     | decimal             | Przydzielony budżet. Jeśli ta wartość ma wartość null, nie ma żadnego budżetu wydatków przydzielonego temu klientowi. |
| Atrybuty | ResourceAttributes | Atrybuty metadanych odpowiadające budżetowi.                                                |
