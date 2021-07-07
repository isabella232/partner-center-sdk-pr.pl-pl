---
title: Zasoby interfejsu API wydatków platformy Azure
description: Dowiedz się, jak partnerzy programu CSP mogą używać Partner Center API do wyświetlania wydatków i użycia platformy Azure dla partnerów i klientów oraz zarządzania nimi w stosunku do ich budżetu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 472554de1c354559d5bc4b21959c109467891806
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974322"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="801cb-103">Zasoby interfejsu API wydatków platformy Azure do zarządzania wydatkami i użyciem partnerów lub klientów względem budżetu</span><span class="sxs-lookup"><span data-stu-id="801cb-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="801cb-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="801cb-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="801cb-105">Dostawca rozwiązań w chmurze (CSP) mogą wyświetlać wydatki na platformę Azure i zarządzać nimi za pośrednictwem Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="801cb-105">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="801cb-106">Mogą również programowo wyświetlać wydatki klientów względem budżetu wydatków na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="801cb-106">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="801cb-107">Aby uzyskać więcej informacji, zobacz scenariusze, w których partnerzy programu CSP mogą używać interfejsów API Partner Center do zarządzania kontami klientów i [partnerów oraz zamówieniami.](scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="801cb-107">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="801cb-108">Zarządzanie użyciem partnerów</span><span class="sxs-lookup"><span data-stu-id="801cb-108">Partner usage management</span></span>

- <span data-ttu-id="801cb-109">[Uzyskiwanie podsumowania użycia partnera przy](get-a-partner-usage-summary.md) użyciu zasobu **PartnerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="801cb-109">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="801cb-110">[Uzyskiwanie rekordów użycia dla wszystkich klientów przy](get-a-customer-s-usage-records.md) użyciu zasobu **CustomerMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="801cb-110">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="801cb-111">Zarządzanie użyciem przez klientów</span><span class="sxs-lookup"><span data-stu-id="801cb-111">Customer usage management</span></span>

- <span data-ttu-id="801cb-112">[Pobierz podsumowanie użycia klienta przy użyciu](get-a-customer-usage-summary.md) zasobu **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="801cb-112">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="801cb-113">[Pobierz wszystkie rekordy użycia subskrypcji dla klienta przy](get-a-customer-subscription-s-usage-records.md) użyciu zasobu **SubscriptionMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="801cb-113">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="801cb-114">Zarządzanie użyciem subskrypcji</span><span class="sxs-lookup"><span data-stu-id="801cb-114">Subscription usage management</span></span>

- <span data-ttu-id="801cb-115">[Uzyskiwanie podsumowania użycia subskrypcji przy](get-a-customer-subscription-usage-summary.md) użyciu zasobu **SubscriptionUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="801cb-115">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="801cb-116">[Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji przy](get-all-monthly-usage-records-for-a-subscription.md) użyciu zasobu **AzureResourceMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="801cb-116">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="801cb-117">[Uzyskiwanie danych użycia dla subskrypcji według zasobu przy](get-a-customer-subscription-resource-usage-records.md) użyciu zasobu **ResourceUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="801cb-117">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="801cb-118">[Uzyskiwanie danych użycia subskrypcji według miernika przy](get-a-customer-subscription-meter-usage-records.md) użyciu **zasobu MeterUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="801cb-118">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="801cb-119">Zarządzanie budżetem wydatków na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="801cb-119">Azure spending budget management</span></span>

- <span data-ttu-id="801cb-120">[Uzyskiwanie budżetu użycia klienta przy](get-a-customer-s-usage-spending-budget.md) użyciu zasobu **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="801cb-120">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="801cb-121">[Aktualizowanie budżetu użycia klienta przy](update-a-customer-s-usage-spending-budget.md) użyciu zasobu **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="801cb-121">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
