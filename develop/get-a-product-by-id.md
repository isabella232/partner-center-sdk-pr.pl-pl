---
title: Pobieranie produktu według identyfikatora
description: Pobiera określony zasób produktu przy użyciu identyfikatora produktu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767897"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="dd843-103">Pobieranie produktu według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="dd843-103">Get a product by ID</span></span>

<span data-ttu-id="dd843-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="dd843-104">**Applies To**</span></span>

- <span data-ttu-id="dd843-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="dd843-105">Partner Center</span></span>

<span data-ttu-id="dd843-106">Pobiera określony zasób produktu przy użyciu identyfikatora produktu.</span><span class="sxs-lookup"><span data-stu-id="dd843-106">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd843-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dd843-107">Prerequisites</span></span>

- <span data-ttu-id="dd843-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dd843-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dd843-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dd843-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dd843-110">Identyfikator produktu.</span><span class="sxs-lookup"><span data-stu-id="dd843-110">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="dd843-111">C\#</span><span class="sxs-lookup"><span data-stu-id="dd843-111">C\#</span></span>

<span data-ttu-id="dd843-112">Aby znaleźć konkretny produkt według identyfikatora, Użyj kolekcji **IAggregatePartner. Products** , wybierz kraj przy użyciu metody **ByCountry ()** , a następnie Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="dd843-112">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="dd843-113">Na koniec Wywołaj metodę **Get ()** lub **GetAsync ()** w celu zwrócenia produktu.</span><span class="sxs-lookup"><span data-stu-id="dd843-113">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="dd843-114">Java</span><span class="sxs-lookup"><span data-stu-id="dd843-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="dd843-115">Aby znaleźć konkretny produkt według identyfikatora, użyj funkcji **IAggregatePartner. getProducts** , wybierz kraj przy użyciu funkcji **byCountry ()** , a następnie wywołaj funkcję **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="dd843-115">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="dd843-116">Na koniec wywołaj funkcję **Get ()** w celu zwrócenia produktu.</span><span class="sxs-lookup"><span data-stu-id="dd843-116">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="dd843-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd843-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="dd843-118">Aby znaleźć konkretny produkt według identyfikatora, należy wykonać polecenie [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) i określić parametr **ProductID** .</span><span class="sxs-lookup"><span data-stu-id="dd843-118">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="dd843-119">Parametr **CountryCode** jest opcjami, jeśli nie zostanie określony, zostanie użyty kraj skojarzony z odsprzedawcą.</span><span class="sxs-lookup"><span data-stu-id="dd843-119">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="dd843-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="dd843-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dd843-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="dd843-121">Request syntax</span></span>

| <span data-ttu-id="dd843-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="dd843-122">Method</span></span>  | <span data-ttu-id="dd843-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="dd843-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="dd843-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="dd843-124">**GET**</span></span> | <span data-ttu-id="dd843-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}? Country = {Country} http/1.1</span><span class="sxs-lookup"><span data-stu-id="dd843-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="dd843-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="dd843-126">URI parameter</span></span>

<span data-ttu-id="dd843-127">Aby uzyskać określony produkt, użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="dd843-127">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="dd843-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dd843-128">Name</span></span>                   | <span data-ttu-id="dd843-129">Typ</span><span class="sxs-lookup"><span data-stu-id="dd843-129">Type</span></span>     | <span data-ttu-id="dd843-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd843-130">Required</span></span> | <span data-ttu-id="dd843-131">Opis</span><span class="sxs-lookup"><span data-stu-id="dd843-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="dd843-132">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="dd843-132">product-id</span></span>             | <span data-ttu-id="dd843-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="dd843-133">string</span></span>   | <span data-ttu-id="dd843-134">Tak</span><span class="sxs-lookup"><span data-stu-id="dd843-134">Yes</span></span>      | <span data-ttu-id="dd843-135">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="dd843-135">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="dd843-136">country</span><span class="sxs-lookup"><span data-stu-id="dd843-136">country</span></span>                | <span data-ttu-id="dd843-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="dd843-137">string</span></span>   | <span data-ttu-id="dd843-138">Tak</span><span class="sxs-lookup"><span data-stu-id="dd843-138">Yes</span></span>      | <span data-ttu-id="dd843-139">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="dd843-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="dd843-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="dd843-140">Request headers</span></span>

<span data-ttu-id="dd843-141">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dd843-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dd843-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="dd843-142">Request body</span></span>

<span data-ttu-id="dd843-143">Brak.</span><span class="sxs-lookup"><span data-stu-id="dd843-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dd843-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="dd843-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="dd843-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="dd843-145">REST response</span></span>

<span data-ttu-id="dd843-146">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [produktu](product-resources.md#product) .</span><span class="sxs-lookup"><span data-stu-id="dd843-146">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dd843-147">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dd843-147">Response success and error codes</span></span>

<span data-ttu-id="dd843-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="dd843-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dd843-149">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="dd843-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dd843-150">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dd843-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="dd843-151">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="dd843-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="dd843-152">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="dd843-152">HTTP Status Code</span></span>     | <span data-ttu-id="dd843-153">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="dd843-153">Error code</span></span>   | <span data-ttu-id="dd843-154">Opis</span><span class="sxs-lookup"><span data-stu-id="dd843-154">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="dd843-155">404</span><span class="sxs-lookup"><span data-stu-id="dd843-155">404</span></span>                  | <span data-ttu-id="dd843-156">400013</span><span class="sxs-lookup"><span data-stu-id="dd843-156">400013</span></span>       | <span data-ttu-id="dd843-157">Produkt nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="dd843-157">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="dd843-158">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dd843-158">Response example</span></span>

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
