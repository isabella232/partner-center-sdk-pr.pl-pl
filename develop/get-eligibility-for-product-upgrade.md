---
title: Sprawdź uprawnienia klienta do uaktualniania do planu platformy Azure
description: Za pomocą zasobu ProductUpgradeRequest można zwrócić zasób ProductUpgradesEligibility w celu ustalenia, czy klient ma uprawnienia do uaktualnienia z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767690"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="9552a-103">Sprawdź uprawnienia klienta do uaktualniania do planu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9552a-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="9552a-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="9552a-104">**Applies to:**</span></span>

- <span data-ttu-id="9552a-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9552a-105">Partner Center</span></span>

<span data-ttu-id="9552a-106">Możesz użyć zasobu [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) , aby sprawdzić, czy klient jest uprawniony do uaktualnienia do planu platformy Azure z subskrypcji Microsoft Azure (MS-AZR-0145P) Ta metoda zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) z uprawnieniem do uaktualnienia produktu klienta.</span><span class="sxs-lookup"><span data-stu-id="9552a-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9552a-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9552a-107">Prerequisites</span></span>

- <span data-ttu-id="9552a-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9552a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9552a-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9552a-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="9552a-110">Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="9552a-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="9552a-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9552a-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9552a-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="9552a-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9552a-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="9552a-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9552a-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="9552a-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9552a-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="9552a-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9552a-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9552a-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9552a-117">Rodzina produktów.</span><span class="sxs-lookup"><span data-stu-id="9552a-117">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="9552a-118">C\#</span><span class="sxs-lookup"><span data-stu-id="9552a-118">C\#</span></span>

<span data-ttu-id="9552a-119">Aby sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="9552a-119">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="9552a-120">Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz "Azure" jako rodzinę produktów.</span><span class="sxs-lookup"><span data-stu-id="9552a-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="9552a-121">Użyj kolekcji **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="9552a-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="9552a-122">Wywołaj metodę **CheckEligibility** i przekaż obiekt **ProductUpgradesRequest** , który zwróci obiekt **ProductUpgradesEligibility** .</span><span class="sxs-lookup"><span data-stu-id="9552a-122">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="9552a-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9552a-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9552a-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9552a-124">Request syntax</span></span>

| <span data-ttu-id="9552a-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="9552a-125">Method</span></span>   | <span data-ttu-id="9552a-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9552a-126">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="9552a-127">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="9552a-127">**POST**</span></span> | <span data-ttu-id="9552a-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/productUpgrades/Eligibility http/1.1</span><span class="sxs-lookup"><span data-stu-id="9552a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9552a-129">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9552a-129">Request headers</span></span>

<span data-ttu-id="9552a-130">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9552a-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9552a-131">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9552a-131">Request body</span></span>

<span data-ttu-id="9552a-132">Treść żądania musi zawierać zasób [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="9552a-132">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="9552a-133">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9552a-133">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="9552a-134">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9552a-134">REST response</span></span>

<span data-ttu-id="9552a-135">Jeśli to się powiedzie, metoda zwraca zasób [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) w treści.</span><span class="sxs-lookup"><span data-stu-id="9552a-135">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9552a-136">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9552a-136">Response success and error codes</span></span>

<span data-ttu-id="9552a-137">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9552a-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9552a-138">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9552a-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9552a-139">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9552a-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9552a-140">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9552a-140">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
