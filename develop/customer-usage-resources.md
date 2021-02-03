---
title: Zasoby użycia klienta
description: Zasoby dla klientów korzystających z subskrypcji opartych na użyciu i budżetów miesięcznych użycia (w tym CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary i SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ec82fcfe6c08a8ad55dd1fb48984859b954dd3c8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767737"
---
# <a name="customer-usage-resources"></a>Zasoby użycia klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Klienci z subskrypcjami opartymi na użyciu mogą korzystać z budżetu miesięcznego. Ten budżet określa limit maksymalnego użycia klienta i umożliwia partnerom śledzenie ich użycia w czasie.

> [!NOTE]
> Numery użycia klientów to oszacowania (nie wartości końcowe), które nie powinny być używane na potrzeby rozliczeń.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** reprezentuje szacowany koszt pieniężny użycia klienta w bieżącym miesiącu.

| Właściwość         | Typ               | Opis                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budżet           | SpendingBudget     | Budżet wydatków przyznany klientowi.                          |
| PercentUsed      | decimal             | Procent używany z przydzielonym budżetem.                        |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu.                                   |
| ResourceName     | ciąg             | Nazwa zasobu.                                                |
| TotalCost        | decimal             | Szacowany łączny koszt użycia zasobów w ramach subskrypcji.|
| CurrencyLocale   | ciąg             | Ustawienia regionalne waluty klienta. Dostępne dla subskrypcji Microsoft Azure (MS-AZR-0145P).            |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.           |
| USDTotalCost     | decimal             | Pobiera lub ustawia Szacowany łączny koszt w USD. Dostępne dla planów platformy Azure.                                         |
| Isupgraded       | bool             | Pobiera lub ustawia wartość wskazującą, czy subskrypcja platformy Azure klienta została uaktualniona. Wartość **true** reprezentuje klientów, którzy mają plan platformy Azure.                         |
| LastModifiedDate | date               | Data ostatniej modyfikacji danych użycia.                               |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające rekordowi użycia.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** reprezentuje Podsumowanie użycia klienta dla całego okresu rozliczeniowego.

| Właściwość         | Typ               | Opis                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budżet           | SpendingBudget     | Budżet wydatków przyznany klientowi.                                                                  |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu. W kontekście CustomerMonthlyUsageRecord identyfikator to identyfikator klienta. |
| ResourceName     | ciąg             | Nazwa zasobu. W kontekście CustomerMonthlyUsageRecord jest to nazwa klienta.               |
| BillingStartDate | date               | Data rozpoczęcia bieżącego okresu rozliczeniowego.                                                                    |
| BillingEndDate   | date               | Data końcowa bieżącego okresu rozliczeniowego.                                                                      |
| TotalCost        | decimal             | Szacowany łączny koszt użycia zasobów w ramach subskrypcji.                                         |
| CurrencyLocale   | ciąg             | Ustawienia regionalne waluty klienta. Dostępne dla subskrypcji Microsoft Azure (MS-AZR-0145P).                                         |
| CurrencyCode     | ciąg             | Pobiera lub ustawia kod waluty. Dostępne dla planów platformy Azure.                                         |
| USDTotalCost     | decimal             | Pobiera lub ustawia Szacowany łączny koszt w USD. Dostępne dla zasobów subskrypcji planu platformy Azure.                                         |
| LastModifiedDate | date               | Data ostatniej modyfikacji danych użycia.                                                                       |
| Linki            | ResourceLinks      | Linki do zasobów powiązane z podsumowaniem użycia.                                                           |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające podsumowaniem użycia.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** przedstawia podsumowanie użycia budżetu na poziomie partnera dla wszystkich klientów.

| Właściwość         | Typ               | Opis                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | tablica ciągów   | Lista adresów e-mail dla powiadomień.                                                                   |
| CustomerOverBudget | liczba całkowita          | Liczba klientów, którzy przekraczają budżet.                                                                    |
| CustomersTrendingOver | liczba całkowita       | Liczba klientów, którzy są blisko przechodzenia przez budżet.                                                     |
| CustomersWithUsageBasedSubscriptions  | liczba całkowita | Liczba klientów z subskrypcją opartą na użyciu.                                               |
| ResourceId       | ciąg             | Unikatowy identyfikator zasobu. W kontekście CustomerMonthlyUsageRecord identyfikator to identyfikator klienta. |
| ResourceName     | ciąg             | Nazwa zasobu. W kontekście CustomerMonthlyUsageRecord jest to nazwa klienta.               |
| BillingStartDate | date               | Data rozpoczęcia bieżącego okresu rozliczeniowego.                                                                    |
| BillingEndDate   | date               | Data końcowa bieżącego okresu rozliczeniowego.                                                                      |
| TotalCost        | decimal             | Szacowany łączny koszt wszystkich klientów użycia na podstawie bieżącego użycia od początku okresu rozliczeniowego.      |
| CurrencyLocale   | ciąg             | Ustawienia regionalne waluty.                                                                                             |
| LastModifiedDate | date               | Data ostatniej modyfikacji danych użycia.                                                                       |
| Linki            | ResourceLinks      | Linki do zasobów powiązane z podsumowaniem użycia.                                                           |
| Atrybuty       | ResourceAttributes | Atrybuty metadanych odpowiadające podsumowaniem użycia.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget** reprezentuje budżet przypisany do tego klienta na potrzeby subskrypcji opartych na użyciu.

| Właściwość   | Typ               | Opis                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Kwota     | decimal             | Przydzielony budżet. Jeśli wartość jest równa null, nie istnieje budżet wydatków przypisany do tego klienta. |
| Atrybuty | ResourceAttributes | Atrybuty metadanych odpowiadające budżetowi.                                                |
