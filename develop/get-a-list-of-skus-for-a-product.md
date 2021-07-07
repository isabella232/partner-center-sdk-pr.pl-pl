---
title: Pobieranie listy jednostek SKU dla produktu (według kraju)
description: Możesz pobrać i filtrować kolekcję jednostki SKU według kraju dla produktu przy użyciu Partner Center API.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 27a2391a22a9439461fb53764b87c1cafa68b875
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873891"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="dec8e-103">Pobieranie listy jednostek SKU dla produktu (według kraju)</span><span class="sxs-lookup"><span data-stu-id="dec8e-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="dec8e-104">Możesz uzyskać kolekcję dostępnych w danym kraju jednostki SKU dla określonego produktu przy użyciu Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="dec8e-104">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dec8e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dec8e-105">Prerequisites</span></span>

- <span data-ttu-id="dec8e-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="dec8e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dec8e-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dec8e-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dec8e-108">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="dec8e-108">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="dec8e-109">C\#</span><span class="sxs-lookup"><span data-stu-id="dec8e-109">C\#</span></span>

<span data-ttu-id="dec8e-110">Aby uzyskać listę jednostki SKU dla produktu:</span><span class="sxs-lookup"><span data-stu-id="dec8e-110">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="dec8e-111">Aby uzyskać interfejs dla operacji określonego produktu, należy wykonać kroki opisane w te tematu [Get a product by ID (Uzyskiwanie produktu według identyfikatora).](get-a-product-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="dec8e-111">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="dec8e-112">Z interfejsu wybierz właściwość **Jednostki SKU,** aby uzyskać interfejs z dostępnymi operacjami dla jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="dec8e-112">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="dec8e-113">Wywołaj **metodę Get()** **lub GetAsync(),** aby pobrać kolekcję dostępnych jednostki SKU dla produktu.</span><span class="sxs-lookup"><span data-stu-id="dec8e-113">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="dec8e-114">(Opcjonalnie) Wybierz zakres rezerwacji przy użyciu **metody ByReservationScope().**</span><span class="sxs-lookup"><span data-stu-id="dec8e-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="dec8e-115">(Opcjonalnie) Użyj metody **ByTargetSegment(),** aby filtrować jednostki SKU według segmentu docelowego przed wywołaniem metody **Get()** lub **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="dec8e-115">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

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

## <a name="java"></a><span data-ttu-id="dec8e-116">Java</span><span class="sxs-lookup"><span data-stu-id="dec8e-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="dec8e-117">Aby uzyskać listę jednostki SKU dla produktu:</span><span class="sxs-lookup"><span data-stu-id="dec8e-117">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="dec8e-118">Aby uzyskać interfejs dla operacji określonego produktu, należy wykonać kroki opisane w te tematu [Get a product by ID (Uzyskiwanie produktu według identyfikatora).](get-a-product-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="dec8e-118">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="dec8e-119">W interfejsie wybierz funkcję **getSkus,** aby uzyskać interfejs z dostępnymi operacjami dla jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="dec8e-119">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="dec8e-120">Wywołaj **funkcję get(),** aby pobrać kolekcję dostępnych jednostki SKU dla produktu.</span><span class="sxs-lookup"><span data-stu-id="dec8e-120">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="dec8e-121">(Opcjonalnie) Użyj funkcji **byTargetSegment(),** aby filtrować jednostki SKU według segmentu docelowego przed wywołaniem **funkcji get().**</span><span class="sxs-lookup"><span data-stu-id="dec8e-121">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="dec8e-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dec8e-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="dec8e-123">Aby uzyskać listę jednostki SKU dla produktu:</span><span class="sxs-lookup"><span data-stu-id="dec8e-123">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="dec8e-124">Wykonaj polecenie [**Get-PartnerProductSku.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md)</span><span class="sxs-lookup"><span data-stu-id="dec8e-124">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="dec8e-125">(Opcjonalnie) Określ parametr **Segment,** aby filtrować jednostki SKU według segmentu docelowego.</span><span class="sxs-lookup"><span data-stu-id="dec8e-125">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="dec8e-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="dec8e-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dec8e-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="dec8e-127">Request syntax</span></span>

| <span data-ttu-id="dec8e-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="dec8e-128">Method</span></span>  | <span data-ttu-id="dec8e-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="dec8e-129">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dec8e-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="dec8e-130">**GET**</span></span> | <span data-ttu-id="dec8e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dec8e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="dec8e-132">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="dec8e-132">URI parameters</span></span>

<span data-ttu-id="dec8e-133">Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę jednostki SKU dla produktu.</span><span class="sxs-lookup"><span data-stu-id="dec8e-133">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="dec8e-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dec8e-134">Name</span></span>                   | <span data-ttu-id="dec8e-135">Typ</span><span class="sxs-lookup"><span data-stu-id="dec8e-135">Type</span></span>     | <span data-ttu-id="dec8e-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dec8e-136">Required</span></span> | <span data-ttu-id="dec8e-137">Opis</span><span class="sxs-lookup"><span data-stu-id="dec8e-137">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="dec8e-138">product-id</span><span class="sxs-lookup"><span data-stu-id="dec8e-138">product-id</span></span>             | <span data-ttu-id="dec8e-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="dec8e-139">string</span></span>   | <span data-ttu-id="dec8e-140">Tak</span><span class="sxs-lookup"><span data-stu-id="dec8e-140">Yes</span></span>      | <span data-ttu-id="dec8e-141">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="dec8e-141">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="dec8e-142">kod kraju</span><span class="sxs-lookup"><span data-stu-id="dec8e-142">country-code</span></span>           | <span data-ttu-id="dec8e-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="dec8e-143">string</span></span>   | <span data-ttu-id="dec8e-144">Tak</span><span class="sxs-lookup"><span data-stu-id="dec8e-144">Yes</span></span>      | <span data-ttu-id="dec8e-145">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="dec8e-145">A country/region ID.</span></span>                                            |
| <span data-ttu-id="dec8e-146">segment docelowy</span><span class="sxs-lookup"><span data-stu-id="dec8e-146">target-segment</span></span>         | <span data-ttu-id="dec8e-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="dec8e-147">string</span></span>   | <span data-ttu-id="dec8e-148">Nie</span><span class="sxs-lookup"><span data-stu-id="dec8e-148">No</span></span>       | <span data-ttu-id="dec8e-149">Ciąg, który identyfikuje segment docelowy używany do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="dec8e-149">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="dec8e-150">reservationScope</span><span class="sxs-lookup"><span data-stu-id="dec8e-150">reservationScope</span></span> | <span data-ttu-id="dec8e-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="dec8e-151">string</span></span>   | <span data-ttu-id="dec8e-152">Nie</span><span class="sxs-lookup"><span data-stu-id="dec8e-152">No</span></span> | <span data-ttu-id="dec8e-153">Podczas wykonywania zapytania o listę jednostki SKU dla produktu rezerwacji platformy Azure określ, aby uzyskać listę jednostki SKU, które `reservationScope=AzurePlan` mają zastosowanie do usługi AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="dec8e-153">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs that are applicable to AzurePlan.</span></span> <span data-ttu-id="dec8e-154">Wyklucz ten parametr, aby uzyskać listę jednostki SKU dla produktów rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="dec8e-154">Exclude this parameter to get a list of SKUs for Azure Reservation products that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="dec8e-155">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="dec8e-155">Request headers</span></span>

<span data-ttu-id="dec8e-156">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dec8e-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dec8e-157">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="dec8e-157">Request body</span></span>

<span data-ttu-id="dec8e-158">Brak.</span><span class="sxs-lookup"><span data-stu-id="dec8e-158">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="dec8e-159">Przykłady żądań</span><span class="sxs-lookup"><span data-stu-id="dec8e-159">Request examples</span></span>

<span data-ttu-id="dec8e-160">Pobierz listę jednostki SKU dla danego produktu:</span><span class="sxs-lookup"><span data-stu-id="dec8e-160">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="dec8e-161">Pobierz listę jednostki SKU dla produktu rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dec8e-161">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="dec8e-162">Uwzględnij tylko jednostki SKU, które mają zastosowanie do planów platformy Azure, Microsoft Azure subskrypcji (MS-AZR-0145P):</span><span class="sxs-lookup"><span data-stu-id="dec8e-162">Only include the SKUs that are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="dec8e-163">Pobierz listę jednostki SKU dla produktu rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dec8e-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="dec8e-164">Uwzględnij tylko jednostki SKU, które mają zastosowanie Microsoft Azure subskrypcji (MS-AZR-0145P), a nie planów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="dec8e-164">Only include the SKUs that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="dec8e-165">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="dec8e-165">REST response</span></span>

<span data-ttu-id="dec8e-166">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [SKU.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="dec8e-166">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dec8e-167">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dec8e-167">Response success and error codes</span></span>

<span data-ttu-id="dec8e-168">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="dec8e-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dec8e-169">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="dec8e-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dec8e-170">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dec8e-170">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="dec8e-171">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="dec8e-171">This method returns the following error codes:</span></span>

| <span data-ttu-id="dec8e-172">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="dec8e-172">HTTP Status Code</span></span>     | <span data-ttu-id="dec8e-173">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="dec8e-173">Error code</span></span>   | <span data-ttu-id="dec8e-174">Opis</span><span class="sxs-lookup"><span data-stu-id="dec8e-174">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dec8e-175">403</span><span class="sxs-lookup"><span data-stu-id="dec8e-175">403</span></span>                  | <span data-ttu-id="dec8e-176">400030</span><span class="sxs-lookup"><span data-stu-id="dec8e-176">400030</span></span>       | <span data-ttu-id="dec8e-177">Dostęp do żądanego obiektu targetSegment nie jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="dec8e-177">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="dec8e-178">404</span><span class="sxs-lookup"><span data-stu-id="dec8e-178">404</span></span>                  | <span data-ttu-id="dec8e-179">400013</span><span class="sxs-lookup"><span data-stu-id="dec8e-179">400013</span></span>       | <span data-ttu-id="dec8e-180">Nie znaleziono produktu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="dec8e-180">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="dec8e-181">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dec8e-181">Response example</span></span>

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
