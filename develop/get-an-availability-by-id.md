---
title: Uzyskiwanie dostępności według identyfikatora
description: Pobiera dostępność dla określonego produktu i sku przy użyciu identyfikatora dostępności.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760202"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="31bb0-103">Uzyskiwanie dostępności według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="31bb0-103">Get the availability by ID</span></span>

<span data-ttu-id="31bb0-104">Pobiera dostępność dla określonego produktu i sku przy użyciu identyfikatora dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-104">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31bb0-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="31bb0-105">Prerequisites</span></span>

- <span data-ttu-id="31bb0-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="31bb0-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="31bb0-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31bb0-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="31bb0-108">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="31bb0-108">A product ID.</span></span>

- <span data-ttu-id="31bb0-109">Identyfikator SKU.</span><span class="sxs-lookup"><span data-stu-id="31bb0-109">A SKU ID.</span></span>

- <span data-ttu-id="31bb0-110">Identyfikator dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-110">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="31bb0-111">C\#</span><span class="sxs-lookup"><span data-stu-id="31bb0-111">C\#</span></span>

<span data-ttu-id="31bb0-112">Aby uzyskać szczegółowe informacje o określonej [dostępności,](product-resources.md#availability)zacznij od kroków z artykułu Get [a SKU by ID (Uzyskiwanie sku za](get-a-sku-by-id.md) pomocą identyfikatora) w celu uzyskania interfejsu dla operacji [określonej sku.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="31bb0-112">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="31bb0-113">Z wynikowego interfejsu wybierz właściwość **Availabilities,** aby uzyskać interfejs z dostępnymi operacjami dla właściwości Availabilities.</span><span class="sxs-lookup"><span data-stu-id="31bb0-113">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="31bb0-114">Następnie przekaż identyfikator dostępności do metody **ById(),** aby pobrać operacje dla tej określonej dostępności, a następnie wywołaj metodę **Get()** lub **GetAsync(),** aby pobrać szczegóły dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-114">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="31bb0-115">Java</span><span class="sxs-lookup"><span data-stu-id="31bb0-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="31bb0-116">Aby uzyskać szczegółowe informacje o określonej [dostępności,](product-resources.md#availability)zacznij od kroków z artykułu Get [a SKU by ID (Uzyskiwanie sku za](get-a-sku-by-id.md) pomocą identyfikatora) w celu uzyskania interfejsu dla operacji [określonej sku.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="31bb0-116">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="31bb0-117">Z wynikowego interfejsu wybierz funkcję **getAvailabilities,** aby uzyskać interfejs z dostępnymi operacjami dla opcji Dostępność.</span><span class="sxs-lookup"><span data-stu-id="31bb0-117">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="31bb0-118">Następnie przekaż identyfikator dostępności do funkcji **byId(),** aby pobrać operacje dla tej określonej dostępności, a następnie wywołaj funkcję **get(),** aby pobrać szczegóły dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-118">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="31bb0-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31bb0-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="31bb0-120">Aby uzyskać szczegółowe informacje o [określonej](product-resources.md#availability)dostępności, wykonaj polecenie [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) i określ parametry **AvailabilityId**, **CountryCode,** **ProductId** i **SkuId,** aby pobrać szczegóły dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-120">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="31bb0-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="31bb0-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="31bb0-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="31bb0-122">Request syntax</span></span>

| <span data-ttu-id="31bb0-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="31bb0-123">Method</span></span>  | <span data-ttu-id="31bb0-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="31bb0-124">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="31bb0-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="31bb0-125">**GET**</span></span> | <span data-ttu-id="31bb0-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{identyfikator-produktu}/skus/{sku-id}/availabilities/{identyfikator-dostępności}?country={kod-kraju} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="31bb0-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="31bb0-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="31bb0-127">URI parameter</span></span>

<span data-ttu-id="31bb0-128">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać określoną dostępność przy użyciu identyfikatora dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-128">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="31bb0-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="31bb0-129">Name</span></span>                   | <span data-ttu-id="31bb0-130">Typ</span><span class="sxs-lookup"><span data-stu-id="31bb0-130">Type</span></span>     | <span data-ttu-id="31bb0-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="31bb0-131">Required</span></span> | <span data-ttu-id="31bb0-132">Opis</span><span class="sxs-lookup"><span data-stu-id="31bb0-132">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="31bb0-133">identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="31bb0-133">product-id</span></span>             | <span data-ttu-id="31bb0-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="31bb0-134">string</span></span>   | <span data-ttu-id="31bb0-135">Tak</span><span class="sxs-lookup"><span data-stu-id="31bb0-135">Yes</span></span>      | <span data-ttu-id="31bb0-136">Ciąg w formacie identyfikatora GUID, który identyfikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="31bb0-136">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="31bb0-137">identyfikator sku</span><span class="sxs-lookup"><span data-stu-id="31bb0-137">sku-id</span></span>                 | <span data-ttu-id="31bb0-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="31bb0-138">string</span></span>   | <span data-ttu-id="31bb0-139">Tak</span><span class="sxs-lookup"><span data-stu-id="31bb0-139">Yes</span></span>      | <span data-ttu-id="31bb0-140">Ciąg w formacie identyfikatora GUID, który identyfikuje sku.</span><span class="sxs-lookup"><span data-stu-id="31bb0-140">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="31bb0-141">identyfikator dostępności</span><span class="sxs-lookup"><span data-stu-id="31bb0-141">availability-id</span></span>        | <span data-ttu-id="31bb0-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="31bb0-142">string</span></span>   | <span data-ttu-id="31bb0-143">Tak</span><span class="sxs-lookup"><span data-stu-id="31bb0-143">Yes</span></span>      | <span data-ttu-id="31bb0-144">Ciąg w formacie identyfikatora GUID, który identyfikuje dostępność.</span><span class="sxs-lookup"><span data-stu-id="31bb0-144">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="31bb0-145">kod kraju</span><span class="sxs-lookup"><span data-stu-id="31bb0-145">country-code</span></span>           | <span data-ttu-id="31bb0-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="31bb0-146">string</span></span>   | <span data-ttu-id="31bb0-147">Tak</span><span class="sxs-lookup"><span data-stu-id="31bb0-147">Yes</span></span>      | <span data-ttu-id="31bb0-148">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="31bb0-148">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="31bb0-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="31bb0-149">Request headers</span></span>

<span data-ttu-id="31bb0-150">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="31bb0-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="31bb0-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="31bb0-151">Request body</span></span>

<span data-ttu-id="31bb0-152">Brak.</span><span class="sxs-lookup"><span data-stu-id="31bb0-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="31bb0-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="31bb0-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="31bb0-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="31bb0-154">REST response</span></span>

<span data-ttu-id="31bb0-155">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób Availability.](product-resources.md#availability)</span><span class="sxs-lookup"><span data-stu-id="31bb0-155">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="31bb0-156">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="31bb0-156">Response success and error codes</span></span>

<span data-ttu-id="31bb0-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="31bb0-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="31bb0-158">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="31bb0-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="31bb0-159">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="31bb0-159">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="31bb0-160">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="31bb0-160">This method returns the following error codes:</span></span>

| <span data-ttu-id="31bb0-161">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="31bb0-161">HTTP Status Code</span></span>     | <span data-ttu-id="31bb0-162">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="31bb0-162">Error code</span></span>   | <span data-ttu-id="31bb0-163">Opis</span><span class="sxs-lookup"><span data-stu-id="31bb0-163">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="31bb0-164">404</span><span class="sxs-lookup"><span data-stu-id="31bb0-164">404</span></span>                  | <span data-ttu-id="31bb0-165">400013</span><span class="sxs-lookup"><span data-stu-id="31bb0-165">400013</span></span>       | <span data-ttu-id="31bb0-166">Nie znaleziono produktu.</span><span class="sxs-lookup"><span data-stu-id="31bb0-166">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="31bb0-167">404</span><span class="sxs-lookup"><span data-stu-id="31bb0-167">404</span></span>                  | <span data-ttu-id="31bb0-168">400018</span><span class="sxs-lookup"><span data-stu-id="31bb0-168">400018</span></span>       | <span data-ttu-id="31bb0-169">Nie znaleziono sku.</span><span class="sxs-lookup"><span data-stu-id="31bb0-169">SKU was not found.</span></span>                                                                                        |
| <span data-ttu-id="31bb0-170">404</span><span class="sxs-lookup"><span data-stu-id="31bb0-170">404</span></span>                  | <span data-ttu-id="31bb0-171">400019</span><span class="sxs-lookup"><span data-stu-id="31bb0-171">400019</span></span>       | <span data-ttu-id="31bb0-172">Nie znaleziono dostępności.</span><span class="sxs-lookup"><span data-stu-id="31bb0-172">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="31bb0-173">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="31bb0-173">Response example</span></span>

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
