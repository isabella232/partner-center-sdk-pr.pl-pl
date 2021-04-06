---
title: Pobieranie listy kategorii oferty według rynku
description: Dowiedz się, jak uzyskać kolekcję zawierającą wszystkie kategorie oferty w danym kraju/regionie i ustawieniach regionalnych dla wszystkich chmur firmy Microsoft.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 05aad095c6cb8eaee4cbf7ce976ca1b4b7a408c4
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500060"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="2ca82-103">Pobieranie listy kategorii oferty według rynku</span><span class="sxs-lookup"><span data-stu-id="2ca82-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="2ca82-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="2ca82-104">**Applies to:**</span></span>

- <span data-ttu-id="2ca82-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="2ca82-105">Partner Center</span></span>
- <span data-ttu-id="2ca82-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2ca82-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2ca82-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="2ca82-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2ca82-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2ca82-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2ca82-109">W tym artykule opisano, jak uzyskać kolekcję zawierającą wszystkie kategorie oferty w danym kraju/regionie i ustawieniach regionalnych.</span><span class="sxs-lookup"><span data-stu-id="2ca82-109">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ca82-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ca82-110">Prerequisites</span></span>

- <span data-ttu-id="2ca82-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2ca82-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2ca82-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ca82-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2ca82-113">C\#</span><span class="sxs-lookup"><span data-stu-id="2ca82-113">C\#</span></span>

<span data-ttu-id="2ca82-114">Aby uzyskać listę kategorii oferty w danym kraju/regionie i ustawieniach regionalnych:</span><span class="sxs-lookup"><span data-stu-id="2ca82-114">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="2ca82-115">Użyj kolekcji [**IAggregatePartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) , aby wywołać metodę [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) w danym kontekście.</span><span class="sxs-lookup"><span data-stu-id="2ca82-115">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="2ca82-116">Sprawdź Właściwość [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) obiektu będącego wynikiem.</span><span class="sxs-lookup"><span data-stu-id="2ca82-116">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="2ca82-117">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="2ca82-117">For an example, see the following:</span></span>

- <span data-ttu-id="2ca82-118">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2ca82-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2ca82-119">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="2ca82-119">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="2ca82-120">Klasa: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="2ca82-120">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2ca82-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2ca82-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2ca82-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2ca82-122">Request syntax</span></span>

| <span data-ttu-id="2ca82-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="2ca82-123">Method</span></span>  | <span data-ttu-id="2ca82-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2ca82-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ca82-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="2ca82-125">**GET**</span></span> | <span data-ttu-id="2ca82-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/offercategories? Country = {Country-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2ca82-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="2ca82-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2ca82-127">URI parameter</span></span>

<span data-ttu-id="2ca82-128">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania kategorii oferty.</span><span class="sxs-lookup"><span data-stu-id="2ca82-128">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="2ca82-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2ca82-129">Name</span></span>           | <span data-ttu-id="2ca82-130">Typ</span><span class="sxs-lookup"><span data-stu-id="2ca82-130">Type</span></span>       | <span data-ttu-id="2ca82-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2ca82-131">Required</span></span> | <span data-ttu-id="2ca82-132">Opis</span><span class="sxs-lookup"><span data-stu-id="2ca82-132">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="2ca82-133">**Identyfikator kraju**</span><span class="sxs-lookup"><span data-stu-id="2ca82-133">**country-id**</span></span> | <span data-ttu-id="2ca82-134">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="2ca82-134">**string**</span></span> | <span data-ttu-id="2ca82-135">Y</span><span class="sxs-lookup"><span data-stu-id="2ca82-135">Y</span></span>        | <span data-ttu-id="2ca82-136">Identyfikator kraju/regionu.</span><span class="sxs-lookup"><span data-stu-id="2ca82-136">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2ca82-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2ca82-137">Request headers</span></span>

<span data-ttu-id="2ca82-138">Wymagany jest **identyfikator ustawień regionalnych** , który jest sformatowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="2ca82-138">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="2ca82-139">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2ca82-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2ca82-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2ca82-140">Request body</span></span>

<span data-ttu-id="2ca82-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="2ca82-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2ca82-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2ca82-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2ca82-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2ca82-143">REST response</span></span>

<span data-ttu-id="2ca82-144">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **OfferCategory** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2ca82-144">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2ca82-145">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2ca82-145">Response success and error codes</span></span>

<span data-ttu-id="2ca82-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="2ca82-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2ca82-147">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2ca82-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2ca82-148">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2ca82-148">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2ca82-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2ca82-149">Response example</span></span>

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
