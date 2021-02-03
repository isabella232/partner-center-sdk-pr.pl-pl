---
title: Pobieranie wszystkich informacji analitycznych dotyczących poleceń
description: Jak uzyskać wszystkie informacje analityczne dotyczące odwołań.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767929"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="3d587-103">Pobieranie wszystkich informacji analitycznych dotyczących poleceń</span><span class="sxs-lookup"><span data-stu-id="3d587-103">Get all referrals analytics information</span></span>

<span data-ttu-id="3d587-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="3d587-104">**Applies To**</span></span>

- <span data-ttu-id="3d587-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="3d587-105">Partner Center</span></span>
- <span data-ttu-id="3d587-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="3d587-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3d587-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3d587-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3d587-108">Jak uzyskać wszystkie informacje o analizie odwołań dla swoich klientów.</span><span class="sxs-lookup"><span data-stu-id="3d587-108">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d587-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3d587-109">Prerequisites</span></span>

- <span data-ttu-id="3d587-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3d587-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3d587-111">Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3d587-111">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3d587-112">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3d587-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3d587-113">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3d587-113">Request syntax</span></span>

| <span data-ttu-id="3d587-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="3d587-114">Method</span></span>  | <span data-ttu-id="3d587-115">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3d587-115">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="3d587-116">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3d587-116">**GET**</span></span> | <span data-ttu-id="3d587-117">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/Referrals http/1.1</span><span class="sxs-lookup"><span data-stu-id="3d587-117">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3d587-118">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="3d587-118">URI parameters</span></span>

| <span data-ttu-id="3d587-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="3d587-119">Parameter</span></span> | <span data-ttu-id="3d587-120">Typ</span><span class="sxs-lookup"><span data-stu-id="3d587-120">Type</span></span> | <span data-ttu-id="3d587-121">Opis</span><span class="sxs-lookup"><span data-stu-id="3d587-121">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="3d587-122">filter</span><span class="sxs-lookup"><span data-stu-id="3d587-122">filter</span></span> | <span data-ttu-id="3d587-123">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d587-123">string</span></span> | <span data-ttu-id="3d587-124">Zwraca dane pasujące do warunku filtru.</span><span class="sxs-lookup"><span data-stu-id="3d587-124">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="3d587-125">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="3d587-125">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="3d587-126">GroupBy</span><span class="sxs-lookup"><span data-stu-id="3d587-126">groupby</span></span> | <span data-ttu-id="3d587-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d587-127">string</span></span> | <span data-ttu-id="3d587-128">Obsługuje zarówno warunki, jak i daty.</span><span class="sxs-lookup"><span data-stu-id="3d587-128">Supports both terms and dates.</span></span> <span data-ttu-id="3d587-129">Algorytm krótkiego obwodu ograniczający liczbę przedziałów.</span><span class="sxs-lookup"><span data-stu-id="3d587-129">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="3d587-130">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="3d587-130">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="3d587-131">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="3d587-131">aggregationLevel</span></span> | <span data-ttu-id="3d587-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d587-132">string</span></span> | <span data-ttu-id="3d587-133">Parametr *aggregationLevel* wymaga elementu *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="3d587-133">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="3d587-134">Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty znajdujących się w *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="3d587-134">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="3d587-135">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="3d587-135">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="3d587-136">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="3d587-136">top</span></span> | <span data-ttu-id="3d587-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d587-137">string</span></span> | <span data-ttu-id="3d587-138">Limit stron to 10000.</span><span class="sxs-lookup"><span data-stu-id="3d587-138">The page limit is 10000.</span></span> <span data-ttu-id="3d587-139">Przyjmuje dowolną wartość mniejszą niż 10000.</span><span class="sxs-lookup"><span data-stu-id="3d587-139">Takes any value less than 10000.</span></span></br> <span data-ttu-id="3d587-140">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="3d587-140">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="3d587-141">Pomiń</span><span class="sxs-lookup"><span data-stu-id="3d587-141">skip</span></span> | <span data-ttu-id="3d587-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d587-142">string</span></span> | <span data-ttu-id="3d587-143">Liczba wierszy do pominięcia.</span><span class="sxs-lookup"><span data-stu-id="3d587-143">Number of rows to skip.</span></span></br> <span data-ttu-id="3d587-144">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="3d587-144">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="3d587-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3d587-145">Request headers</span></span>

<span data-ttu-id="3d587-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3d587-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3d587-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3d587-147">Request body</span></span>

<span data-ttu-id="3d587-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="3d587-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3d587-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3d587-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3d587-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3d587-150">REST response</span></span>

<span data-ttu-id="3d587-151">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [odwołań](partner-center-analytics-resources.md#referrals-resource) .</span><span class="sxs-lookup"><span data-stu-id="3d587-151">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3d587-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3d587-152">Response success and error codes</span></span>

<span data-ttu-id="3d587-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="3d587-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3d587-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3d587-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3d587-155">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3d587-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3d587-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3d587-156">Response example</span></span>

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a><span data-ttu-id="3d587-157">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3d587-157">See also</span></span>

- [<span data-ttu-id="3d587-158">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="3d587-158">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
