---
title: Pobierz dostępność według identyfikatora
description: Pobiera dostępność dla określonego produktu i jednostki SKU przy użyciu identyfikatora dostępności.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767714"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="cf7cf-103">Pobierz dostępność według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="cf7cf-103">Get the availability by ID</span></span>

<span data-ttu-id="cf7cf-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="cf7cf-104">**Applies To**</span></span>

- <span data-ttu-id="cf7cf-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="cf7cf-105">Partner Center</span></span>

<span data-ttu-id="cf7cf-106">Pobiera dostępność dla określonego produktu i jednostki SKU przy użyciu identyfikatora dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-106">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf7cf-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf7cf-107">Prerequisites</span></span>

- <span data-ttu-id="cf7cf-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cf7cf-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cf7cf-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cf7cf-110">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-110">A product ID.</span></span>

- <span data-ttu-id="cf7cf-111">IDENTYFIKATOR JEDNOSTKI SKU.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-111">A SKU ID.</span></span>

- <span data-ttu-id="cf7cf-112">Identyfikator dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-112">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="cf7cf-113">C\#</span><span class="sxs-lookup"><span data-stu-id="cf7cf-113">C\#</span></span>

<span data-ttu-id="cf7cf-114">Aby uzyskać szczegółowe informacje o konkretnej [dostępności](product-resources.md#availability), Zacznij od wykonania kroków z sekcji [pobieranie jednostki SKU według identyfikatora](get-a-sku-by-id.md) , aby uzyskać interfejs dla operacji określonej [jednostki SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="cf7cf-114">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="cf7cf-115">Z poziomu interfejsu uzyskanego wybierz właściwość **dostępność** , aby uzyskać interfejs z dostępnymi operacjami dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-115">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="cf7cf-116">Następnie Przekaż identyfikator dostępności do metody **ById ()** w celu uzyskania operacji dla tej konkretnej dostępności, a następnie Wywołaj metodę **Get ()** lub **GetAsync ()** , aby pobrać szczegóły dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-116">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="cf7cf-117">Java</span><span class="sxs-lookup"><span data-stu-id="cf7cf-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="cf7cf-118">Aby uzyskać szczegółowe informacje o konkretnej [dostępności](product-resources.md#availability), Zacznij od wykonania kroków z sekcji [pobieranie jednostki SKU według identyfikatora](get-a-sku-by-id.md) , aby uzyskać interfejs dla operacji określonej [jednostki SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="cf7cf-118">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="cf7cf-119">W interfejsie wynikającym wybierz funkcję **getAvailabilities** , aby uzyskać interfejs z dostępnymi operacjami dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-119">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="cf7cf-120">Następnie Przekaż identyfikator dostępności do funkcji **byId ()** w celu uzyskania operacji dla tej konkretnej dostępności, a następnie wywołaj funkcję **Get ()** , aby pobrać szczegóły dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-120">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="cf7cf-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf7cf-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="cf7cf-122">Aby uzyskać szczegółowe informacje o konkretnej [dostępności](product-resources.md#availability), wykonaj [**polecenie Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) i określ **Parametry AvailabilityId**, **CountryCode**, **ProductID** i **identyfikatora skuId** , aby pobrać szczegóły dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-122">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="cf7cf-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cf7cf-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cf7cf-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cf7cf-124">Request syntax</span></span>

| <span data-ttu-id="cf7cf-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="cf7cf-125">Method</span></span>  | <span data-ttu-id="cf7cf-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cf7cf-126">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf7cf-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cf7cf-127">**GET**</span></span> | <span data-ttu-id="cf7cf-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID}? Country = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cf7cf-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="cf7cf-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cf7cf-129">URI parameter</span></span>

<span data-ttu-id="cf7cf-130">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać określoną dostępność przy użyciu identyfikatora dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-130">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="cf7cf-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf7cf-131">Name</span></span>                   | <span data-ttu-id="cf7cf-132">Typ</span><span class="sxs-lookup"><span data-stu-id="cf7cf-132">Type</span></span>     | <span data-ttu-id="cf7cf-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cf7cf-133">Required</span></span> | <span data-ttu-id="cf7cf-134">Opis</span><span class="sxs-lookup"><span data-stu-id="cf7cf-134">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="cf7cf-135">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="cf7cf-135">product-id</span></span>             | <span data-ttu-id="cf7cf-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf7cf-136">string</span></span>   | <span data-ttu-id="cf7cf-137">Tak</span><span class="sxs-lookup"><span data-stu-id="cf7cf-137">Yes</span></span>      | <span data-ttu-id="cf7cf-138">Ciąg w formacie GUID, który identyfikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-138">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="cf7cf-139">jednostka SKU — identyfikator</span><span class="sxs-lookup"><span data-stu-id="cf7cf-139">sku-id</span></span>                 | <span data-ttu-id="cf7cf-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf7cf-140">string</span></span>   | <span data-ttu-id="cf7cf-141">Tak</span><span class="sxs-lookup"><span data-stu-id="cf7cf-141">Yes</span></span>      | <span data-ttu-id="cf7cf-142">Ciąg w formacie GUID, który identyfikuje jednostkę SKU.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-142">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="cf7cf-143">Identyfikator dostępności</span><span class="sxs-lookup"><span data-stu-id="cf7cf-143">availability-id</span></span>        | <span data-ttu-id="cf7cf-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf7cf-144">string</span></span>   | <span data-ttu-id="cf7cf-145">Tak</span><span class="sxs-lookup"><span data-stu-id="cf7cf-145">Yes</span></span>      | <span data-ttu-id="cf7cf-146">Ciąg w formacie GUID, który identyfikuje dostępność.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-146">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="cf7cf-147">Kraj — kod</span><span class="sxs-lookup"><span data-stu-id="cf7cf-147">country-code</span></span>           | <span data-ttu-id="cf7cf-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf7cf-148">string</span></span>   | <span data-ttu-id="cf7cf-149">Tak</span><span class="sxs-lookup"><span data-stu-id="cf7cf-149">Yes</span></span>      | <span data-ttu-id="cf7cf-150">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-150">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="cf7cf-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cf7cf-151">Request headers</span></span>

<span data-ttu-id="cf7cf-152">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cf7cf-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cf7cf-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cf7cf-153">Request body</span></span>

<span data-ttu-id="cf7cf-154">Brak.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cf7cf-155">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cf7cf-155">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="cf7cf-156">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cf7cf-156">REST response</span></span>

<span data-ttu-id="cf7cf-157">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [dostępności](product-resources.md#availability) .</span><span class="sxs-lookup"><span data-stu-id="cf7cf-157">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cf7cf-158">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf7cf-158">Response success and error codes</span></span>

<span data-ttu-id="cf7cf-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cf7cf-160">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cf7cf-161">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cf7cf-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="cf7cf-162">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="cf7cf-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="cf7cf-163">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="cf7cf-163">HTTP Status Code</span></span>     | <span data-ttu-id="cf7cf-164">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="cf7cf-164">Error code</span></span>   | <span data-ttu-id="cf7cf-165">Opis</span><span class="sxs-lookup"><span data-stu-id="cf7cf-165">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf7cf-166">404</span><span class="sxs-lookup"><span data-stu-id="cf7cf-166">404</span></span>                  | <span data-ttu-id="cf7cf-167">400013</span><span class="sxs-lookup"><span data-stu-id="cf7cf-167">400013</span></span>       | <span data-ttu-id="cf7cf-168">Produkt nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-168">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="cf7cf-169">404</span><span class="sxs-lookup"><span data-stu-id="cf7cf-169">404</span></span>                  | <span data-ttu-id="cf7cf-170">400018</span><span class="sxs-lookup"><span data-stu-id="cf7cf-170">400018</span></span>       | <span data-ttu-id="cf7cf-171">Nie znaleziono jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-171">Sku was not found.</span></span>                                                                                        |
| <span data-ttu-id="cf7cf-172">404</span><span class="sxs-lookup"><span data-stu-id="cf7cf-172">404</span></span>                  | <span data-ttu-id="cf7cf-173">400019</span><span class="sxs-lookup"><span data-stu-id="cf7cf-173">400019</span></span>       | <span data-ttu-id="cf7cf-174">Nie znaleziono dostępności.</span><span class="sxs-lookup"><span data-stu-id="cf7cf-174">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="cf7cf-175">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf7cf-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
