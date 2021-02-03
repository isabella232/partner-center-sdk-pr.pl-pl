---
title: Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure
description: Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768169"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="26b70-103">Pobieranie wszystkich informacji analitycznych dotyczących użycia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26b70-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="26b70-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="26b70-104">**Applies To**</span></span>

- <span data-ttu-id="26b70-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="26b70-105">Partner Center</span></span>
- <span data-ttu-id="26b70-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="26b70-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="26b70-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="26b70-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="26b70-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="26b70-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="26b70-109">Jak uzyskać wszystkie informacje dotyczące analizy użycia platformy Azure dla klientów.</span><span class="sxs-lookup"><span data-stu-id="26b70-109">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26b70-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="26b70-110">Prerequisites</span></span>

- <span data-ttu-id="26b70-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="26b70-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="26b70-112">Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="26b70-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="26b70-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="26b70-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="26b70-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="26b70-114">Request syntax</span></span>

| <span data-ttu-id="26b70-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="26b70-115">Method</span></span>  | <span data-ttu-id="26b70-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="26b70-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="26b70-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="26b70-117">**GET**</span></span> | <span data-ttu-id="26b70-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/Usage/Azure http/1.1</span><span class="sxs-lookup"><span data-stu-id="26b70-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="26b70-119">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="26b70-119">URI parameters</span></span>

|<span data-ttu-id="26b70-120">Parametr</span><span class="sxs-lookup"><span data-stu-id="26b70-120">Parameter</span></span>        |<span data-ttu-id="26b70-121">Typ</span><span class="sxs-lookup"><span data-stu-id="26b70-121">Type</span></span>                        |<span data-ttu-id="26b70-122">Opis</span><span class="sxs-lookup"><span data-stu-id="26b70-122">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="26b70-123">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="26b70-123">top</span></span>              | <span data-ttu-id="26b70-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="26b70-124">string</span></span>                     | <span data-ttu-id="26b70-125">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="26b70-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="26b70-126">Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000.</span><span class="sxs-lookup"><span data-stu-id="26b70-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="26b70-127">Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="26b70-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="26b70-128">Pomiń</span><span class="sxs-lookup"><span data-stu-id="26b70-128">skip</span></span>             | <span data-ttu-id="26b70-129">int</span><span class="sxs-lookup"><span data-stu-id="26b70-129">int</span></span>                        | <span data-ttu-id="26b70-130">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="26b70-130">The number of rows to skip in the query.</span></span> <span data-ttu-id="26b70-131">Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych.</span><span class="sxs-lookup"><span data-stu-id="26b70-131">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="26b70-132">Na przykład program `top=10000 and skip=0` Pobiera pierwsze 10000 wierszy danych, `top=10000 and skip=10000` pobiera następne 10000 wierszy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="26b70-132">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="26b70-133">filter</span><span class="sxs-lookup"><span data-stu-id="26b70-133">filter</span></span>           | <span data-ttu-id="26b70-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="26b70-134">string</span></span>                     | <span data-ttu-id="26b70-135">Parametr *Filter* żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="26b70-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="26b70-136">Każda instrukcja zawiera pole i wartość, które są skojarzone z `eq` `ne` operatorami or, a instrukcje można łączyć za pomocą `and` lub `or` .</span><span class="sxs-lookup"><span data-stu-id="26b70-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="26b70-137">Można określić następujące ciągi:</span><span class="sxs-lookup"><span data-stu-id="26b70-137">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="26b70-138">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="26b70-138">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="26b70-139">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="26b70-139">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="26b70-140">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="26b70-140">aggregationLevel</span></span> | <span data-ttu-id="26b70-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="26b70-141">string</span></span>                    | <span data-ttu-id="26b70-142">Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane.</span><span class="sxs-lookup"><span data-stu-id="26b70-142">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="26b70-143">Może być jednym z następujących ciągów: `day` , `week` , lub `month` .</span><span class="sxs-lookup"><span data-stu-id="26b70-143">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="26b70-144">Jeśli nie zostanie określony, wartość domyślna to `day` .</span><span class="sxs-lookup"><span data-stu-id="26b70-144">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="26b70-145">`aggregationLevel`Parametr nie jest obsługiwany bez `groupby` .</span><span class="sxs-lookup"><span data-stu-id="26b70-145">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="26b70-146">Ten `aggregationLevel` parametr ma zastosowanie do wszystkich pól daty znajdujących się w `groupby` .</span><span class="sxs-lookup"><span data-stu-id="26b70-146">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="26b70-147">OrderBy</span><span class="sxs-lookup"><span data-stu-id="26b70-147">orderby</span></span>          |<span data-ttu-id="26b70-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="26b70-148">string</span></span>                     | <span data-ttu-id="26b70-149">Instrukcja, która porządkuje wartości danych wynikowych dla każdej instalacji.</span><span class="sxs-lookup"><span data-stu-id="26b70-149">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="26b70-150">Składnia jest następująca: `...&orderby=field [order],field [order],...`</span><span class="sxs-lookup"><span data-stu-id="26b70-150">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="26b70-151">`field`Parametr może być jednym z następujących ciągów:</span><span class="sxs-lookup"><span data-stu-id="26b70-151">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="26b70-152">Parametr *Order* jest opcjonalny i może mieć wartość `asc` lub `desc` , aby określić kolejność rosnącą lub malejącą dla każdego pola.</span><span class="sxs-lookup"><span data-stu-id="26b70-152">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="26b70-153">Wartość domyślna to `asc`.</span><span class="sxs-lookup"><span data-stu-id="26b70-153">The default is `asc`.</span></span><br/><br/><span data-ttu-id="26b70-154">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="26b70-154">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="26b70-155">GroupBy</span><span class="sxs-lookup"><span data-stu-id="26b70-155">groupby</span></span>          |<span data-ttu-id="26b70-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="26b70-156">string</span></span>                    | <span data-ttu-id="26b70-157">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="26b70-157">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="26b70-158">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="26b70-158">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="26b70-159">Zwracane wiersze danych będą zawierać pola określone w `groupby`  parametrze, a także *ilość*.</span><span class="sxs-lookup"><span data-stu-id="26b70-159">The returned data rows will contain the fields specified in the `groupby`  parameter as well as the *Quantity*.</span></span><br/><br/><span data-ttu-id="26b70-160">`groupby`Parametru można użyć z `aggregationLevel` parametrem.</span><span class="sxs-lookup"><span data-stu-id="26b70-160">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="26b70-161">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="26b70-161">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="26b70-162">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="26b70-162">Request headers</span></span>

<span data-ttu-id="26b70-163">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="26b70-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="26b70-164">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="26b70-164">Request body</span></span>

<span data-ttu-id="26b70-165">Brak.</span><span class="sxs-lookup"><span data-stu-id="26b70-165">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="26b70-166">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="26b70-166">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="26b70-167">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="26b70-167">REST response</span></span>

<span data-ttu-id="26b70-168">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [użycia platformy Azure](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) .</span><span class="sxs-lookup"><span data-stu-id="26b70-168">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="26b70-169">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="26b70-169">Response success and error codes</span></span>

<span data-ttu-id="26b70-170">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="26b70-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="26b70-171">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="26b70-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="26b70-172">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="26b70-172">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="26b70-173">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="26b70-173">Response example</span></span>

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a><span data-ttu-id="26b70-174">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="26b70-174">See also</span></span>

- [<span data-ttu-id="26b70-175">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="26b70-175">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
