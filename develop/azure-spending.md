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
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="98d2c-103">Zasoby interfejsu API wydatków na platformę Azure umożliwiające zarządzanie wydatkami i obciążeniem klientów oraz korzystanie z budżetu</span><span class="sxs-lookup"><span data-stu-id="98d2c-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="98d2c-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="98d2c-104">**Applies to:**</span></span>

- <span data-ttu-id="98d2c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="98d2c-105">Partner Center</span></span>
- <span data-ttu-id="98d2c-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="98d2c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="98d2c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="98d2c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="98d2c-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="98d2c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="98d2c-109">Partnerzy dostawcy rozwiązań w chmurze mogą wyświetlać swoje wydatki na platformę Azure i zarządzać nimi za pomocą interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="98d2c-109">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="98d2c-110">Mogą również programistycznie wyświetlać wydatki klientów w porównaniu z budżetem wydatków na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="98d2c-110">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="98d2c-111">Aby uzyskać więcej informacji, zobacz [scenariusze, w których partnerzy programu CSP mogą używać interfejsów API Centrum partnerskiego do zarządzania kontami i zamówieniami klientów i partnerów](scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="98d2c-111">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="98d2c-112">Zarządzanie użyciem partnerów</span><span class="sxs-lookup"><span data-stu-id="98d2c-112">Partner usage management</span></span>

- <span data-ttu-id="98d2c-113">[Pobieranie podsumowania użycia partnerów](get-a-partner-usage-summary.md) przy użyciu zasobu **PartnerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="98d2c-113">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="98d2c-114">[Pobierz rekordy użycia dla wszystkich klientów](get-a-customer-s-usage-records.md) korzystających z zasobów **CustomerMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="98d2c-114">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="98d2c-115">Zarządzanie użyciem klienta</span><span class="sxs-lookup"><span data-stu-id="98d2c-115">Customer usage management</span></span>

- <span data-ttu-id="98d2c-116">[Pobieranie podsumowania użycia klienta](get-a-customer-usage-summary.md) przy użyciu zasobu **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="98d2c-116">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="98d2c-117">[Pobierz wszystkie rekordy użycia subskrypcji dla klienta](get-a-customer-subscription-s-usage-records.md) przy użyciu zasobu **SubscriptionMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="98d2c-117">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="98d2c-118">Zarządzanie użyciem subskrypcji</span><span class="sxs-lookup"><span data-stu-id="98d2c-118">Subscription usage management</span></span>

- <span data-ttu-id="98d2c-119">[Pobieranie podsumowania użycia subskrypcji](get-a-customer-subscription-usage-summary.md) przy użyciu zasobu **SubscriptionUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="98d2c-119">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="98d2c-120">[Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji](get-all-monthly-usage-records-for-a-subscription.md) przy użyciu zasobu **AzureResourceMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="98d2c-120">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="98d2c-121">[Pobieranie danych użycia dla subskrypcji przez zasób](get-a-customer-subscription-resource-usage-records.md) przy użyciu zasobu **ResourceUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="98d2c-121">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="98d2c-122">[Pobieranie danych użycia dla subskrypcji przez licznik](get-a-customer-subscription-meter-usage-records.md) przy użyciu zasobu **MeterUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="98d2c-122">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="98d2c-123">Zarządzanie budżetem przez platformę Azure</span><span class="sxs-lookup"><span data-stu-id="98d2c-123">Azure spending budget management</span></span>

- <span data-ttu-id="98d2c-124">[Pobieranie budżetu użycia klienta](get-a-customer-s-usage-spending-budget.md) przy użyciu zasobu **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="98d2c-124">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="98d2c-125">[Aktualizowanie budżetu użycia klienta](update-a-customer-s-usage-spending-budget.md) przy użyciu zasobu **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="98d2c-125">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
