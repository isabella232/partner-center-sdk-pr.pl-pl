---
title: Pobieranie listy jednostek SKU dla produktu (według kraju)
description: Możesz uzyskać i przefiltrować kolekcję jednostek SKU według kraju dla produktu przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767937"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="9240b-103">Pobieranie listy jednostek SKU dla produktu (według kraju)</span><span class="sxs-lookup"><span data-stu-id="9240b-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="9240b-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="9240b-104">**Applies to:**</span></span>

- <span data-ttu-id="9240b-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9240b-105">Partner Center</span></span>

<span data-ttu-id="9240b-106">Możesz uzyskać kolekcję jednostek SKU dostępnych w danym kraju dla określonego produktu przy użyciu interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="9240b-106">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9240b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9240b-107">Prerequisites</span></span>

- <span data-ttu-id="9240b-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9240b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9240b-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9240b-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9240b-110">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="9240b-110">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="9240b-111">C\#</span><span class="sxs-lookup"><span data-stu-id="9240b-111">C\#</span></span>

<span data-ttu-id="9240b-112">Aby uzyskać listę jednostek SKU produktu:</span><span class="sxs-lookup"><span data-stu-id="9240b-112">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="9240b-113">Pobierz interfejs dla operacji określonego produktu, wykonując kroki opisane w temacie [Uzyskiwanie produktu według identyfikatora](get-a-product-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="9240b-113">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="9240b-114">Z poziomu interfejsu wybierz właściwość **SKU** , aby uzyskać interfejs z dostępnymi operacjami dla jednostek SKU.</span><span class="sxs-lookup"><span data-stu-id="9240b-114">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="9240b-115">Wywołaj metodę **Get ()** lub **GetAsync ()** , aby pobrać kolekcję dostępnych jednostek SKU dla produktu.</span><span class="sxs-lookup"><span data-stu-id="9240b-115">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="9240b-116">Obowiązkowe Wybierz zakres rezerwacji przy użyciu metody **ByReservationScope ()** .</span><span class="sxs-lookup"><span data-stu-id="9240b-116">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="9240b-117">Obowiązkowe Użyj metody **ByTargetSegment ()** , aby odfiltrować jednostki SKU według segmentu docelowego przed wywołaniem metody **Get ()** lub **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="9240b-117">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="9240b-118">Java</span><span class="sxs-lookup"><span data-stu-id="9240b-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9240b-119">Aby uzyskać listę jednostek SKU produktu:</span><span class="sxs-lookup"><span data-stu-id="9240b-119">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="9240b-120">Pobierz interfejs dla operacji określonego produktu, wykonując kroki opisane w temacie [Uzyskiwanie produktu według identyfikatora](get-a-product-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="9240b-120">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="9240b-121">Z poziomu interfejsu wybierz funkcję **Getskus** , aby uzyskać interfejs z dostępnymi operacjami dla jednostek SKU.</span><span class="sxs-lookup"><span data-stu-id="9240b-121">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="9240b-122">Wywołaj funkcję **Get ()** , aby pobrać kolekcję dostępnych jednostek SKU dla produktu.</span><span class="sxs-lookup"><span data-stu-id="9240b-122">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="9240b-123">Obowiązkowe Użyj funkcji **byTargetSegment ()** , aby odfiltrować jednostki SKU według segmentu docelowego przed wywołaniem funkcji **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="9240b-123">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a><span data-ttu-id="9240b-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9240b-124">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9240b-125">Aby uzyskać listę jednostek SKU produktu:</span><span class="sxs-lookup"><span data-stu-id="9240b-125">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="9240b-126">Wykonaj polecenie [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) .</span><span class="sxs-lookup"><span data-stu-id="9240b-126">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="9240b-127">Obowiązkowe Określ parametr **segmentu** , aby przefiltrować jednostki SKU według segmentu docelowego.</span><span class="sxs-lookup"><span data-stu-id="9240b-127">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="9240b-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9240b-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9240b-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9240b-129">Request syntax</span></span>

| <span data-ttu-id="9240b-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="9240b-130">Method</span></span>  | <span data-ttu-id="9240b-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9240b-131">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9240b-132">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9240b-132">**GET**</span></span> | <span data-ttu-id="9240b-133">[*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs? Country = {Country-code} &targetSegment = {Target-segment} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9240b-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="9240b-134">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="9240b-134">URI parameters</span></span>

<span data-ttu-id="9240b-135">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę jednostek SKU dla produktu.</span><span class="sxs-lookup"><span data-stu-id="9240b-135">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="9240b-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9240b-136">Name</span></span>                   | <span data-ttu-id="9240b-137">Typ</span><span class="sxs-lookup"><span data-stu-id="9240b-137">Type</span></span>     | <span data-ttu-id="9240b-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9240b-138">Required</span></span> | <span data-ttu-id="9240b-139">Opis</span><span class="sxs-lookup"><span data-stu-id="9240b-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="9240b-140">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="9240b-140">product-id</span></span>             | <span data-ttu-id="9240b-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="9240b-141">string</span></span>   | <span data-ttu-id="9240b-142">Tak</span><span class="sxs-lookup"><span data-stu-id="9240b-142">Yes</span></span>      | <span data-ttu-id="9240b-143">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="9240b-143">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="9240b-144">Kraj — kod</span><span class="sxs-lookup"><span data-stu-id="9240b-144">country-code</span></span>           | <span data-ttu-id="9240b-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="9240b-145">string</span></span>   | <span data-ttu-id="9240b-146">Tak</span><span class="sxs-lookup"><span data-stu-id="9240b-146">Yes</span></span>      | <span data-ttu-id="9240b-147">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="9240b-147">A country/region ID.</span></span>                                            |
| <span data-ttu-id="9240b-148">segment docelowy</span><span class="sxs-lookup"><span data-stu-id="9240b-148">target-segment</span></span>         | <span data-ttu-id="9240b-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="9240b-149">string</span></span>   | <span data-ttu-id="9240b-150">Nie</span><span class="sxs-lookup"><span data-stu-id="9240b-150">No</span></span>       | <span data-ttu-id="9240b-151">Ciąg, który identyfikuje segment docelowy używany do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="9240b-151">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="9240b-152">reservationScope</span><span class="sxs-lookup"><span data-stu-id="9240b-152">reservationScope</span></span> | <span data-ttu-id="9240b-153">ciąg</span><span class="sxs-lookup"><span data-stu-id="9240b-153">string</span></span>   | <span data-ttu-id="9240b-154">Nie</span><span class="sxs-lookup"><span data-stu-id="9240b-154">No</span></span> | <span data-ttu-id="9240b-155">Podczas wykonywania zapytania o listę jednostek SKU dla produktu Azure Reservation należy określić, `reservationScope=AzurePlan` Aby uzyskać listę jednostek SKU, które mają zastosowanie do AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="9240b-155">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs which are applicable to AzurePlan.</span></span> <span data-ttu-id="9240b-156">Wyklucz ten parametr, aby uzyskać listę jednostek SKU dla produktów rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="9240b-156">Exclude this parameter to get a list of SKUs for an Azure Reservation products which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="9240b-157">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9240b-157">Request headers</span></span>

<span data-ttu-id="9240b-158">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9240b-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9240b-159">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9240b-159">Request body</span></span>

<span data-ttu-id="9240b-160">Brak.</span><span class="sxs-lookup"><span data-stu-id="9240b-160">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="9240b-161">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="9240b-161">Request examples</span></span>

<span data-ttu-id="9240b-162">Pobierz listę jednostek SKU dla danego produktu:</span><span class="sxs-lookup"><span data-stu-id="9240b-162">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="9240b-163">Pobierz listę jednostek SKU dla produktu rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9240b-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="9240b-164">Uwzględnij tylko jednostki SKU, które mają zastosowanie do planów platformy Azure, a nie Microsoft Azure (MS-AZR-0145P):</span><span class="sxs-lookup"><span data-stu-id="9240b-164">Only include the SKUs which are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="9240b-165">Pobierz listę jednostek SKU dla produktu rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9240b-165">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="9240b-166">Uwzględnij tylko jednostki SKU, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P), a nie planów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="9240b-166">Only include the SKUs which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="9240b-167">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9240b-167">REST response</span></span>

<span data-ttu-id="9240b-168">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [jednostki SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="9240b-168">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9240b-169">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9240b-169">Response success and error codes</span></span>

<span data-ttu-id="9240b-170">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9240b-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9240b-171">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9240b-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9240b-172">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9240b-172">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="9240b-173">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="9240b-173">This method returns the following error codes:</span></span>

| <span data-ttu-id="9240b-174">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="9240b-174">HTTP Status Code</span></span>     | <span data-ttu-id="9240b-175">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="9240b-175">Error code</span></span>   | <span data-ttu-id="9240b-176">Opis</span><span class="sxs-lookup"><span data-stu-id="9240b-176">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9240b-177">403</span><span class="sxs-lookup"><span data-stu-id="9240b-177">403</span></span>                  | <span data-ttu-id="9240b-178">400030</span><span class="sxs-lookup"><span data-stu-id="9240b-178">400030</span></span>       | <span data-ttu-id="9240b-179">Nie można uzyskać dostępu do żądanego targetSegment.</span><span class="sxs-lookup"><span data-stu-id="9240b-179">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="9240b-180">404</span><span class="sxs-lookup"><span data-stu-id="9240b-180">404</span></span>                  | <span data-ttu-id="9240b-181">400013</span><span class="sxs-lookup"><span data-stu-id="9240b-181">400013</span></span>       | <span data-ttu-id="9240b-182">Nie znaleziono produktu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="9240b-182">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="9240b-183">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9240b-183">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
