---
title: Pobieranie listy dostępności dla jednostki SKU (według kraju)
description: Jak uzyskać kolekcję dostępności dla określonego produktu i dla określonej skuku według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b29c005e74ad8a4da547a888b78e4599e74ebd02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874537"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="cac7b-103">Pobieranie listy dostępności dla jednostki SKU (według kraju)</span><span class="sxs-lookup"><span data-stu-id="cac7b-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="cac7b-104">W tym artykule opisano sposób pobierania kolekcji dostępności w określonym kraju dla określonego produktu i sku.</span><span class="sxs-lookup"><span data-stu-id="cac7b-104">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cac7b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cac7b-105">Prerequisites</span></span>

- <span data-ttu-id="cac7b-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cac7b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cac7b-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cac7b-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cac7b-108">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="cac7b-108">A product identifier.</span></span>

- <span data-ttu-id="cac7b-109">Identyfikator jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cac7b-109">A SKU identifier.</span></span>

- <span data-ttu-id="cac7b-110">Kraj.</span><span class="sxs-lookup"><span data-stu-id="cac7b-110">A country.</span></span>

## <a name="c"></a><span data-ttu-id="cac7b-111">C\#</span><span class="sxs-lookup"><span data-stu-id="cac7b-111">C\#</span></span>

<span data-ttu-id="cac7b-112">Aby uzyskać listę dostępności [dla](product-resources.md#availability) [SKU:](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="cac7b-112">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="cac7b-113">Wykonaj kroki opisane w [te tematu Get a SKU by ID (Uzyskiwanie SKU według identyfikatora),](get-a-sku-by-id.md) aby uzyskać interfejs dla operacji określonej sku.</span><span class="sxs-lookup"><span data-stu-id="cac7b-113">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="cac7b-114">W interfejsie SKU wybierz właściwość **Availabilities,** aby uzyskać interfejs z operacjami dostępności.</span><span class="sxs-lookup"><span data-stu-id="cac7b-114">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="cac7b-115">(Opcjonalnie) Użyj metody **ByTargetSegment(),** aby filtrować dostępność według segmentu docelowego.</span><span class="sxs-lookup"><span data-stu-id="cac7b-115">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="cac7b-116">Wywołaj **get()** lub **GetAsync(),** aby pobrać kolekcję dostępności dla tej sku.</span><span class="sxs-lookup"><span data-stu-id="cac7b-116">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a><span data-ttu-id="cac7b-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cac7b-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cac7b-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cac7b-118">Request syntax</span></span>

| <span data-ttu-id="cac7b-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="cac7b-119">Method</span></span>  | <span data-ttu-id="cac7b-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cac7b-120">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cac7b-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cac7b-121">**GET**</span></span> | <span data-ttu-id="cac7b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cac7b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="cac7b-123">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="cac7b-123">URI parameters</span></span>

<span data-ttu-id="cac7b-124">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę dostępności dla SKU.</span><span class="sxs-lookup"><span data-stu-id="cac7b-124">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="cac7b-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cac7b-125">Name</span></span>                   | <span data-ttu-id="cac7b-126">Typ</span><span class="sxs-lookup"><span data-stu-id="cac7b-126">Type</span></span>     | <span data-ttu-id="cac7b-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cac7b-127">Required</span></span> | <span data-ttu-id="cac7b-128">Opis</span><span class="sxs-lookup"><span data-stu-id="cac7b-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="cac7b-129">product-id</span><span class="sxs-lookup"><span data-stu-id="cac7b-129">product-id</span></span>             | <span data-ttu-id="cac7b-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="cac7b-130">string</span></span>   | <span data-ttu-id="cac7b-131">Tak</span><span class="sxs-lookup"><span data-stu-id="cac7b-131">Yes</span></span>      | <span data-ttu-id="cac7b-132">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="cac7b-132">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="cac7b-133">identyfikator sku</span><span class="sxs-lookup"><span data-stu-id="cac7b-133">sku-id</span></span>                 | <span data-ttu-id="cac7b-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="cac7b-134">string</span></span>   | <span data-ttu-id="cac7b-135">Tak</span><span class="sxs-lookup"><span data-stu-id="cac7b-135">Yes</span></span>      | <span data-ttu-id="cac7b-136">Ciąg identyfikujący sku.</span><span class="sxs-lookup"><span data-stu-id="cac7b-136">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="cac7b-137">kod kraju</span><span class="sxs-lookup"><span data-stu-id="cac7b-137">country-code</span></span>           | <span data-ttu-id="cac7b-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="cac7b-138">string</span></span>   | <span data-ttu-id="cac7b-139">Tak</span><span class="sxs-lookup"><span data-stu-id="cac7b-139">Yes</span></span>      | <span data-ttu-id="cac7b-140">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="cac7b-140">A country/region ID.</span></span>                                            |
| <span data-ttu-id="cac7b-141">segment docelowy</span><span class="sxs-lookup"><span data-stu-id="cac7b-141">target-segment</span></span>         | <span data-ttu-id="cac7b-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="cac7b-142">string</span></span>   | <span data-ttu-id="cac7b-143">Nie</span><span class="sxs-lookup"><span data-stu-id="cac7b-143">No</span></span>       | <span data-ttu-id="cac7b-144">Ciąg, który identyfikuje segment docelowy używany do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="cac7b-144">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="cac7b-145">reservationScope</span><span class="sxs-lookup"><span data-stu-id="cac7b-145">reservationScope</span></span> | <span data-ttu-id="cac7b-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="cac7b-146">string</span></span>   | <span data-ttu-id="cac7b-147">Nie</span><span class="sxs-lookup"><span data-stu-id="cac7b-147">No</span></span> | <span data-ttu-id="cac7b-148">Podczas wykonywania zapytania o listę dostępności dla wersji SKU rezerwacji platformy Azure określ, aby uzyskać listę dostępności, które mają zastosowanie `reservationScope=AzurePlan` do usługi AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="cac7b-148">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities that are applicable to AzurePlan.</span></span> <span data-ttu-id="cac7b-149">Wyklucz ten parametr, aby uzyskać listę dostępności, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="cac7b-149">Exclude this parameter to get a list of availabilities that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="cac7b-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cac7b-150">Request headers</span></span>

<span data-ttu-id="cac7b-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cac7b-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cac7b-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cac7b-152">Request body</span></span>

<span data-ttu-id="cac7b-153">Brak.</span><span class="sxs-lookup"><span data-stu-id="cac7b-153">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="cac7b-154">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="cac7b-154">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="cac7b-155">Dostępność dla SKU według kraju</span><span class="sxs-lookup"><span data-stu-id="cac7b-155">Availabilities for SKU by country</span></span>

<span data-ttu-id="cac7b-156">Postępuj zgodnie z tym przykładem, aby uzyskać listę dostępności dla danej sku według kraju:</span><span class="sxs-lookup"><span data-stu-id="cac7b-156">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="cac7b-157">Dostępność rezerwacji maszyn wirtualnych (plan platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="cac7b-157">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="cac7b-158">Postępuj zgodnie z tym przykładem, aby uzyskać listę dostępności według kraju dla wystąpień zarezerwowanych maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cac7b-158">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="cac7b-159">Ten przykład dotyczy jednostki SKU, które mają zastosowanie do planów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cac7b-159">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="cac7b-160">Dostępność rezerwacji maszyn wirtualnych dla Microsoft Azure subskrypcji (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="cac7b-160">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="cac7b-161">Postępuj zgodnie z tym przykładem, aby uzyskać listę dostępności według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji usługi Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="cac7b-161">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="cac7b-162">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cac7b-162">REST response</span></span>

<span data-ttu-id="cac7b-163">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [**zasobów**](product-resources.md#availability) dostępności.</span><span class="sxs-lookup"><span data-stu-id="cac7b-163">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cac7b-164">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cac7b-164">Response success and error codes</span></span>

<span data-ttu-id="cac7b-165">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="cac7b-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cac7b-166">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cac7b-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cac7b-167">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cac7b-167">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="cac7b-168">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="cac7b-168">This method returns the following error codes:</span></span>

| <span data-ttu-id="cac7b-169">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="cac7b-169">HTTP Status Code</span></span>     | <span data-ttu-id="cac7b-170">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="cac7b-170">Error code</span></span>   | <span data-ttu-id="cac7b-171">Opis</span><span class="sxs-lookup"><span data-stu-id="cac7b-171">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cac7b-172">403</span><span class="sxs-lookup"><span data-stu-id="cac7b-172">403</span></span>                  | <span data-ttu-id="cac7b-173">400030</span><span class="sxs-lookup"><span data-stu-id="cac7b-173">400030</span></span>       | <span data-ttu-id="cac7b-174">Dostęp do żądanego **obiektu targetSegment** nie jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="cac7b-174">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="cac7b-175">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cac7b-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
