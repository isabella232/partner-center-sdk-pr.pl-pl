---
title: Pobieranie produktu według identyfikatora
description: Pobiera określony zasób produktu przy użyciu identyfikatora produktu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 769a4307dc3cebdc7ebbdcf51d9f2b67a9f4b7c2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874027"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="a5d86-103">Pobieranie produktu według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="a5d86-103">Get a product by ID</span></span>

<span data-ttu-id="a5d86-104">Pobiera określony zasób produktu przy użyciu identyfikatora produktu.</span><span class="sxs-lookup"><span data-stu-id="a5d86-104">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5d86-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a5d86-105">Prerequisites</span></span>

- <span data-ttu-id="a5d86-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a5d86-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a5d86-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a5d86-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a5d86-108">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="a5d86-108">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="a5d86-109">C\#</span><span class="sxs-lookup"><span data-stu-id="a5d86-109">C\#</span></span>

<span data-ttu-id="a5d86-110">Aby znaleźć konkretny produkt według identyfikatora, użyj kolekcji **IAggregatePartner.Products,** wybierz kraj przy użyciu metody **ByCountry(),** a następnie wywołaj metodę **ById().**</span><span class="sxs-lookup"><span data-stu-id="a5d86-110">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="a5d86-111">Na koniec wywołaj **metodę Get()** **lub GetAsync(),** aby zwrócić produkt.</span><span class="sxs-lookup"><span data-stu-id="a5d86-111">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="a5d86-112">Java</span><span class="sxs-lookup"><span data-stu-id="a5d86-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="a5d86-113">Aby znaleźć konkretny produkt według identyfikatora, użyj funkcji **IAggregatePartner.getProducts,** wybierz kraj przy użyciu funkcji **byCountry(),** a następnie wywołaj funkcję **byId().**</span><span class="sxs-lookup"><span data-stu-id="a5d86-113">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="a5d86-114">Na koniec wywołaj **funkcję get(),** aby zwrócić produkt.</span><span class="sxs-lookup"><span data-stu-id="a5d86-114">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="a5d86-115">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5d86-115">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="a5d86-116">Aby znaleźć określony produkt według identyfikatora, wykonaj polecenie [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) i określ **parametr ProductId.**</span><span class="sxs-lookup"><span data-stu-id="a5d86-116">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="a5d86-117">Parametr **CountryCode** jest opcjami, jeśli nie zostanie określony, zostanie użyty kraj skojarzony z odsprzedawcą.</span><span class="sxs-lookup"><span data-stu-id="a5d86-117">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="a5d86-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a5d86-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a5d86-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a5d86-119">Request syntax</span></span>

| <span data-ttu-id="a5d86-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="a5d86-120">Method</span></span>  | <span data-ttu-id="a5d86-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a5d86-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="a5d86-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a5d86-122">**GET**</span></span> | <span data-ttu-id="a5d86-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{identyfikator-produktu}?country={country} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a5d86-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="a5d86-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a5d86-124">URI parameter</span></span>

<span data-ttu-id="a5d86-125">Użyj następujących parametrów ścieżki, aby uzyskać określony produkt.</span><span class="sxs-lookup"><span data-stu-id="a5d86-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="a5d86-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a5d86-126">Name</span></span>                   | <span data-ttu-id="a5d86-127">Typ</span><span class="sxs-lookup"><span data-stu-id="a5d86-127">Type</span></span>     | <span data-ttu-id="a5d86-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a5d86-128">Required</span></span> | <span data-ttu-id="a5d86-129">Opis</span><span class="sxs-lookup"><span data-stu-id="a5d86-129">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="a5d86-130">product-id</span><span class="sxs-lookup"><span data-stu-id="a5d86-130">product-id</span></span>             | <span data-ttu-id="a5d86-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="a5d86-131">string</span></span>   | <span data-ttu-id="a5d86-132">Tak</span><span class="sxs-lookup"><span data-stu-id="a5d86-132">Yes</span></span>      | <span data-ttu-id="a5d86-133">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="a5d86-133">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="a5d86-134">country</span><span class="sxs-lookup"><span data-stu-id="a5d86-134">country</span></span>                | <span data-ttu-id="a5d86-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="a5d86-135">string</span></span>   | <span data-ttu-id="a5d86-136">Tak</span><span class="sxs-lookup"><span data-stu-id="a5d86-136">Yes</span></span>      | <span data-ttu-id="a5d86-137">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="a5d86-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="a5d86-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a5d86-138">Request headers</span></span>

<span data-ttu-id="a5d86-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a5d86-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a5d86-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a5d86-140">Request body</span></span>

<span data-ttu-id="a5d86-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="a5d86-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a5d86-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a5d86-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="a5d86-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a5d86-143">REST response</span></span>

<span data-ttu-id="a5d86-144">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób](product-resources.md#product) Product.</span><span class="sxs-lookup"><span data-stu-id="a5d86-144">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a5d86-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a5d86-145">Response success and error codes</span></span>

<span data-ttu-id="a5d86-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="a5d86-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a5d86-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a5d86-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a5d86-148">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a5d86-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="a5d86-149">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="a5d86-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="a5d86-150">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="a5d86-150">HTTP Status Code</span></span>     | <span data-ttu-id="a5d86-151">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="a5d86-151">Error code</span></span>   | <span data-ttu-id="a5d86-152">Opis</span><span class="sxs-lookup"><span data-stu-id="a5d86-152">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="a5d86-153">404</span><span class="sxs-lookup"><span data-stu-id="a5d86-153">404</span></span>                  | <span data-ttu-id="a5d86-154">400013</span><span class="sxs-lookup"><span data-stu-id="a5d86-154">400013</span></span>       | <span data-ttu-id="a5d86-155">Nie znaleziono produktu.</span><span class="sxs-lookup"><span data-stu-id="a5d86-155">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="a5d86-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a5d86-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
