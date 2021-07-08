---
title: Pobieranie listy kategorii oferty według rynku
description: Dowiedz się, jak uzyskać kolekcję zawierającą wszystkie kategorie ofert w danym kraju/regionie oraz informacje o lokalnych lokalizacjach dla wszystkich chmur firmy Microsoft.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874282"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="9803e-103">Pobieranie listy kategorii oferty według rynku</span><span class="sxs-lookup"><span data-stu-id="9803e-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="9803e-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9803e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9803e-105">W tym artykule opisano sposób pobierania kolekcji zawierającej wszystkie kategorie ofert w danym kraju/regionie i w określonych regionach.</span><span class="sxs-lookup"><span data-stu-id="9803e-105">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9803e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9803e-106">Prerequisites</span></span>

- <span data-ttu-id="9803e-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9803e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9803e-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9803e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="9803e-109">C\#</span><span class="sxs-lookup"><span data-stu-id="9803e-109">C\#</span></span>

<span data-ttu-id="9803e-110">Aby uzyskać listę kategorii ofert w danym kraju/regionie i w określonych regionach:</span><span class="sxs-lookup"><span data-stu-id="9803e-110">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="9803e-111">Użyj [**kolekcji IAggregatePartner.Operations,**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) aby wywołać metodę [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) w danym kontekście.</span><span class="sxs-lookup"><span data-stu-id="9803e-111">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="9803e-112">Sprawdź właściwość [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) wynikowego obiektu.</span><span class="sxs-lookup"><span data-stu-id="9803e-112">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="9803e-113">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="9803e-113">For an example, see the following:</span></span>

- <span data-ttu-id="9803e-114">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9803e-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="9803e-115">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="9803e-115">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="9803e-116">Klasa: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="9803e-116">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="9803e-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9803e-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9803e-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9803e-118">Request syntax</span></span>

| <span data-ttu-id="9803e-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="9803e-119">Method</span></span>  | <span data-ttu-id="9803e-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9803e-120">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="9803e-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9803e-121">**GET**</span></span> | <span data-ttu-id="9803e-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9803e-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="9803e-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9803e-123">URI parameter</span></span>

<span data-ttu-id="9803e-124">Ta tabela zawiera listę parametrów zapytania wymaganych do uzyskania kategorii ofert.</span><span class="sxs-lookup"><span data-stu-id="9803e-124">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="9803e-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9803e-125">Name</span></span>           | <span data-ttu-id="9803e-126">Typ</span><span class="sxs-lookup"><span data-stu-id="9803e-126">Type</span></span>       | <span data-ttu-id="9803e-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9803e-127">Required</span></span> | <span data-ttu-id="9803e-128">Opis</span><span class="sxs-lookup"><span data-stu-id="9803e-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="9803e-129">**country-id**</span><span class="sxs-lookup"><span data-stu-id="9803e-129">**country-id**</span></span> | <span data-ttu-id="9803e-130">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="9803e-130">**string**</span></span> | <span data-ttu-id="9803e-131">Y</span><span class="sxs-lookup"><span data-stu-id="9803e-131">Y</span></span>        | <span data-ttu-id="9803e-132">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="9803e-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9803e-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9803e-133">Request headers</span></span>

<span data-ttu-id="9803e-134">Wymagany **jest identyfikator locale-id** sformatowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="9803e-134">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="9803e-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9803e-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9803e-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9803e-136">Request body</span></span>

<span data-ttu-id="9803e-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="9803e-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9803e-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9803e-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9803e-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9803e-139">REST response</span></span>

<span data-ttu-id="9803e-140">W przypadku powodzenia ta metoda zwraca kolekcję zasobów **OfferCategory** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9803e-140">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9803e-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9803e-141">Response success and error codes</span></span>

<span data-ttu-id="9803e-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9803e-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9803e-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9803e-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9803e-144">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9803e-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9803e-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9803e-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
