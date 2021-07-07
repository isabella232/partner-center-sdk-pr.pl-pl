---
title: Pobieranie oferty według identyfikatora
description: Pobiera zasób Oferty, który odpowiada identyfikatorowi oferty.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: f759cbdeefb4f550c41b41de40e9979e72e4ddeb
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760644"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="b8f08-103">Pobieranie oferty według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="b8f08-103">Get an offer by ID</span></span>

<span data-ttu-id="b8f08-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b8f08-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b8f08-105">Pobiera **zasób Oferty,** który odpowiada identyfikatorowi oferty.</span><span class="sxs-lookup"><span data-stu-id="b8f08-105">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8f08-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b8f08-106">Prerequisites</span></span>

- <span data-ttu-id="b8f08-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b8f08-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b8f08-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b8f08-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b8f08-109">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="b8f08-109">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="b8f08-110">C\#</span><span class="sxs-lookup"><span data-stu-id="b8f08-110">C\#</span></span>

<span data-ttu-id="b8f08-111">Aby znaleźć określoną ofertę według identyfikatora, użyj kolekcji **IAggregatePartner.Offers,** ustanów kraj za pomocą wywołania metody **ByCountry(),** a następnie wywołaj metodę [**ByID().**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="b8f08-111">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="b8f08-112">Następnie wywołaj metodę [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) [**lub Get Async().**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="b8f08-112">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="b8f08-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b8f08-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b8f08-114">**Project:** PartnerSDK.FeatureSample, **klasa**: GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="b8f08-114">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="b8f08-115">Java</span><span class="sxs-lookup"><span data-stu-id="b8f08-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="b8f08-116">Aby znaleźć określoną ofertę według identyfikatora, użyj funkcji **IAggregatePartner.getOffers,** ustanów kraj za pomocą wywołania funkcji **byCountry(),** a następnie wywołaj funkcję **byID().**</span><span class="sxs-lookup"><span data-stu-id="b8f08-116">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="b8f08-117">Następnie wywołaj **funkcję get().**</span><span class="sxs-lookup"><span data-stu-id="b8f08-117">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="b8f08-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8f08-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="b8f08-119">Aby znaleźć określoną ofertę według identyfikatora, wykonaj polecenie [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) i określ parametry **CountryCode** i **OfferId.**</span><span class="sxs-lookup"><span data-stu-id="b8f08-119">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="b8f08-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b8f08-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8f08-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b8f08-121">Request syntax</span></span>

| <span data-ttu-id="b8f08-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="b8f08-122">Method</span></span>  | <span data-ttu-id="b8f08-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b8f08-123">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b8f08-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b8f08-124">**GET**</span></span> | <span data-ttu-id="b8f08-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{identyfikator-oferty}?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b8f08-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b8f08-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b8f08-126">URI parameter</span></span>

| <span data-ttu-id="b8f08-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b8f08-127">Name</span></span>           | <span data-ttu-id="b8f08-128">Typ</span><span class="sxs-lookup"><span data-stu-id="b8f08-128">Type</span></span>       | <span data-ttu-id="b8f08-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b8f08-129">Required</span></span> | <span data-ttu-id="b8f08-130">Opis</span><span class="sxs-lookup"><span data-stu-id="b8f08-130">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="b8f08-131">**identyfikator oferty**</span><span class="sxs-lookup"><span data-stu-id="b8f08-131">**offer-id**</span></span>   | <span data-ttu-id="b8f08-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="b8f08-132">**guid**</span></span>   | <span data-ttu-id="b8f08-133">Y</span><span class="sxs-lookup"><span data-stu-id="b8f08-133">Y</span></span>        | <span data-ttu-id="b8f08-134">Identyfikator GUID odpowiadający ofercie.</span><span class="sxs-lookup"><span data-stu-id="b8f08-134">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="b8f08-135">**country-id**</span><span class="sxs-lookup"><span data-stu-id="b8f08-135">**country-id**</span></span> | <span data-ttu-id="b8f08-136">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="b8f08-136">**string**</span></span> | <span data-ttu-id="b8f08-137">Y</span><span class="sxs-lookup"><span data-stu-id="b8f08-137">Y</span></span>        | <span data-ttu-id="b8f08-138">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="b8f08-138">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="b8f08-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b8f08-139">Request headers</span></span>

- <span data-ttu-id="b8f08-140">Wymagany **jest identyfikator locale-id** sformatowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="b8f08-140">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="b8f08-141">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b8f08-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b8f08-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b8f08-142">Request body</span></span>

<span data-ttu-id="b8f08-143">Brak.</span><span class="sxs-lookup"><span data-stu-id="b8f08-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b8f08-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b8f08-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="b8f08-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b8f08-145">REST response</span></span>

<span data-ttu-id="b8f08-146">W przypadku powodzenia ta metoda zwraca **zasób Offer** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b8f08-146">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8f08-147">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b8f08-147">Response success and error codes</span></span>

<span data-ttu-id="b8f08-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="b8f08-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8f08-149">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b8f08-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b8f08-150">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b8f08-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b8f08-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b8f08-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
