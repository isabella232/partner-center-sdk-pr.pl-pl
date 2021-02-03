---
title: Sprawdź spis
description: Dowiedz się, jak używać interfejsów API usługi Partner Center do sprawdzania spisu określonego zestawu elementów katalogu. Można to zrobić, aby zidentyfikować produkty lub jednostki SKU klienta.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6921760abc0b95aff820467e84b3e8e9435731cd
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768598"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="45038-104">Sprawdzanie spisu elementów katalogu przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="45038-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="45038-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="45038-105">**Applies to:**</span></span>

- <span data-ttu-id="45038-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="45038-106">Partner Center</span></span>

<span data-ttu-id="45038-107">Sprawdzanie spisu określonego zestawu elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="45038-107">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45038-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="45038-108">Prerequisites</span></span>

- <span data-ttu-id="45038-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="45038-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="45038-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="45038-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="45038-111">Co najmniej jeden identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="45038-111">One or more product IDs.</span></span> <span data-ttu-id="45038-112">Opcjonalnie można również określić identyfikatory jednostek SKU.</span><span class="sxs-lookup"><span data-stu-id="45038-112">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="45038-113">Wszelkie dodatkowe konteksty potrzebne do zweryfikowania spisu jednostek SKU, do których odwołują się dostarczone identyfikatory produktu/jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="45038-113">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="45038-114">Te wymagania mogą być różne w zależności od typu produktu/jednostki SKU i można je określić na podstawie właściwości **InventoryVariables** [jednostki SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="45038-114">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="45038-115">C\#</span><span class="sxs-lookup"><span data-stu-id="45038-115">C\#</span></span>

<span data-ttu-id="45038-116">Aby sprawdzić spis, Utwórz obiekt [InventoryCheckRequest](product-resources.md#inventorycheckrequest) za pomocą obiektu [InventoryItem](product-resources.md#inventoryitem) dla każdego elementu, który ma zostać sprawdzony.</span><span class="sxs-lookup"><span data-stu-id="45038-116">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="45038-117">Następnie użyj metody dostępu **IAggregatePartner. Extensions** , określ zakres dla **produktu** , a następnie wybierz kraj przy użyciu metod **ByCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="45038-117">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="45038-118">Na koniec Wywołaj metodę **CheckInventory ()** za pomocą obiektu **InventoryCheckRequest** .</span><span class="sxs-lookup"><span data-stu-id="45038-118">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a><span data-ttu-id="45038-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="45038-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45038-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="45038-120">Request syntax</span></span>

| <span data-ttu-id="45038-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="45038-121">Method</span></span>   | <span data-ttu-id="45038-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="45038-122">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="45038-123">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="45038-123">**POST**</span></span> | <span data-ttu-id="45038-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Extensions/Product/checkInventory? Country = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="45038-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="45038-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="45038-125">URI parameter</span></span>

<span data-ttu-id="45038-126">Użyj następującego parametru zapytania, aby sprawdzić spis.</span><span class="sxs-lookup"><span data-stu-id="45038-126">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="45038-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="45038-127">Name</span></span>                   | <span data-ttu-id="45038-128">Typ</span><span class="sxs-lookup"><span data-stu-id="45038-128">Type</span></span>     | <span data-ttu-id="45038-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="45038-129">Required</span></span> | <span data-ttu-id="45038-130">Opis</span><span class="sxs-lookup"><span data-stu-id="45038-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="45038-131">Kraj — kod</span><span class="sxs-lookup"><span data-stu-id="45038-131">country-code</span></span>           | <span data-ttu-id="45038-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="45038-132">string</span></span>   | <span data-ttu-id="45038-133">Tak</span><span class="sxs-lookup"><span data-stu-id="45038-133">Yes</span></span>      | <span data-ttu-id="45038-134">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="45038-134">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="45038-135">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="45038-135">Request headers</span></span>

<span data-ttu-id="45038-136">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="45038-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="45038-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="45038-137">Request body</span></span>

<span data-ttu-id="45038-138">Szczegóły żądania spisu, składające się z zasobu [InventoryCheckRequest](product-resources.md#inventorycheckrequest) zawierającego co najmniej jeden zasób [InventoryItem](product-resources.md#inventoryitem) .</span><span class="sxs-lookup"><span data-stu-id="45038-138">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="45038-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="45038-139">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a><span data-ttu-id="45038-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="45038-140">REST response</span></span>

<span data-ttu-id="45038-141">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję obiektów [InventoryItem](product-resources.md#inventoryitem) z informacjami o ograniczeniach, jeśli ma zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="45038-141">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="45038-142">Jeśli InventoryItem wejściowy reprezentuje element, którego nie można znaleźć w wykazie, nie zostanie uwzględniony w kolekcji wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="45038-142">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45038-143">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="45038-143">Response success and error codes</span></span>

<span data-ttu-id="45038-144">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="45038-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45038-145">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="45038-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45038-146">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="45038-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="45038-147">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="45038-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
