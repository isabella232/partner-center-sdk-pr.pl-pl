---
title: Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji
description: Jak uzyskać wszystkie informacje analityczne dotyczące subskrypcji.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760253"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="2f5a4-103">Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2f5a4-103">Get all subscription analytics information</span></span>

<span data-ttu-id="2f5a4-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2f5a4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f5a4-105">W tym artykule opisano sposób uzyskania wszystkich informacji analizy subskrypcji dla klientów.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-105">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f5a4-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f5a4-106">Prerequisites</span></span>

- <span data-ttu-id="2f5a4-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2f5a4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f5a4-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="2f5a4-109">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2f5a4-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f5a4-110">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2f5a4-110">Request syntax</span></span>

| <span data-ttu-id="2f5a4-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="2f5a4-111">Method</span></span> | <span data-ttu-id="2f5a4-112">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2f5a4-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="2f5a4-113">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="2f5a4-113">**GET**</span></span> | <span data-ttu-id="2f5a4-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f5a4-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2f5a4-115">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="2f5a4-115">URI parameters</span></span>

<span data-ttu-id="2f5a4-116">W poniższej tabeli wymieniono parametry opcjonalne i ich opisy:</span><span class="sxs-lookup"><span data-stu-id="2f5a4-116">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="2f5a4-117">Parametr</span><span class="sxs-lookup"><span data-stu-id="2f5a4-117">Parameter</span></span> | <span data-ttu-id="2f5a4-118">Typ</span><span class="sxs-lookup"><span data-stu-id="2f5a4-118">Type</span></span> |  <span data-ttu-id="2f5a4-119">Opis</span><span class="sxs-lookup"><span data-stu-id="2f5a4-119">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="2f5a4-120">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="2f5a4-120">top</span></span> | <span data-ttu-id="2f5a4-121">int</span><span class="sxs-lookup"><span data-stu-id="2f5a4-121">int</span></span> | <span data-ttu-id="2f5a4-122">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-122">The number of rows of data to return in the request.</span></span> <span data-ttu-id="2f5a4-123">Jeśli wartość nie zostanie określona, wartością maksymalną i wartością domyślną będzie `10000` .</span><span class="sxs-lookup"><span data-stu-id="2f5a4-123">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="2f5a4-124">Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-124">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="2f5a4-125">Pomiń</span><span class="sxs-lookup"><span data-stu-id="2f5a4-125">skip</span></span> | <span data-ttu-id="2f5a4-126">int</span><span class="sxs-lookup"><span data-stu-id="2f5a4-126">int</span></span> | <span data-ttu-id="2f5a4-127">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-127">The number of rows to skip in the query.</span></span> <span data-ttu-id="2f5a4-128">Ten parametr umożliwia stronicować duże zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-128">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="2f5a4-129">Na przykład `top=10000` i pobiera pierwsze `skip=0` 10000 wierszy danych i pobiera `top=10000` następne `skip=10000` 10000 wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-129">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="2f5a4-130">filter</span><span class="sxs-lookup"><span data-stu-id="2f5a4-130">filter</span></span> | <span data-ttu-id="2f5a4-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f5a4-131">string</span></span> | <span data-ttu-id="2f5a4-132">Co najmniej jedna instrukcja, która filtruje wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-132">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="2f5a4-133">Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość skojarzoną z operatorem **`eq`** , lub dla niektórych **`ne`** **`contains`** pól.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-133">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="2f5a4-134">Instrukcje można łączyć przy użyciu **`and`** instrukcji lub **`or`** .</span><span class="sxs-lookup"><span data-stu-id="2f5a4-134">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="2f5a4-135">Wartości ciągów muszą być otoczone pojedynczymi cudzysłowami w **parametrze filtru.**</span><span class="sxs-lookup"><span data-stu-id="2f5a4-135">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="2f5a4-136">Zobacz następującą sekcję, aby uzyskać listę pól, które można filtrować, oraz operatory obsługiwane przez te pola.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-136">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="2f5a4-137">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="2f5a4-137">aggregationLevel</span></span> | <span data-ttu-id="2f5a4-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f5a4-138">string</span></span> | <span data-ttu-id="2f5a4-139">Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-139">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="2f5a4-140">Może być jednym z następujących ciągów: **dzień,** **tydzień** lub **miesiąc**.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-140">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="2f5a4-141">Jeśli wartość nie zostanie określona, wartością domyślną jest **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-141">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="2f5a4-142">Ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przekazywane jako część **parametru groupBy.**</span><span class="sxs-lookup"><span data-stu-id="2f5a4-142">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="2f5a4-143">Groupby</span><span class="sxs-lookup"><span data-stu-id="2f5a4-143">groupBy</span></span> | <span data-ttu-id="2f5a4-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f5a4-144">string</span></span> | <span data-ttu-id="2f5a4-145">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-145">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2f5a4-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2f5a4-146">Request headers</span></span>

<span data-ttu-id="2f5a4-147">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2f5a4-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f5a4-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2f5a4-148">Request body</span></span>

<span data-ttu-id="2f5a4-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2f5a4-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2f5a4-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="2f5a4-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2f5a4-151">REST response</span></span>

<span data-ttu-id="2f5a4-152">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [**subskrypcji.**](partner-center-analytics-resources.md#subscription-resource)</span><span class="sxs-lookup"><span data-stu-id="2f5a4-152">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f5a4-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2f5a4-153">Response success and error codes</span></span>

<span data-ttu-id="2f5a4-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f5a4-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2f5a4-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f5a4-156">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2f5a4-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2f5a4-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2f5a4-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2f5a4-158">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2f5a4-158">See also</span></span>

- [<span data-ttu-id="2f5a4-159">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="2f5a4-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
