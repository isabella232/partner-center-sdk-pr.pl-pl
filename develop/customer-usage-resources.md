---
title: Zasoby dotyczące użycia przez klientów
description: Zasoby dla klientów z subskrypcjami opartymi na użyciu i budżetami użycia miesięcznego (w tym CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary i SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066fd84f872365b419796f00125c097c685f4579731aaacd67e826bf671bd789
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995156"
---
# <a name="customer-usage-resources"></a>Zasoby dotyczące użycia przez klientów

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Klienci z subskrypcjami opartymi na użyciu mogą mieć miesięczny budżet użycia. Ten budżet ustawia limit maksymalnego użycia klienta i umożliwia partnerowi śledzenie ich użycia w czasie.

> [!NOTE]
> Numery użycia klientów to oszacowania (a nie wartości końcowe), których nie należy używać do celów rozliczeniowych.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**Rekord CustomerMonthlyUsageRecord** reprezentuje szacowany koszt pieniężny użycia klienta w bieżącym miesiącu.

| Właściwość         | Typ               | Opis                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budżet           | Budżet wydatków     | Budżet wydatków przydzielony dla klienta.                          |
| PercentUsed      | decimal             | Wartość procentowa wykorzystana w przydzielonym budżecie.                        |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu.                                   |
| ResourceName     | ciąg             | Nazwa zasobu.                                                |
| Łączny koszt        | decimal             | Szacowany całkowity koszt użycia zasobów w subskrypcji.|
| CurrencyLocale   | ciąg             | Waluty klienta. Dostępne Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P).            |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.           |
| USDTotalCost     | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla planów platformy Azure.                                         |
| IsUpgraded       | bool             | Pobiera lub ustawia wartość wskazującą, czy subskrypcja platformy Azure klienta została uaktualniona. Wartość true **reprezentuje klientów,** którzy mają plan platformy Azure.                         |
| LastModifiedDate | data               | Data ostatniej modyfikacji danych użycia.                               |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające rekordowi użycia.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** reprezentuje podsumowanie użycia klienta w całym okresie rozliczeniowym.

| Właściwość         | Typ               | Opis                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budżet           | Budżet wydatków     | Budżet wydatków przydzielony dla klienta.                                                                  |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu. W kontekście rekordu CustomerMonthlyUsageRecord ten identyfikator jest identyfikatorem klienta. |
| ResourceName     | ciąg             | Nazwa zasobu. W kontekście rekordu CustomerMonthlyUsageRecord jest to nazwa klienta.               |
| BillingStartDate | data               | Data rozpoczęcia bieżącego okresu rozliczeniowego.                                                                    |
| BillingEndDate   | data               | Data zakończenia bieżącego okresu rozliczeniowego.                                                                      |
| Łączny koszt        | decimal             | Szacowany całkowity koszt użycia zasobów w subskrypcji.                                         |
| CurrencyLocale   | ciąg             | Waluty klienta. Dostępne Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P).                                         |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.                                         |
| USDTotalCost     | decimal             | Pobiera lub ustawia szacowany łączny koszt w USD. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| LastModifiedDate | data               | Data ostatniej modyfikacji danych użycia.                                                                       |
| Linki            | ResourceLinks      | Linki zasobów odpowiadające podsumowaniu użycia.                                                           |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające podsumowaniu użycia.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** reprezentuje podsumowanie budżetu użycia dla wszystkich klientów na poziomie partnera.

| Właściwość         | Typ               | Opis                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Wiadomości e-mailToNotify   | tablica ciągów   | Lista adresów e-mail dla powiadomień.                                                                   |
| CustomerOverBudget | liczba całkowita          | Liczba klientów, którzy przesłonili budżet.                                                                    |
| CustomersTrendingOver | liczba całkowita       | Liczba klientów, którzy są blisko przesłoni budżetu.                                                     |
| CustomersWithUsageBasedSubscriptions  | liczba całkowita | Liczba klientów z subskrypcją opartą na użyciu.                                               |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu. W kontekście rekordu CustomerMonthlyUsageRecord ten identyfikator jest identyfikatorem klienta. |
| ResourceName     | ciąg             | Nazwa zasobu. W kontekście rekordu CustomerMonthlyUsageRecord jest to nazwa klienta.               |
| BillingStartDate | data               | Data rozpoczęcia bieżącego okresu rozliczeniowego.                                                                    |
| BillingEndDate   | data               | Data zakończenia bieżącego okresu rozliczeniowego.                                                                      |
| Łączny koszt        | decimal             | Szacowany łączny koszt użycia wszystkich klientów na podstawie bieżącego użycia od początku okresu rozliczeniowego.      |
| CurrencyLocale   | ciąg             | Wartości regionalnych waluty.                                                                                             |
| LastModifiedDate | data               | Data ostatniej modyfikacji danych użycia.                                                                       |
| Linki            | ResourceLinks      | Linki zasobów odpowiadające podsumowaniu użycia.                                                           |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające podsumowaniu użycia.                                                      |

## <a name="spendingbudget"></a>WydatkiBudget

**WydatkiBudyt** reprezentuje budżet przydzielony do tego klienta dla subskrypcji opartych na użyciu.

| Właściwość   | Typ               | Opis                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Kwota     | decimal             | Przydzielony budżet. Jeśli wartość jest pusta, nie ma żadnego budżetu wydatków przydzielonego temu klientowi. |
| Atrybuty | ResourceAttributes | Atrybuty metadanych odpowiadające budżetowi.                                                |
