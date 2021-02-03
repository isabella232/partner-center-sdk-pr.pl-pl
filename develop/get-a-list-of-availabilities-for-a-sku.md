---
title: Pobieranie listy dostępności dla jednostki SKU (według kraju)
description: Jak uzyskać zbiór podaży dla określonego produktu i jednostki SKU według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767957"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="cf75c-103">Pobieranie listy dostępności dla jednostki SKU (według kraju)</span><span class="sxs-lookup"><span data-stu-id="cf75c-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="cf75c-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="cf75c-104">**Applies to:**</span></span>

- <span data-ttu-id="cf75c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="cf75c-105">Partner Center</span></span>

<span data-ttu-id="cf75c-106">W tym artykule opisano, jak uzyskać zbiór podaży w określonym kraju dla określonego produktu i jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cf75c-106">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf75c-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf75c-107">Prerequisites</span></span>

- <span data-ttu-id="cf75c-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cf75c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cf75c-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cf75c-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cf75c-110">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="cf75c-110">A product identifier.</span></span>

- <span data-ttu-id="cf75c-111">Identyfikator jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cf75c-111">A SKU identifier.</span></span>

- <span data-ttu-id="cf75c-112">Kraj.</span><span class="sxs-lookup"><span data-stu-id="cf75c-112">A country.</span></span>

## <a name="c"></a><span data-ttu-id="cf75c-113">C\#</span><span class="sxs-lookup"><span data-stu-id="cf75c-113">C\#</span></span>

