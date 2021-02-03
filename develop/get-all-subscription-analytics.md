---
title: Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji
description: Jak uzyskać wszystkie informacje o usłudze Subscription Analytics.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767710"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="e4d66-103">Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e4d66-103">Get all subscription analytics information</span></span>

<span data-ttu-id="e4d66-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="e4d66-104">**Applies to:**</span></span>

- <span data-ttu-id="e4d66-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e4d66-105">Partner Center</span></span>
- <span data-ttu-id="e4d66-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e4d66-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e4d66-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e4d66-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e4d66-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e4d66-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e4d66-109">W tym artykule opisano, jak uzyskać wszystkie informacje o usłudze Subscription Analytics dla swoich klientów.</span><span class="sxs-lookup"><span data-stu-id="e4d66-109">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4d66-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e4d66-110">Prerequisites</span></span>

- <span data-ttu-id="e4d66-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e4d66-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4d66-112">Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4d66-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e4d66-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e4d66-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4d66-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e4d66-114">Request syntax</span></span>

| <span data-ttu-id="e4d66-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="e4d66-115">Method</span></span> | <span data-ttu-id="e4d66-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e4d66-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="e4d66-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e4d66-117">**GET**</span></span> | <span data-ttu-id="e4d66-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/subscriptions http/1.1</span><span class="sxs-lookup"><span data-stu-id="e4d66-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e4d66-119">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="e4d66-119">URI parameters</span></span>

<span data-ttu-id="e4d66-120">W poniższej tabeli wymieniono parametry opcjonalne i ich opisy:</span><span class="sxs-lookup"><span data-stu-id="e4d66-120">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="e4d66-121">Parametr</span><span class="sxs-lookup"><span data-stu-id="e4d66-121">Parameter</span></span> | <span data-ttu-id="e4d66-122">Typ</span><span class="sxs-lookup"><span data-stu-id="e4d66-122">Type</span></span> |  <span data-ttu-id="e4d66-123">Opis</span><span class="sxs-lookup"><span data-stu-id="e4d66-123">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="e4d66-124">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="e4d66-124">top</span></span> | <span data-ttu-id="e4d66-125">int</span><span class="sxs-lookup"><span data-stu-id="e4d66-125">int</span></span> | <span data-ttu-id="e4d66-126">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="e4d66-126">The number of rows of data to return in the request.</span></span> <span data-ttu-id="e4d66-127">Jeśli wartość nie jest określona, wartość maksymalna i wartość domyślna to `10000` .</span><span class="sxs-lookup"><span data-stu-id="e4d66-127">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="e4d66-128">Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="e4d66-128">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="e4d66-129">Pomiń</span><span class="sxs-lookup"><span data-stu-id="e4d66-129">skip</span></span> | <span data-ttu-id="e4d66-130">int</span><span class="sxs-lookup"><span data-stu-id="e4d66-130">int</span></span> | <span data-ttu-id="e4d66-131">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="e4d66-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="e4d66-132">Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych.</span><span class="sxs-lookup"><span data-stu-id="e4d66-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="e4d66-133">Na przykład program `top=10000` `skip=0` pobiera pierwsze 10000 wierszy danych `top=10000` i `skip=10000` pobiera następne 10000 wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="e4d66-133">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="e4d66-134">filter</span><span class="sxs-lookup"><span data-stu-id="e4d66-134">filter</span></span> | <span data-ttu-id="e4d66-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="e4d66-135">string</span></span> | <span data-ttu-id="e4d66-136">Jedna lub więcej instrukcji, które filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e4d66-136">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="e4d66-137">Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość, która jest skojarzona z **`eq`** , **`ne`** lub dla niektórych pól, **`contains`** operatora.</span><span class="sxs-lookup"><span data-stu-id="e4d66-137">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="e4d66-138">Instrukcje można łączyć przy użyciu **`and`** lub **`or`** .</span><span class="sxs-lookup"><span data-stu-id="e4d66-138">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="e4d66-139">Wartości ciągu muszą być ujęte w pojedyncze cudzysłowy w parametrze **Filter** .</span><span class="sxs-lookup"><span data-stu-id="e4d66-139">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="e4d66-140">W poniższej sekcji znajduje się lista pól, które można filtrować i operatory, które są obsługiwane przez te pola.</span><span class="sxs-lookup"><span data-stu-id="e4d66-140">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="e4d66-141">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="e4d66-141">aggregationLevel</span></span> | <span data-ttu-id="e4d66-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="e4d66-142">string</span></span> | <span data-ttu-id="e4d66-143">Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane.</span><span class="sxs-lookup"><span data-stu-id="e4d66-143">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="e4d66-144">Może to być jeden z następujących ciągów: **dzień**, **tydzień** lub **miesiąc**.</span><span class="sxs-lookup"><span data-stu-id="e4d66-144">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="e4d66-145">Jeśli wartość nie jest określona, wartością domyślną jest **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="e4d66-145">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="e4d66-146">Ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przesyłane jako część parametru **GroupBy** .</span><span class="sxs-lookup"><span data-stu-id="e4d66-146">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="e4d66-147">groupBy</span><span class="sxs-lookup"><span data-stu-id="e4d66-147">groupBy</span></span> | <span data-ttu-id="e4d66-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="e4d66-148">string</span></span> | <span data-ttu-id="e4d66-149">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="e4d66-149">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e4d66-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e4d66-150">Request headers</span></span>

<span data-ttu-id="e4d66-151">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e4d66-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4d66-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e4d66-152">Request body</span></span>

<span data-ttu-id="e4d66-153">Brak.</span><span class="sxs-lookup"><span data-stu-id="e4d66-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e4d66-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e4d66-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="e4d66-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e4d66-155">REST response</span></span>

<span data-ttu-id="e4d66-156">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [**subskrypcji**](partner-center-analytics-resources.md#subscription-resource) .</span><span class="sxs-lookup"><span data-stu-id="e4d66-156">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4d66-157">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e4d66-157">Response success and error codes</span></span>

<span data-ttu-id="e4d66-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e4d66-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4d66-159">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e4d66-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4d66-160">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e4d66-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e4d66-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e4d66-161">Response example</span></span>

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a><span data-ttu-id="e4d66-162">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e4d66-162">See also</span></span>

- [<span data-ttu-id="e4d66-163">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="e4d66-163">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
