---
title: Sprawdzanie spisu
description: Dowiedz się, jak używać Partner Center API do sprawdzania spisu określonego zestawu elementów katalogu. Możesz to zrobić, aby zidentyfikować produkty lub jednostki SKU klienta.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b982dbd7e5e10d454ef87a1e750546ea50eb8438
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974084"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="8b820-104">Sprawdzanie spisu elementów wykazu przy użyciu interfejsów API Partner Center API</span><span class="sxs-lookup"><span data-stu-id="8b820-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="8b820-105">Jak sprawdzić spis określonego zestawu elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="8b820-105">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b820-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b820-106">Prerequisites</span></span>

- <span data-ttu-id="8b820-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8b820-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8b820-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b820-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8b820-109">Co najmniej jeden identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="8b820-109">One or more product IDs.</span></span> <span data-ttu-id="8b820-110">Opcjonalnie można również określić identyfikatory SKU.</span><span class="sxs-lookup"><span data-stu-id="8b820-110">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="8b820-111">Wszelkie dodatkowe konteksty potrzebne do zweryfikowania spisu ku SKU przywołynych przez podane identyfikatory produktów/SKU.</span><span class="sxs-lookup"><span data-stu-id="8b820-111">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="8b820-112">Te wymagania mogą się różnić w zależności od [](product-resources.md#sku) typu produktu/SKU i można je określić na podstawie właściwości **InventoryVariables tej sku.**</span><span class="sxs-lookup"><span data-stu-id="8b820-112">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="8b820-113">C\#</span><span class="sxs-lookup"><span data-stu-id="8b820-113">C\#</span></span>

<span data-ttu-id="8b820-114">Aby sprawdzić spis, skonstruuj obiekt [InventoryCheckRequest](product-resources.md#inventorycheckrequest) przy użyciu obiektu [InventoryItem](product-resources.md#inventoryitem) dla każdego elementu do sprawdzenia.</span><span class="sxs-lookup"><span data-stu-id="8b820-114">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="8b820-115">Następnie użyj metody dostępu **IAggregatePartner.Extensions,** określ jej zakres w dół do opcji **Produkt,** a następnie wybierz kraj przy użyciu **metody ByCountry().**</span><span class="sxs-lookup"><span data-stu-id="8b820-115">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="8b820-116">Na koniec wywołaj **metodę CheckInventory()** przy użyciu obiektu **InventoryCheckRequest.**</span><span class="sxs-lookup"><span data-stu-id="8b820-116">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="8b820-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8b820-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8b820-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8b820-118">Request syntax</span></span>

| <span data-ttu-id="8b820-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="8b820-119">Method</span></span>   | <span data-ttu-id="8b820-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8b820-120">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b820-121">**Post**</span><span class="sxs-lookup"><span data-stu-id="8b820-121">**POST**</span></span> | <span data-ttu-id="8b820-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8b820-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="8b820-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8b820-123">URI parameter</span></span>

<span data-ttu-id="8b820-124">Użyj następującego parametru zapytania, aby sprawdzić spis.</span><span class="sxs-lookup"><span data-stu-id="8b820-124">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="8b820-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8b820-125">Name</span></span>                   | <span data-ttu-id="8b820-126">Typ</span><span class="sxs-lookup"><span data-stu-id="8b820-126">Type</span></span>     | <span data-ttu-id="8b820-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8b820-127">Required</span></span> | <span data-ttu-id="8b820-128">Opis</span><span class="sxs-lookup"><span data-stu-id="8b820-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="8b820-129">kod kraju</span><span class="sxs-lookup"><span data-stu-id="8b820-129">country-code</span></span>           | <span data-ttu-id="8b820-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="8b820-130">string</span></span>   | <span data-ttu-id="8b820-131">Tak</span><span class="sxs-lookup"><span data-stu-id="8b820-131">Yes</span></span>      | <span data-ttu-id="8b820-132">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="8b820-132">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="8b820-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8b820-133">Request headers</span></span>

<span data-ttu-id="8b820-134">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8b820-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8b820-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8b820-135">Request body</span></span>

<span data-ttu-id="8b820-136">Szczegóły żądania spisu składające się z zasobu [InventoryCheckRequest](product-resources.md#inventorycheckrequest) zawierającego co najmniej jeden [zasób InventoryItem.](product-resources.md#inventoryitem)</span><span class="sxs-lookup"><span data-stu-id="8b820-136">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="8b820-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8b820-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8b820-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8b820-138">REST response</span></span>

<span data-ttu-id="8b820-139">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję obiektów [InventoryItem](product-resources.md#inventoryitem) wypełnionych szczegółami ograniczeń, jeśli mają zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="8b820-139">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="8b820-140">Jeśli wejściowy element InventoryItem reprezentuje element, który nie można odnaleźć w wykazie, nie zostanie uwzględniony w kolekcji wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="8b820-140">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8b820-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b820-141">Response success and error codes</span></span>

<span data-ttu-id="8b820-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8b820-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8b820-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8b820-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8b820-144">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8b820-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8b820-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b820-145">Response example</span></span>

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