<span data-ttu-id="cf75c-114">Aby uzyskać listę [podaży](product-resources.md#availability) dla [jednostki SKU](product-resources.md#sku):</span><span class="sxs-lookup"><span data-stu-id="cf75c-114">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="cf75c-115">Postępuj zgodnie z instrukcjami w temacie [pobieranie jednostki SKU według identyfikatora](get-a-sku-by-id.md) , aby uzyskać interfejs dla operacji określonej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cf75c-115">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="cf75c-116">W interfejsie SKU wybierz właściwość **dostępność** , aby uzyskać interfejs z operacjami dla opcji dostępność.</span><span class="sxs-lookup"><span data-stu-id="cf75c-116">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="cf75c-117">Obowiązkowe Użyj metody **ByTargetSegment ()** , aby odfiltrować dostępność przez segment docelowy.</span><span class="sxs-lookup"><span data-stu-id="cf75c-117">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="cf75c-118">Wywoływanie **Get ()** lub **GetAsync ()** w celu pobrania kolekcji podaży dla tej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cf75c-118">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="cf75c-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cf75c-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cf75c-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cf75c-120">Request syntax</span></span>

| <span data-ttu-id="cf75c-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="cf75c-121">Method</span></span>  | <span data-ttu-id="cf75c-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cf75c-122">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf75c-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cf75c-123">**GET**</span></span> | <span data-ttu-id="cf75c-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities? Country = {Country-code} &targetSegment = {Target-segment} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cf75c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="cf75c-125">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="cf75c-125">URI parameters</span></span>

<span data-ttu-id="cf75c-126">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę dostępność dla jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="cf75c-126">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="cf75c-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf75c-127">Name</span></span>                   | <span data-ttu-id="cf75c-128">Typ</span><span class="sxs-lookup"><span data-stu-id="cf75c-128">Type</span></span>     | <span data-ttu-id="cf75c-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cf75c-129">Required</span></span> | <span data-ttu-id="cf75c-130">Opis</span><span class="sxs-lookup"><span data-stu-id="cf75c-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="cf75c-131">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="cf75c-131">product-id</span></span>             | <span data-ttu-id="cf75c-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf75c-132">string</span></span>   | <span data-ttu-id="cf75c-133">Tak</span><span class="sxs-lookup"><span data-stu-id="cf75c-133">Yes</span></span>      | <span data-ttu-id="cf75c-134">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="cf75c-134">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="cf75c-135">jednostka SKU — identyfikator</span><span class="sxs-lookup"><span data-stu-id="cf75c-135">sku-id</span></span>                 | <span data-ttu-id="cf75c-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf75c-136">string</span></span>   | <span data-ttu-id="cf75c-137">Tak</span><span class="sxs-lookup"><span data-stu-id="cf75c-137">Yes</span></span>      | <span data-ttu-id="cf75c-138">Ciąg, który identyfikuje jednostkę SKU.</span><span class="sxs-lookup"><span data-stu-id="cf75c-138">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="cf75c-139">Kraj — kod</span><span class="sxs-lookup"><span data-stu-id="cf75c-139">country-code</span></span>           | <span data-ttu-id="cf75c-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf75c-140">string</span></span>   | <span data-ttu-id="cf75c-141">Tak</span><span class="sxs-lookup"><span data-stu-id="cf75c-141">Yes</span></span>      | <span data-ttu-id="cf75c-142">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="cf75c-142">A country/region ID.</span></span>                                            |
| <span data-ttu-id="cf75c-143">segment docelowy</span><span class="sxs-lookup"><span data-stu-id="cf75c-143">target-segment</span></span>         | <span data-ttu-id="cf75c-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf75c-144">string</span></span>   | <span data-ttu-id="cf75c-145">Nie</span><span class="sxs-lookup"><span data-stu-id="cf75c-145">No</span></span>       | <span data-ttu-id="cf75c-146">Ciąg, który identyfikuje segment docelowy używany do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="cf75c-146">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="cf75c-147">reservationScope</span><span class="sxs-lookup"><span data-stu-id="cf75c-147">reservationScope</span></span> | <span data-ttu-id="cf75c-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="cf75c-148">string</span></span>   | <span data-ttu-id="cf75c-149">Nie</span><span class="sxs-lookup"><span data-stu-id="cf75c-149">No</span></span> | <span data-ttu-id="cf75c-150">Podczas wykonywania zapytania o listę dostępności dla jednostki SKU rezerwacji platformy Azure należy określić, `reservationScope=AzurePlan` Aby uzyskać listę dostępności, która ma zastosowanie do AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="cf75c-150">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities which are applicable to AzurePlan.</span></span> <span data-ttu-id="cf75c-151">Wyklucz ten parametr, aby uzyskać listę dostępności, która ma zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="cf75c-151">Exclude this parameter to get a list of availabilities which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="cf75c-152">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cf75c-152">Request headers</span></span>

<span data-ttu-id="cf75c-153">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cf75c-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cf75c-154">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cf75c-154">Request body</span></span>

<span data-ttu-id="cf75c-155">Brak.</span><span class="sxs-lookup"><span data-stu-id="cf75c-155">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="cf75c-156">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="cf75c-156">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="cf75c-157">Dostępność dla jednostki SKU według kraju</span><span class="sxs-lookup"><span data-stu-id="cf75c-157">Availabilities for SKU by country</span></span>

<span data-ttu-id="cf75c-158">Postępuj zgodnie z tym przykładem, aby uzyskać listę podaży dla danej jednostki SKU według kraju:</span><span class="sxs-lookup"><span data-stu-id="cf75c-158">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="cf75c-159">Dostępność na potrzeby rezerwacji maszyn wirtualnych (plan platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="cf75c-159">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="cf75c-160">Postępuj zgodnie z tym przykładem, aby uzyskać listę podaży według kraju dla jednostek SKU rezerwacji maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cf75c-160">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="cf75c-161">Ten przykład dotyczy jednostek SKU, które są stosowane do planów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cf75c-161">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="cf75c-162">Dostępność dla rezerwacji maszyn wirtualnych dla subskrypcji Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="cf75c-162">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="cf75c-163">Postępuj zgodnie z tym przykładem, aby uzyskać listę dostępności według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="cf75c-163">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="cf75c-164">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cf75c-164">REST response</span></span>

<span data-ttu-id="cf75c-165">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [**dostępności**](product-resources.md#availability) .</span><span class="sxs-lookup"><span data-stu-id="cf75c-165">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cf75c-166">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf75c-166">Response success and error codes</span></span>

<span data-ttu-id="cf75c-167">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="cf75c-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cf75c-168">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cf75c-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cf75c-169">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cf75c-169">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="cf75c-170">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="cf75c-170">This method returns the following error codes:</span></span>

| <span data-ttu-id="cf75c-171">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="cf75c-171">HTTP Status Code</span></span>     | <span data-ttu-id="cf75c-172">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="cf75c-172">Error code</span></span>   | <span data-ttu-id="cf75c-173">Opis</span><span class="sxs-lookup"><span data-stu-id="cf75c-173">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf75c-174">403</span><span class="sxs-lookup"><span data-stu-id="cf75c-174">403</span></span>                  | <span data-ttu-id="cf75c-175">400030</span><span class="sxs-lookup"><span data-stu-id="cf75c-175">400030</span></span>       | <span data-ttu-id="cf75c-176">Nie można uzyskać dostępu do żądanego **targetSegment** .</span><span class="sxs-lookup"><span data-stu-id="cf75c-176">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="cf75c-177">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf75c-177">Response example</span></span>

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
