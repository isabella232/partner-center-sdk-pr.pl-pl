---
title: Zasoby interfejsu API do wydatków platformy Azure
description: Dowiedz się, w jaki sposób partnerzy usług kryptograficznych mogą używać interfejsów API Centrum partnerskiego, aby wyświetlać i zarządzać wydatkami i użyciem platformy Azure w porównaniu z budżetem.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a2995a06473cc6990d1234acd522a3b38a03d3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768538"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Zasoby interfejsu API wydatków na platformę Azure umożliwiające zarządzanie wydatkami i obciążeniem klientów oraz korzystanie z budżetu 

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Partnerzy dostawcy rozwiązań w chmurze mogą wyświetlać swoje wydatki na platformę Azure i zarządzać nimi za pomocą interfejsów API Centrum partnerskiego. Mogą również programistycznie wyświetlać wydatki klientów w porównaniu z budżetem wydatków na platformę Azure.

Aby uzyskać więcej informacji, zobacz [scenariusze, w których partnerzy programu CSP mogą używać interfejsów API Centrum partnerskiego do zarządzania kontami i zamówieniami klientów i partnerów](scenarios.md).

## <a name="partner-usage-management"></a>Zarządzanie użyciem partnerów

- [Pobieranie podsumowania użycia partnerów](get-a-partner-usage-summary.md) przy użyciu zasobu **PartnerUsageSummary**
- [Pobierz rekordy użycia dla wszystkich klientów](get-a-customer-s-usage-records.md) korzystających z zasobów **CustomerMonthlyUsageRecord**

## <a name="customer-usage-management"></a>Zarządzanie użyciem klienta

- [Pobieranie podsumowania użycia klienta](get-a-customer-usage-summary.md) przy użyciu zasobu **CustomerUsageSummary**
- [Pobierz wszystkie rekordy użycia subskrypcji dla klienta](get-a-customer-subscription-s-usage-records.md) przy użyciu zasobu **SubscriptionMonthlyUsageRecord**

## <a name="subscription-usage-management"></a>Zarządzanie użyciem subskrypcji

- [Pobieranie podsumowania użycia subskrypcji](get-a-customer-subscription-usage-summary.md) przy użyciu zasobu **SubscriptionUsageSummary**
- [Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji](get-all-monthly-usage-records-for-a-subscription.md) przy użyciu zasobu **AzureResourceMonthlyUsageRecord**
- [Pobieranie danych użycia dla subskrypcji przez zasób](get-a-customer-subscription-resource-usage-records.md) przy użyciu zasobu **ResourceUsageRecord**
- [Pobieranie danych użycia dla subskrypcji przez licznik](get-a-customer-subscription-meter-usage-records.md) przy użyciu zasobu **MeterUsageRecord**

## <a name="azure-spending-budget-management"></a>Zarządzanie budżetem przez platformę Azure

- [Pobieranie budżetu użycia klienta](get-a-customer-s-usage-spending-budget.md) przy użyciu zasobu **CustomerUsageSummary**
- [Aktualizowanie budżetu użycia klienta](update-a-customer-s-usage-spending-budget.md) przy użyciu zasobu **CustomerUsageSummary**
