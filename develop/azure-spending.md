---
title: Zasoby interfejsu API wydatków na platformę Azure
description: Dowiedz się, jak partnerzy programu CSP mogą używać Partner Center API do wyświetlania wydatków i użycia platformy Azure dla partnerów i klientów oraz zarządzania nimi w stosunku do ich budżetu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b51ccbcdaee18b6d5b3bd1b9531a64b22c8bac5a9d95e6cf94291ee802ed5d9
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992402"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Zasoby interfejsu API wydatków platformy Azure do zarządzania wydatkami i użyciem partnerów lub klientów względem budżetu 

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Dostawca rozwiązań w chmurze (CSP) mogą wyświetlać swoje wydatki na platformę Azure i zarządzać nimi za pośrednictwem Partner Center API. Mogą również programowo wyświetlać wydatki klientów względem budżetu wydatków platformy Azure.

Aby uzyskać więcej informacji, zobacz scenariusze, w których partnerzy programu CSP mogą używać interfejsów API Partner Center do zarządzania kontami klientów i [partnerów oraz zamówieniami.](scenarios.md)

## <a name="partner-usage-management"></a>Zarządzanie użyciem partnerów

- [Uzyskiwanie podsumowania użycia partnera przy](get-a-partner-usage-summary.md) użyciu zasobu **PartnerUsageSummary**
- [Uzyskiwanie rekordów użycia dla wszystkich klientów przy](get-a-customer-s-usage-records.md) użyciu zasobu **CustomerMonthlyUsageRecord**

## <a name="customer-usage-management"></a>Zarządzanie użyciem przez klientów

- [Pobierz podsumowanie użycia klienta przy](get-a-customer-usage-summary.md) użyciu zasobu **CustomerUsageSummary**
- [Pobierz wszystkie rekordy użycia subskrypcji dla klienta przy](get-a-customer-subscription-s-usage-records.md) użyciu zasobu **SubscriptionMonthlyUsageRecord**

## <a name="subscription-usage-management"></a>Zarządzanie użyciem subskrypcji

- [Uzyskiwanie podsumowania użycia subskrypcji przy](get-a-customer-subscription-usage-summary.md) użyciu zasobu **SubscriptionUsageSummary**
- [Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji przy](get-all-monthly-usage-records-for-a-subscription.md) użyciu zasobu **AzureResourceMonthlyUsageRecord**
- [Uzyskiwanie danych użycia dla subskrypcji według zasobu przy](get-a-customer-subscription-resource-usage-records.md) użyciu zasobu **ResourceUsageRecord**
- [Uzyskiwanie danych użycia dla subskrypcji według miernika](get-a-customer-subscription-meter-usage-records.md) przy użyciu **zasobu MeterUsageRecord**

## <a name="azure-spending-budget-management"></a>Zarządzanie budżetem wydatków na platformie Azure

- [Uzyskiwanie budżetu użycia klienta przy](get-a-customer-s-usage-spending-budget.md) użyciu zasobu **CustomerUsageSummary**
- [Aktualizowanie budżetu użycia klienta przy](update-a-customer-s-usage-spending-budget.md) użyciu zasobu **CustomerUsageSummary**
