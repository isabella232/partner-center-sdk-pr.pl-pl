---
title: Pobieranie jednostki SKU według identyfikatora
description: Pobiera jednostkę SKU dla określonego produktu przy użyciu określonego identyfikatora jednostki SKU.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 54ef72413d2d2b9e7154e82e4bbdd7427a79a2dd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767934"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="82413-103">Pobieranie jednostki SKU według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="82413-103">Get a SKU by ID</span></span>

<span data-ttu-id="82413-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="82413-104">**Applies To**</span></span>

- <span data-ttu-id="82413-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="82413-105">Partner Center</span></span>

<span data-ttu-id="82413-106">Pobiera jednostkę SKU dla określonego produktu przy użyciu określonego identyfikatora jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-106">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82413-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="82413-107">Prerequisites</span></span>

- <span data-ttu-id="82413-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="82413-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="82413-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="82413-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="82413-110">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="82413-110">A product ID.</span></span>

- <span data-ttu-id="82413-111">IDENTYFIKATOR JEDNOSTKI SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-111">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="82413-112">C\#</span><span class="sxs-lookup"><span data-stu-id="82413-112">C\#</span></span>

<span data-ttu-id="82413-113">Aby uzyskać szczegółowe informacje o określonej jednostce SKU, Zacznij od wykonania kroków w temacie [Uzyskiwanie produktu przez identyfikator](get-a-product-by-id.md) w celu uzyskania interfejsu dla operacji określonego produktu.</span><span class="sxs-lookup"><span data-stu-id="82413-113">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="82413-114">Z poziomu interfejsu uzyskanego wybierz właściwość **SKU** , aby uzyskać interfejs z dostępnymi operacjami dla jednostek SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-114">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="82413-115">Przekaż identyfikator jednostki SKU do metody **ById ()** , a następnie Wywołaj polecenie **Get ()** lub **GetAsync ()** , aby pobrać szczegóły jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-115">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="82413-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="82413-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="82413-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="82413-117">Request syntax</span></span>

| <span data-ttu-id="82413-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="82413-118">Method</span></span>  | <span data-ttu-id="82413-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="82413-119">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="82413-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="82413-120">**GET**</span></span> | <span data-ttu-id="82413-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs/{SKU-ID}? Country = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="82413-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="82413-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="82413-122">URI parameter</span></span>

<span data-ttu-id="82413-123">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać jednostkę SKU dla określonego produktu przy użyciu określonego identyfikatora jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-123">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="82413-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="82413-124">Name</span></span>                   | <span data-ttu-id="82413-125">Typ</span><span class="sxs-lookup"><span data-stu-id="82413-125">Type</span></span>     | <span data-ttu-id="82413-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="82413-126">Required</span></span> | <span data-ttu-id="82413-127">Opis</span><span class="sxs-lookup"><span data-stu-id="82413-127">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="82413-128">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="82413-128">product-id</span></span>             | <span data-ttu-id="82413-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="82413-129">string</span></span>   | <span data-ttu-id="82413-130">Tak</span><span class="sxs-lookup"><span data-stu-id="82413-130">Yes</span></span>      | <span data-ttu-id="82413-131">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="82413-131">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="82413-132">jednostka SKU — identyfikator</span><span class="sxs-lookup"><span data-stu-id="82413-132">sku-id</span></span>                 | <span data-ttu-id="82413-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="82413-133">string</span></span>   | <span data-ttu-id="82413-134">Tak</span><span class="sxs-lookup"><span data-stu-id="82413-134">Yes</span></span>      | <span data-ttu-id="82413-135">Ciąg, który identyfikuje jednostkę SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-135">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="82413-136">Kraj — kod</span><span class="sxs-lookup"><span data-stu-id="82413-136">country-code</span></span>           | <span data-ttu-id="82413-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="82413-137">string</span></span>   | <span data-ttu-id="82413-138">Tak</span><span class="sxs-lookup"><span data-stu-id="82413-138">Yes</span></span>      | <span data-ttu-id="82413-139">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="82413-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="82413-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="82413-140">Request headers</span></span>

<span data-ttu-id="82413-141">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="82413-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="82413-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="82413-142">Request body</span></span>

<span data-ttu-id="82413-143">Brak.</span><span class="sxs-lookup"><span data-stu-id="82413-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="82413-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="82413-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="82413-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="82413-145">REST response</span></span>

<span data-ttu-id="82413-146">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [jednostki SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="82413-146">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="82413-147">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="82413-147">Response success and error codes</span></span>

<span data-ttu-id="82413-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="82413-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="82413-149">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="82413-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="82413-150">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="82413-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="82413-151">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="82413-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="82413-152">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="82413-152">HTTP Status Code</span></span>     | <span data-ttu-id="82413-153">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="82413-153">Error code</span></span>   | <span data-ttu-id="82413-154">Opis</span><span class="sxs-lookup"><span data-stu-id="82413-154">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="82413-155">404</span><span class="sxs-lookup"><span data-stu-id="82413-155">404</span></span>                  | <span data-ttu-id="82413-156">400013</span><span class="sxs-lookup"><span data-stu-id="82413-156">400013</span></span>       | <span data-ttu-id="82413-157">Produkt nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="82413-157">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="82413-158">404</span><span class="sxs-lookup"><span data-stu-id="82413-158">404</span></span>                  | <span data-ttu-id="82413-159">400018</span><span class="sxs-lookup"><span data-stu-id="82413-159">400018</span></span>       | <span data-ttu-id="82413-160">Nie znaleziono jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="82413-160">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="82413-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="82413-161">Response example</span></span>

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
