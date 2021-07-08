---
title: Pobieranie listy uprawnień platformy Azure dla subskrypcji
description: Zasób AzureEntitlement umożliwia pobieranie kolekcji zasobów uprawnień platformy Azure należących do subskrypcji.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 280da155122ed9efd99838d7819fb34f8f7ec52c
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874367"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="9d547-103">Pobieranie listy uprawnień platformy Azure dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9d547-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="9d547-104">Zasób uprawnień [platformy Azure](subscription-resources.md#azureentitlement) **(AzureEntitlement)** umożliwia pobieranie kolekcji zasobów należących do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9d547-104">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d547-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9d547-105">Prerequisites</span></span>

- <span data-ttu-id="9d547-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9d547-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9d547-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d547-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9d547-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9d547-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9d547-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9d547-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9d547-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="9d547-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9d547-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="9d547-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9d547-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="9d547-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9d547-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9d547-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9d547-114">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9d547-114">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="9d547-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9d547-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9d547-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9d547-116">Request syntax</span></span>

| <span data-ttu-id="9d547-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="9d547-117">Method</span></span>  | <span data-ttu-id="9d547-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9d547-118">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="9d547-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9d547-119">**GET**</span></span> | <span data-ttu-id="9d547-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9d547-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="9d547-121">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="9d547-121">URI parameters</span></span>

<span data-ttu-id="9d547-122">W poniższej tabeli wymieniono wymagane parametry zapytania w celu uzyskania wszystkich uprawnień platformy Azure dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9d547-122">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="9d547-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9d547-123">Name</span></span>                   | <span data-ttu-id="9d547-124">Typ</span><span class="sxs-lookup"><span data-stu-id="9d547-124">Type</span></span>     | <span data-ttu-id="9d547-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9d547-125">Required</span></span> | <span data-ttu-id="9d547-126">Opis</span><span class="sxs-lookup"><span data-stu-id="9d547-126">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="9d547-127">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="9d547-127">**customer-tenant-id**</span></span> | <span data-ttu-id="9d547-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="9d547-128">**guid**</span></span> | <span data-ttu-id="9d547-129">Y</span><span class="sxs-lookup"><span data-stu-id="9d547-129">Y</span></span>        | <span data-ttu-id="9d547-130">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="9d547-130">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="9d547-131">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="9d547-131">**subscription-id**</span></span>       | <span data-ttu-id="9d547-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="9d547-132">**guid**</span></span> | <span data-ttu-id="9d547-133">Y</span><span class="sxs-lookup"><span data-stu-id="9d547-133">Y</span></span>        | <span data-ttu-id="9d547-134">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9d547-134">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="9d547-135">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9d547-135">Request headers</span></span>

<span data-ttu-id="9d547-136">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9d547-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9d547-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9d547-137">Request body</span></span>

<span data-ttu-id="9d547-138">Brak.</span><span class="sxs-lookup"><span data-stu-id="9d547-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9d547-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9d547-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9d547-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9d547-140">REST response</span></span>

<span data-ttu-id="9d547-141">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [**AzureEntitlement**](subscription-resources.md#azureentitlement) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9d547-141">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9d547-142">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9d547-142">Response success and error codes</span></span>

<span data-ttu-id="9d547-143">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9d547-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9d547-144">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9d547-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9d547-145">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9d547-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9d547-146">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9d547-146">Response example</span></span>

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
