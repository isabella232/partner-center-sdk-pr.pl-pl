---
title: Pobieranie listy ofert dla rynku
description: Pobiera kolekcję zawierającą wszystkie oferty dla określonego rynku.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a004f6f8f8de8cd398d82c300793e4f196efaaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767946"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="e346c-103">Pobieranie listy ofert dla rynku</span><span class="sxs-lookup"><span data-stu-id="e346c-103">Get a list of offers for a market</span></span>

<span data-ttu-id="e346c-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="e346c-104">**Applies To**</span></span>

- <span data-ttu-id="e346c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e346c-105">Partner Center</span></span>
- <span data-ttu-id="e346c-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e346c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e346c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e346c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e346c-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e346c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e346c-109">Pobiera kolekcję zawierającą wszystkie oferty dla określonego rynku.</span><span class="sxs-lookup"><span data-stu-id="e346c-109">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e346c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e346c-110">Prerequisites</span></span>

- <span data-ttu-id="e346c-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e346c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e346c-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e346c-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e346c-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e346c-113">C\#</span></span>

<span data-ttu-id="e346c-114">Aby uzyskać listę ofert na danym rynku, Użyj kolekcji **IAggregatePartner. offers** , wybierz rynek według kraju i Wywołaj metodę **Get ()** lub **Get Async ()** .</span><span class="sxs-lookup"><span data-stu-id="e346c-114">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="e346c-115">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e346c-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e346c-116">**Project**: PartnerSDK. FeatureSample **Klasa**: offers.cs</span><span class="sxs-lookup"><span data-stu-id="e346c-116">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e346c-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e346c-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e346c-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e346c-118">Request syntax</span></span>

| <span data-ttu-id="e346c-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="e346c-119">Method</span></span>  | <span data-ttu-id="e346c-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e346c-120">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="e346c-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e346c-121">**GET**</span></span> | <span data-ttu-id="e346c-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/offers? Country = {Country-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e346c-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="e346c-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e346c-123">URI parameter</span></span>

<span data-ttu-id="e346c-124">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać oferty.</span><span class="sxs-lookup"><span data-stu-id="e346c-124">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="e346c-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e346c-125">Name</span></span>           | <span data-ttu-id="e346c-126">Typ</span><span class="sxs-lookup"><span data-stu-id="e346c-126">Type</span></span>       | <span data-ttu-id="e346c-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e346c-127">Required</span></span> | <span data-ttu-id="e346c-128">Opis</span><span class="sxs-lookup"><span data-stu-id="e346c-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="e346c-129">**Identyfikator kraju**</span><span class="sxs-lookup"><span data-stu-id="e346c-129">**country-id**</span></span> | <span data-ttu-id="e346c-130">**parametry**</span><span class="sxs-lookup"><span data-stu-id="e346c-130">**string**</span></span> | <span data-ttu-id="e346c-131">Y</span><span class="sxs-lookup"><span data-stu-id="e346c-131">Y</span></span>        | <span data-ttu-id="e346c-132">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="e346c-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e346c-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e346c-133">Request headers</span></span>

- <span data-ttu-id="e346c-134">Wymagany jest **identyfikator ustawień regionalnych** , który jest sformatowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="e346c-134">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="e346c-135">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e346c-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e346c-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e346c-136">Request body</span></span>

<span data-ttu-id="e346c-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="e346c-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e346c-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e346c-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="e346c-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e346c-139">REST response</span></span>

<span data-ttu-id="e346c-140">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **oferty** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e346c-140">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e346c-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e346c-141">Response success and error codes</span></span>

<span data-ttu-id="e346c-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e346c-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e346c-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e346c-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e346c-144">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e346c-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e346c-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e346c-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 26584
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
Date: Mon, 23 Nov 2015 23:20:44 GMT

{
    "totalCount":12,"items":[{
        "id":"E60E0348-1710-484B-992A-32B294D4CDE1",
        "name":"Azure Rights Management Premium (Government Pricing)",
        "description":"Microsoft Azure Rights Management Premium helps you protect confidential documents and email with strong encryption.
                       Control the use of your information by specifying who can view, edit, print, save and share your data.
                       Simple to use and integrated with Microsoft Office, SharePoint and Exchange.",
        "minimumQuantity":1,
        "maximumQuantity":10000000,
        "rank":5,
        "uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/E60E0348-1710-484B-992A-32B294D4CDE1",
        "locale":"EN-US",
        "country":"US",
        "category":{
            "id":"Government_Key",
            "name":"Government",
            "rank":40,
            "locale":"en-us",
            "country":"US",
            "attributes":{
                "objectType":"OfferCategory"
            }
        },
        "prerequisiteOffers":[],
        "isAddOn":false,
        "isAvailableForPurchase":true,
        "billing":"license",
        "isAutoRenewable":true,
        "product":{
            "id":"c52ea49f-fe5d-4e95-93ba-1de91d380f89",
            "name":"Azure Rights Management Premium",
            "unit":"Licenses"
        },
        "unitType":"Licenses",
        "links":{
            "learnMore":{
                "uri":"http://g.microsoftonline.com/0BXPS00en/0000",
                "method":"GET",
                "headers":[]
            },
            "self":{
                "uri":"/offers/E60E0348-1710-484B-992A-32B294D4CDE1",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"Offer"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        },
        "previous":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
