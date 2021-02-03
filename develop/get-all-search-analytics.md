---
title: Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania
description: Jak uzyskać wszystkie informacje dotyczące usługi Search Analytics.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767713"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="38618-103">Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="38618-103">Get all search analytics information</span></span>

<span data-ttu-id="38618-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="38618-104">**Applies To**</span></span>

- <span data-ttu-id="38618-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="38618-105">Partner Center</span></span>
- <span data-ttu-id="38618-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="38618-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="38618-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="38618-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="38618-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="38618-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="38618-109">Jak uzyskać wszystkie informacje o analizie wyszukiwania dla swoich klientów.</span><span class="sxs-lookup"><span data-stu-id="38618-109">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38618-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38618-110">Prerequisites</span></span>

- <span data-ttu-id="38618-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="38618-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38618-112">Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38618-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="38618-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="38618-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38618-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="38618-114">Request syntax</span></span>

| <span data-ttu-id="38618-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="38618-115">Method</span></span>  | <span data-ttu-id="38618-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="38618-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="38618-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="38618-117">**GET**</span></span> | <span data-ttu-id="38618-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/Search http/1.1</span><span class="sxs-lookup"><span data-stu-id="38618-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="38618-119">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="38618-119">URI parameters</span></span>

|    <span data-ttu-id="38618-120">Parametr</span><span class="sxs-lookup"><span data-stu-id="38618-120">Parameter</span></span>     |  <span data-ttu-id="38618-121">Typ</span><span class="sxs-lookup"><span data-stu-id="38618-121">Type</span></span>  |                                                                                                                   <span data-ttu-id="38618-122">Opis</span><span class="sxs-lookup"><span data-stu-id="38618-122">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="38618-123">filter</span><span class="sxs-lookup"><span data-stu-id="38618-123">filter</span></span>      | <span data-ttu-id="38618-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="38618-124">string</span></span> |                                                                     <span data-ttu-id="38618-125">Zwraca dane pasujące do warunku filtru.</span><span class="sxs-lookup"><span data-stu-id="38618-125">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="38618-126">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38618-126">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="38618-127">GroupBy</span><span class="sxs-lookup"><span data-stu-id="38618-127">groupby</span></span>      | <span data-ttu-id="38618-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="38618-128">string</span></span> |                                         <span data-ttu-id="38618-129">Obsługuje zarówno warunki, jak i daty.</span><span class="sxs-lookup"><span data-stu-id="38618-129">Supports both terms and dates.</span></span> <span data-ttu-id="38618-130">Algorytm krótkiego obwodu ograniczający liczbę przedziałów.</span><span class="sxs-lookup"><span data-stu-id="38618-130">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="38618-131">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38618-131">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="38618-132">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="38618-132">aggregationLevel</span></span> | <span data-ttu-id="38618-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="38618-133">string</span></span> | <span data-ttu-id="38618-134">Parametr *aggregationLevel* wymaga elementu *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="38618-134">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="38618-135">Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty znajdujących się w *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="38618-135">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="38618-136">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38618-136">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="38618-137">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="38618-137">top</span></span>        | <span data-ttu-id="38618-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="38618-138">string</span></span> |                                                                     <span data-ttu-id="38618-139">Limit stron to 10000.</span><span class="sxs-lookup"><span data-stu-id="38618-139">The page limit is 10000.</span></span> <span data-ttu-id="38618-140">Przyjmuje dowolną wartość mniejszą niż 10000.</span><span class="sxs-lookup"><span data-stu-id="38618-140">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="38618-141">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38618-141">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="38618-142">Pomiń</span><span class="sxs-lookup"><span data-stu-id="38618-142">skip</span></span>       | <span data-ttu-id="38618-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="38618-143">string</span></span> |                                                                                  <span data-ttu-id="38618-144">Liczba wierszy do pominięcia.</span><span class="sxs-lookup"><span data-stu-id="38618-144">Number of rows to skip.</span></span> </br> <span data-ttu-id="38618-145">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38618-145">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="38618-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="38618-146">Request headers</span></span>

<span data-ttu-id="38618-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="38618-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38618-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="38618-148">Request body</span></span>

<span data-ttu-id="38618-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="38618-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="38618-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="38618-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="38618-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="38618-151">REST response</span></span>

<span data-ttu-id="38618-152">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [wyszukiwania](partner-center-analytics-resources.md#search-resource) .</span><span class="sxs-lookup"><span data-stu-id="38618-152">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38618-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38618-153">Response success and error codes</span></span>

<span data-ttu-id="38618-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="38618-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38618-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="38618-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38618-156">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="38618-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38618-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38618-157">Response example</span></span>

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a><span data-ttu-id="38618-158">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="38618-158">See also</span></span>

- [<span data-ttu-id="38618-159">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="38618-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
