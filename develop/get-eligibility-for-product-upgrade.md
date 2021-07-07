---
title: Sprawdzanie uprawnień klienta do uaktualnienia do planu platformy Azure
description: Zasób ProductUpgradeRequest umożliwia zwrócenie zasobu ProductUpgradesEligibility w celu określenia, czy klient kwalifikuje się do uaktualnienia z subskrypcji usługi Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 34a20611c7d92042b5432c5ffb3ba4702d77e0c2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446262"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="347b8-103">Sprawdzanie uprawnień klienta do uaktualnienia do planu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="347b8-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="347b8-104">Za pomocą zasobu [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) możesz sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure z subskrypcji usługi Microsoft Azure (MS-AZR-0145P) Ta metoda zwraca [**zasób ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) z uprawnieniami do uaktualnienia produktu klienta.</span><span class="sxs-lookup"><span data-stu-id="347b8-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347b8-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="347b8-105">Prerequisites</span></span>

- <span data-ttu-id="347b8-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="347b8-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="347b8-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="347b8-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="347b8-108">Postępuj zgodnie z [modelem bezpiecznej aplikacji w](enable-secure-app-model.md) przypadku korzystania z uwierzytelniania app+user z Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="347b8-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="347b8-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="347b8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="347b8-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="347b8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="347b8-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="347b8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="347b8-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="347b8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="347b8-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="347b8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="347b8-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="347b8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="347b8-115">Rodzina produktów.</span><span class="sxs-lookup"><span data-stu-id="347b8-115">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="347b8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="347b8-116">C\#</span></span>

<span data-ttu-id="347b8-117">Aby sprawdzić, czy klient kwalifikuje się do uaktualnienia do planu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="347b8-117">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="347b8-118">Utwórz obiekt **ProductUpgradesRequest** i określ identyfikator klienta oraz wartość "Azure" jako rodzinę produktów.</span><span class="sxs-lookup"><span data-stu-id="347b8-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="347b8-119">Użyj **kolekcji IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="347b8-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="347b8-120">Wywołaj **metodę CheckEligibility** i przekaż obiekt **ProductUpgradesRequest,** który zwróci **obiekt ProductUpgradesEligibility.**</span><span class="sxs-lookup"><span data-stu-id="347b8-120">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="347b8-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="347b8-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="347b8-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="347b8-122">Request syntax</span></span>

| <span data-ttu-id="347b8-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="347b8-123">Method</span></span>   | <span data-ttu-id="347b8-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="347b8-124">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="347b8-125">**Post**</span><span class="sxs-lookup"><span data-stu-id="347b8-125">**POST**</span></span> | <span data-ttu-id="347b8-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="347b8-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="347b8-127">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="347b8-127">Request headers</span></span>

<span data-ttu-id="347b8-128">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="347b8-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="347b8-129">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="347b8-129">Request body</span></span>

<span data-ttu-id="347b8-130">Treść żądania musi zawierać [**zasób ProductUpgradeRequest.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="347b8-130">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="347b8-131">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="347b8-131">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="347b8-132">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="347b8-132">REST response</span></span>

<span data-ttu-id="347b8-133">W przypadku powodzenia ta metoda zwraca [**zasób ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) w treści.</span><span class="sxs-lookup"><span data-stu-id="347b8-133">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="347b8-134">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="347b8-134">Response success and error codes</span></span>

<span data-ttu-id="347b8-135">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="347b8-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="347b8-136">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="347b8-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="347b8-137">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="347b8-137">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="347b8-138">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="347b8-138">Response example</span></span>

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
