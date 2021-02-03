---
title: Pobieranie oferty według identyfikatora
description: Pobiera zasób oferty, który jest zgodny z IDENTYFIKATORem oferty.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768481"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="0b05e-103">Pobieranie oferty według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="0b05e-103">Get an offer by ID</span></span>

<span data-ttu-id="0b05e-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="0b05e-104">**Applies To**</span></span>

- <span data-ttu-id="0b05e-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0b05e-105">Partner Center</span></span>
- <span data-ttu-id="0b05e-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0b05e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0b05e-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="0b05e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0b05e-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0b05e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0b05e-109">Pobiera zasób **oferty** , który jest zgodny z identyfikatorem oferty.</span><span class="sxs-lookup"><span data-stu-id="0b05e-109">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b05e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0b05e-110">Prerequisites</span></span>

- <span data-ttu-id="0b05e-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0b05e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b05e-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0b05e-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0b05e-113">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="0b05e-113">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="0b05e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="0b05e-114">C\#</span></span>

<span data-ttu-id="0b05e-115">Aby znaleźć określoną ofertę według identyfikatora, Użyj kolekcji **IAggregatePartner. offers** , ustal kraj z wywołaniem **ByCountry ()**, a następnie Wywołaj metodę [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="0b05e-115">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="0b05e-116">Następnie Wywołaj metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) lub [**Get Async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="0b05e-116">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="0b05e-117">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b05e-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0b05e-118">**Project**: PartnerSDK. FeatureSample **Klasa**: GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="0b05e-118">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="0b05e-119">Java</span><span class="sxs-lookup"><span data-stu-id="0b05e-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="0b05e-120">Aby znaleźć określoną ofertę według identyfikatora, użyj funkcji **IAggregatePartner. Getoffers** , ustal kraj z wywołaniem funkcji **byCountry ()** , a następnie wywołaj funkcję **byID ()** .</span><span class="sxs-lookup"><span data-stu-id="0b05e-120">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="0b05e-121">Następnie wywołaj funkcję **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="0b05e-121">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="0b05e-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b05e-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="0b05e-123">Aby znaleźć określoną ofertę według identyfikatora, należy wykonać polecenie [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) i określić parametry **CountryCode** i **OfferId** .</span><span class="sxs-lookup"><span data-stu-id="0b05e-123">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="0b05e-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0b05e-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0b05e-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0b05e-125">Request syntax</span></span>

| <span data-ttu-id="0b05e-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="0b05e-126">Method</span></span>  | <span data-ttu-id="0b05e-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0b05e-127">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b05e-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="0b05e-128">**GET**</span></span> | <span data-ttu-id="0b05e-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/offers/{Offer-ID}? Country = {Country-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="0b05e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0b05e-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0b05e-130">URI parameter</span></span>

| <span data-ttu-id="0b05e-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0b05e-131">Name</span></span>           | <span data-ttu-id="0b05e-132">Typ</span><span class="sxs-lookup"><span data-stu-id="0b05e-132">Type</span></span>       | <span data-ttu-id="0b05e-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0b05e-133">Required</span></span> | <span data-ttu-id="0b05e-134">Opis</span><span class="sxs-lookup"><span data-stu-id="0b05e-134">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="0b05e-135">**Oferta — identyfikator**</span><span class="sxs-lookup"><span data-stu-id="0b05e-135">**offer-id**</span></span>   | <span data-ttu-id="0b05e-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="0b05e-136">**guid**</span></span>   | <span data-ttu-id="0b05e-137">Y</span><span class="sxs-lookup"><span data-stu-id="0b05e-137">Y</span></span>        | <span data-ttu-id="0b05e-138">Identyfikator GUID, który odpowiada ofercie.</span><span class="sxs-lookup"><span data-stu-id="0b05e-138">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="0b05e-139">**Identyfikator kraju**</span><span class="sxs-lookup"><span data-stu-id="0b05e-139">**country-id**</span></span> | <span data-ttu-id="0b05e-140">**parametry**</span><span class="sxs-lookup"><span data-stu-id="0b05e-140">**string**</span></span> | <span data-ttu-id="0b05e-141">Y</span><span class="sxs-lookup"><span data-stu-id="0b05e-141">Y</span></span>        | <span data-ttu-id="0b05e-142">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="0b05e-142">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="0b05e-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0b05e-143">Request headers</span></span>

- <span data-ttu-id="0b05e-144">Wymagany jest **identyfikator ustawień regionalnych** , który jest sformatowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="0b05e-144">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="0b05e-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0b05e-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0b05e-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0b05e-146">Request body</span></span>

<span data-ttu-id="0b05e-147">Brak.</span><span class="sxs-lookup"><span data-stu-id="0b05e-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0b05e-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0b05e-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="0b05e-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0b05e-149">REST response</span></span>

<span data-ttu-id="0b05e-150">Jeśli to się powiedzie, ta metoda zwraca zasób **oferty** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0b05e-150">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0b05e-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0b05e-151">Response success and error codes</span></span>

<span data-ttu-id="0b05e-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="0b05e-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0b05e-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0b05e-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0b05e-154">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0b05e-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0b05e-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0b05e-155">Response example</span></span>

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
