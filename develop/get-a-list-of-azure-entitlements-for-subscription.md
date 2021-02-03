---
title: Pobieranie listy uprawnień platformy Azure dla subskrypcji
description: Możesz użyć zasobu AzureEntitlement, aby uzyskać kolekcję zasobów uprawnień platformy Azure należących do subskrypcji.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: d7d0a10c571dc073bd49e82084f3b7ece7234daf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767953"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="5c74c-103">Pobieranie listy uprawnień platformy Azure dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5c74c-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="5c74c-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="5c74c-104">**Applies to:**</span></span>

- <span data-ttu-id="5c74c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="5c74c-105">Partner Center</span></span>

<span data-ttu-id="5c74c-106">Możesz użyć [zasobu uprawnienia platformy Azure](subscription-resources.md#azureentitlement) (**AzureEntitlement**), aby uzyskać kolekcję zasobów należących do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c74c-106">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c74c-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c74c-107">Prerequisites</span></span>

- <span data-ttu-id="5c74c-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5c74c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5c74c-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c74c-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5c74c-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5c74c-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5c74c-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5c74c-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5c74c-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="5c74c-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5c74c-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="5c74c-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5c74c-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="5c74c-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5c74c-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5c74c-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5c74c-116">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c74c-116">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5c74c-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5c74c-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c74c-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5c74c-118">Request syntax</span></span>

| <span data-ttu-id="5c74c-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="5c74c-119">Method</span></span>  | <span data-ttu-id="5c74c-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5c74c-120">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="5c74c-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="5c74c-121">**GET**</span></span> | <span data-ttu-id="5c74c-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/azureentitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="5c74c-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5c74c-123">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="5c74c-123">URI parameters</span></span>

<span data-ttu-id="5c74c-124">Poniższa tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać wszystkie uprawnienia platformy Azure do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c74c-124">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="5c74c-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5c74c-125">Name</span></span>                   | <span data-ttu-id="5c74c-126">Typ</span><span class="sxs-lookup"><span data-stu-id="5c74c-126">Type</span></span>     | <span data-ttu-id="5c74c-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5c74c-127">Required</span></span> | <span data-ttu-id="5c74c-128">Opis</span><span class="sxs-lookup"><span data-stu-id="5c74c-128">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="5c74c-129">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="5c74c-129">**customer-tenant-id**</span></span> | <span data-ttu-id="5c74c-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="5c74c-130">**guid**</span></span> | <span data-ttu-id="5c74c-131">Y</span><span class="sxs-lookup"><span data-stu-id="5c74c-131">Y</span></span>        | <span data-ttu-id="5c74c-132">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="5c74c-132">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="5c74c-133">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="5c74c-133">**subscription-id**</span></span>       | <span data-ttu-id="5c74c-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="5c74c-134">**guid**</span></span> | <span data-ttu-id="5c74c-135">Y</span><span class="sxs-lookup"><span data-stu-id="5c74c-135">Y</span></span>        | <span data-ttu-id="5c74c-136">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c74c-136">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="5c74c-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5c74c-137">Request headers</span></span>

<span data-ttu-id="5c74c-138">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5c74c-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5c74c-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5c74c-139">Request body</span></span>

<span data-ttu-id="5c74c-140">Brak.</span><span class="sxs-lookup"><span data-stu-id="5c74c-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5c74c-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5c74c-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="5c74c-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5c74c-142">REST response</span></span>

<span data-ttu-id="5c74c-143">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [**AzureEntitlement**](subscription-resources.md#azureentitlement) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5c74c-143">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c74c-144">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5c74c-144">Response success and error codes</span></span>

<span data-ttu-id="5c74c-145">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5c74c-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c74c-146">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5c74c-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c74c-147">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5c74c-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5c74c-148">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5c74c-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
```
