---
title: Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania
description: Jak uzyskać wszystkie informacje dotyczące analizy wyszukiwania.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760168"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="909cf-103">Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="909cf-103">Get all search analytics information</span></span>

<span data-ttu-id="909cf-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="909cf-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="909cf-105">Jak uzyskać wszystkie informacje analityczne wyszukiwania dla klientów.</span><span class="sxs-lookup"><span data-stu-id="909cf-105">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="909cf-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="909cf-106">Prerequisites</span></span>

- <span data-ttu-id="909cf-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="909cf-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="909cf-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="909cf-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="909cf-109">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="909cf-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="909cf-110">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="909cf-110">Request syntax</span></span>

| <span data-ttu-id="909cf-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="909cf-111">Method</span></span>  | <span data-ttu-id="909cf-112">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="909cf-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="909cf-113">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="909cf-113">**GET**</span></span> | <span data-ttu-id="909cf-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="909cf-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="909cf-115">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="909cf-115">URI parameters</span></span>

|    <span data-ttu-id="909cf-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="909cf-116">Parameter</span></span>     |  <span data-ttu-id="909cf-117">Typ</span><span class="sxs-lookup"><span data-stu-id="909cf-117">Type</span></span>  |                                                                                                                   <span data-ttu-id="909cf-118">Opis</span><span class="sxs-lookup"><span data-stu-id="909cf-118">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="909cf-119">filter</span><span class="sxs-lookup"><span data-stu-id="909cf-119">filter</span></span>      | <span data-ttu-id="909cf-120">ciąg</span><span class="sxs-lookup"><span data-stu-id="909cf-120">string</span></span> |                                                                     <span data-ttu-id="909cf-121">Zwraca dane zgodne z warunkiem filtru.</span><span class="sxs-lookup"><span data-stu-id="909cf-121">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="909cf-122">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="909cf-122">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="909cf-123">Groupby</span><span class="sxs-lookup"><span data-stu-id="909cf-123">groupby</span></span>      | <span data-ttu-id="909cf-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="909cf-124">string</span></span> |                                         <span data-ttu-id="909cf-125">Obsługuje zarówno terminy, jak i daty.</span><span class="sxs-lookup"><span data-stu-id="909cf-125">Supports both terms and dates.</span></span> <span data-ttu-id="909cf-126">Logika obwodu krótkiego ograniczająca liczbę zasobników.</span><span class="sxs-lookup"><span data-stu-id="909cf-126">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="909cf-127">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="909cf-127">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="909cf-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="909cf-128">aggregationLevel</span></span> | <span data-ttu-id="909cf-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="909cf-129">string</span></span> | <span data-ttu-id="909cf-130">Parametr *aggregationLevel* wymaga *pogrupowania wartości*.</span><span class="sxs-lookup"><span data-stu-id="909cf-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="909cf-131">Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty obecnych w tabeli *grupowania*.</span><span class="sxs-lookup"><span data-stu-id="909cf-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="909cf-132">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="909cf-132">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="909cf-133">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="909cf-133">top</span></span>        | <span data-ttu-id="909cf-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="909cf-134">string</span></span> |                                                                     <span data-ttu-id="909cf-135">Limit stron wynosi 10000.</span><span class="sxs-lookup"><span data-stu-id="909cf-135">The page limit is 10000.</span></span> <span data-ttu-id="909cf-136">Przyjmuje dowolną wartość mniejszą niż 10000.</span><span class="sxs-lookup"><span data-stu-id="909cf-136">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="909cf-137">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="909cf-137">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="909cf-138">Pomiń</span><span class="sxs-lookup"><span data-stu-id="909cf-138">skip</span></span>       | <span data-ttu-id="909cf-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="909cf-139">string</span></span> |                                                                                  <span data-ttu-id="909cf-140">Liczba wierszy do pominięcia.</span><span class="sxs-lookup"><span data-stu-id="909cf-140">Number of rows to skip.</span></span> </br> <span data-ttu-id="909cf-141">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="909cf-141">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="909cf-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="909cf-142">Request headers</span></span>

<span data-ttu-id="909cf-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="909cf-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="909cf-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="909cf-144">Request body</span></span>

<span data-ttu-id="909cf-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="909cf-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="909cf-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="909cf-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="909cf-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="909cf-147">REST response</span></span>

<span data-ttu-id="909cf-148">W przypadku powodzenia treść odpowiedzi zawiera kolekcję [zasobów](partner-center-analytics-resources.md#search-resource) wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="909cf-148">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="909cf-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="909cf-149">Response success and error codes</span></span>

<span data-ttu-id="909cf-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="909cf-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="909cf-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="909cf-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="909cf-152">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="909cf-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="909cf-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="909cf-153">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="909cf-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="909cf-154">See also</span></span>

- [<span data-ttu-id="909cf-155">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="909cf-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
