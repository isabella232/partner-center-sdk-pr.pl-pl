---
title: Pobieranie jednostki SKU według identyfikatora
description: Pobiera wartość SKU dla określonego produktu przy użyciu określonego identyfikatora SKU.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9516a87a438a0a84a6f6069c1f9b2a2e97e90fba
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873857"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="68068-103">Pobieranie jednostki SKU według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="68068-103">Get a SKU by ID</span></span>

<span data-ttu-id="68068-104">Pobiera wartość SKU dla określonego produktu przy użyciu określonego identyfikatora SKU.</span><span class="sxs-lookup"><span data-stu-id="68068-104">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68068-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="68068-105">Prerequisites</span></span>

- <span data-ttu-id="68068-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="68068-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="68068-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="68068-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="68068-108">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="68068-108">A product ID.</span></span>

- <span data-ttu-id="68068-109">Identyfikator SKU.</span><span class="sxs-lookup"><span data-stu-id="68068-109">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="68068-110">C\#</span><span class="sxs-lookup"><span data-stu-id="68068-110">C\#</span></span>

<span data-ttu-id="68068-111">Aby uzyskać szczegółowe informacje o określonej określonej sku, zacznij od kroków z artykułu Get [a product by ID (Uzyskiwanie](get-a-product-by-id.md) produktu według identyfikatora) w celu uzyskania interfejsu dla operacji określonego produktu.</span><span class="sxs-lookup"><span data-stu-id="68068-111">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="68068-112">Z wynikowego interfejsu wybierz właściwość **Jednostki SKU,** aby uzyskać interfejs z dostępnymi operacjami dla jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="68068-112">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="68068-113">Przekaż identyfikator SKU do metody **ById()** i wywołaj metodę **Get()** lub **GetAsync(),** aby pobrać szczegóły dotyczące tej drugiej.</span><span class="sxs-lookup"><span data-stu-id="68068-113">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="68068-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="68068-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="68068-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="68068-115">Request syntax</span></span>

| <span data-ttu-id="68068-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="68068-116">Method</span></span>  | <span data-ttu-id="68068-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="68068-117">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68068-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="68068-118">**GET**</span></span> | <span data-ttu-id="68068-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{identyfikator-produktu}/skus/{sku-id}?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="68068-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="68068-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="68068-120">URI parameter</span></span>

<span data-ttu-id="68068-121">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać wartość SKU dla określonego produktu przy użyciu określonego identyfikatora SKU.</span><span class="sxs-lookup"><span data-stu-id="68068-121">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="68068-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="68068-122">Name</span></span>                   | <span data-ttu-id="68068-123">Typ</span><span class="sxs-lookup"><span data-stu-id="68068-123">Type</span></span>     | <span data-ttu-id="68068-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="68068-124">Required</span></span> | <span data-ttu-id="68068-125">Opis</span><span class="sxs-lookup"><span data-stu-id="68068-125">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="68068-126">identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="68068-126">product-id</span></span>             | <span data-ttu-id="68068-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="68068-127">string</span></span>   | <span data-ttu-id="68068-128">Tak</span><span class="sxs-lookup"><span data-stu-id="68068-128">Yes</span></span>      | <span data-ttu-id="68068-129">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="68068-129">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="68068-130">identyfikator sku</span><span class="sxs-lookup"><span data-stu-id="68068-130">sku-id</span></span>                 | <span data-ttu-id="68068-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="68068-131">string</span></span>   | <span data-ttu-id="68068-132">Tak</span><span class="sxs-lookup"><span data-stu-id="68068-132">Yes</span></span>      | <span data-ttu-id="68068-133">Ciąg identyfikujący sku.</span><span class="sxs-lookup"><span data-stu-id="68068-133">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="68068-134">kod kraju</span><span class="sxs-lookup"><span data-stu-id="68068-134">country-code</span></span>           | <span data-ttu-id="68068-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="68068-135">string</span></span>   | <span data-ttu-id="68068-136">Tak</span><span class="sxs-lookup"><span data-stu-id="68068-136">Yes</span></span>      | <span data-ttu-id="68068-137">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="68068-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="68068-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="68068-138">Request headers</span></span>

<span data-ttu-id="68068-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="68068-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="68068-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="68068-140">Request body</span></span>

<span data-ttu-id="68068-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="68068-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="68068-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="68068-142">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="68068-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="68068-143">REST response</span></span>

<span data-ttu-id="68068-144">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SKU.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="68068-144">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="68068-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68068-145">Response success and error codes</span></span>

<span data-ttu-id="68068-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="68068-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="68068-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="68068-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="68068-148">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="68068-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="68068-149">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="68068-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="68068-150">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="68068-150">HTTP Status Code</span></span>     | <span data-ttu-id="68068-151">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="68068-151">Error code</span></span>   | <span data-ttu-id="68068-152">Opis</span><span class="sxs-lookup"><span data-stu-id="68068-152">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68068-153">404</span><span class="sxs-lookup"><span data-stu-id="68068-153">404</span></span>                  | <span data-ttu-id="68068-154">400013</span><span class="sxs-lookup"><span data-stu-id="68068-154">400013</span></span>       | <span data-ttu-id="68068-155">Nie znaleziono produktu.</span><span class="sxs-lookup"><span data-stu-id="68068-155">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="68068-156">404</span><span class="sxs-lookup"><span data-stu-id="68068-156">404</span></span>                  | <span data-ttu-id="68068-157">400018</span><span class="sxs-lookup"><span data-stu-id="68068-157">400018</span></span>       | <span data-ttu-id="68068-158">Nie znaleziono sku.</span><span class="sxs-lookup"><span data-stu-id="68068-158">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="68068-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="68068-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```
