---
title: Pobieranie informacji dotyczących użycia licencji
description: Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla pakietu Office i usługi Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768161"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="ba315-103">Pobieranie informacji dotyczących użycia licencji</span><span class="sxs-lookup"><span data-stu-id="ba315-103">Get licenses usage information</span></span>

<span data-ttu-id="ba315-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="ba315-104">**Applies To**</span></span>

- <span data-ttu-id="ba315-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="ba315-105">Partner Center</span></span>

<span data-ttu-id="ba315-106">Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla pakietu Office i usługi Dynamics.</span><span class="sxs-lookup"><span data-stu-id="ba315-106">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba315-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ba315-107">Prerequisites</span></span>

<span data-ttu-id="ba315-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ba315-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ba315-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba315-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ba315-110">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ba315-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ba315-111">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ba315-111">Request syntax</span></span>

| <span data-ttu-id="ba315-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="ba315-112">Method</span></span>  | <span data-ttu-id="ba315-113">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ba315-113">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="ba315-114">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="ba315-114">**GET**</span></span> | <span data-ttu-id="ba315-115">[*{baseURL}*](partner-center-rest-urls.md)/V1/Analytics/Commercial/Usage/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="ba315-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ba315-116">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ba315-116">Request headers</span></span>

<span data-ttu-id="ba315-117">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ba315-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="ba315-118">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="ba315-118">URI parameters</span></span>

| <span data-ttu-id="ba315-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="ba315-119">Parameter</span></span>         | <span data-ttu-id="ba315-120">Typ</span><span class="sxs-lookup"><span data-stu-id="ba315-120">Type</span></span>     | <span data-ttu-id="ba315-121">Opis</span><span class="sxs-lookup"><span data-stu-id="ba315-121">Description</span></span> | <span data-ttu-id="ba315-122">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ba315-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="ba315-123">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="ba315-123">top</span></span>               | <span data-ttu-id="ba315-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-124">string</span></span>   | <span data-ttu-id="ba315-125">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="ba315-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="ba315-126">Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000.</span><span class="sxs-lookup"><span data-stu-id="ba315-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="ba315-127">Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="ba315-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="ba315-128">Nie</span><span class="sxs-lookup"><span data-stu-id="ba315-128">No</span></span> |
| <span data-ttu-id="ba315-129">Pomiń</span><span class="sxs-lookup"><span data-stu-id="ba315-129">skip</span></span>              | <span data-ttu-id="ba315-130">int</span><span class="sxs-lookup"><span data-stu-id="ba315-130">int</span></span>      | <span data-ttu-id="ba315-131">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="ba315-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="ba315-132">Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych.</span><span class="sxs-lookup"><span data-stu-id="ba315-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="ba315-133">Na przykład: Top = 10000 i Skip = 0 pobiera pierwsze 10000 wierszy danych, Top = 10000 i Skip = 10000 pobiera następne 10000 wierszy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ba315-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="ba315-134">Nie</span><span class="sxs-lookup"><span data-stu-id="ba315-134">No</span></span> |
| <span data-ttu-id="ba315-135">filter</span><span class="sxs-lookup"><span data-stu-id="ba315-135">filter</span></span>            | <span data-ttu-id="ba315-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-136">string</span></span>   | <span data-ttu-id="ba315-137">Parametr *Filter* żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ba315-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="ba315-138">Każda instrukcja zawiera pole i wartość, które są skojarzone z **`eq`** **`ne`** operatorami or, a instrukcje można łączyć za pomocą **`and`** lub **`or`** .</span><span class="sxs-lookup"><span data-stu-id="ba315-138">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="ba315-139">Oto przykładowe parametry *filtru* :</span><span class="sxs-lookup"><span data-stu-id="ba315-139">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="ba315-140">*Filter = workloadCode EQ "SFB"*</span><span class="sxs-lookup"><span data-stu-id="ba315-140">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="ba315-141">*Filter = workloadCode EQ "SFB"* lub (*Channel EQ "Odsprzedawca"*)</span><span class="sxs-lookup"><span data-stu-id="ba315-141">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="ba315-142">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="ba315-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="ba315-143">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="ba315-143">**workloadCode**</span></span><br/><span data-ttu-id="ba315-144">**Nr obciążenia**</span><span class="sxs-lookup"><span data-stu-id="ba315-144">**workloadName**</span></span><br/><span data-ttu-id="ba315-145">**Kod servicecode**</span><span class="sxs-lookup"><span data-stu-id="ba315-145">**serviceCode**</span></span><br/><span data-ttu-id="ba315-146">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="ba315-146">**serviceName**</span></span><br/><span data-ttu-id="ba315-147">**ukierunkowan**</span><span class="sxs-lookup"><span data-stu-id="ba315-147">**channel**</span></span><br/><span data-ttu-id="ba315-148">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="ba315-148">**customerTenantId**</span></span><br/><span data-ttu-id="ba315-149">**customerName**</span><span class="sxs-lookup"><span data-stu-id="ba315-149">**customerName**</span></span><br/><span data-ttu-id="ba315-150">**Produktu**</span><span class="sxs-lookup"><span data-stu-id="ba315-150">**productId**</span></span><br/><span data-ttu-id="ba315-151">**productName**</span><span class="sxs-lookup"><span data-stu-id="ba315-151">**productName**</span></span> | <span data-ttu-id="ba315-152">Nie</span><span class="sxs-lookup"><span data-stu-id="ba315-152">No</span></span> |
| <span data-ttu-id="ba315-153">GroupBy</span><span class="sxs-lookup"><span data-stu-id="ba315-153">groupby</span></span>           | <span data-ttu-id="ba315-154">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-154">string</span></span>   | <span data-ttu-id="ba315-155">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="ba315-155">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="ba315-156">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="ba315-156">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="ba315-157">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="ba315-157">**workloadCode**</span></span><br/><span data-ttu-id="ba315-158">**Nr obciążenia**</span><span class="sxs-lookup"><span data-stu-id="ba315-158">**workloadName**</span></span><br/><span data-ttu-id="ba315-159">**Kod servicecode**</span><span class="sxs-lookup"><span data-stu-id="ba315-159">**serviceCode**</span></span><br/><span data-ttu-id="ba315-160">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="ba315-160">**serviceName**</span></span><br/><span data-ttu-id="ba315-161">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="ba315-161">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="ba315-162">**customerName**</span><span class="sxs-lookup"><span data-stu-id="ba315-162">**customerName**</span></span><br/><span data-ttu-id="ba315-163">**Produktu**</span><span class="sxs-lookup"><span data-stu-id="ba315-163">**productId**</span></span><br/><span data-ttu-id="ba315-164">**productName**</span><span class="sxs-lookup"><span data-stu-id="ba315-164">**productName**</span></span><br/><br/><span data-ttu-id="ba315-165">Zwracane wiersze danych będą zawierać pola określone w parametrze *GroupBy* , a także następujące:</span><span class="sxs-lookup"><span data-stu-id="ba315-165">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="ba315-166">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="ba315-166">**licensesActive**</span></span><br/><span data-ttu-id="ba315-167">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="ba315-167">**licensesQualified**</span></span> | <span data-ttu-id="ba315-168">Nie</span><span class="sxs-lookup"><span data-stu-id="ba315-168">No</span></span> |
| <span data-ttu-id="ba315-169">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="ba315-169">processedDateTime</span></span> | <span data-ttu-id="ba315-170">DateTime</span><span class="sxs-lookup"><span data-stu-id="ba315-170">DateTime</span></span> | <span data-ttu-id="ba315-171">Jeden może określać datę przetworzenia danych użycia.</span><span class="sxs-lookup"><span data-stu-id="ba315-171">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="ba315-172">Wartość domyślna to najnowsza Data przetworzenia danych</span><span class="sxs-lookup"><span data-stu-id="ba315-172">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="ba315-173">Nie</span><span class="sxs-lookup"><span data-stu-id="ba315-173">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="ba315-174">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ba315-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ba315-175">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ba315-175">REST response</span></span>

<span data-ttu-id="ba315-176">Jeśli to się powiedzie, treść odpowiedzi zawiera następujące pola zawierające dane dotyczące użycia licencji.</span><span class="sxs-lookup"><span data-stu-id="ba315-176">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="ba315-177">Pole</span><span class="sxs-lookup"><span data-stu-id="ba315-177">Field</span></span>             | <span data-ttu-id="ba315-178">Typ</span><span class="sxs-lookup"><span data-stu-id="ba315-178">Type</span></span>     | <span data-ttu-id="ba315-179">Opis</span><span class="sxs-lookup"><span data-stu-id="ba315-179">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="ba315-180">workloadCode</span><span class="sxs-lookup"><span data-stu-id="ba315-180">workloadCode</span></span>      | <span data-ttu-id="ba315-181">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-181">string</span></span>   | <span data-ttu-id="ba315-182">Kod obciążenia</span><span class="sxs-lookup"><span data-stu-id="ba315-182">Workload code</span></span>                                 |
| <span data-ttu-id="ba315-183">Nr obciążenia</span><span class="sxs-lookup"><span data-stu-id="ba315-183">workloadName</span></span>      | <span data-ttu-id="ba315-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-184">string</span></span>   | <span data-ttu-id="ba315-185">Nazwa obciążenia</span><span class="sxs-lookup"><span data-stu-id="ba315-185">Workload name</span></span>                                 |
| <span data-ttu-id="ba315-186">Kod servicecode</span><span class="sxs-lookup"><span data-stu-id="ba315-186">serviceCode</span></span>       | <span data-ttu-id="ba315-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-187">string</span></span>   | <span data-ttu-id="ba315-188">Kod usługi</span><span class="sxs-lookup"><span data-stu-id="ba315-188">Service code</span></span>                                  |
| <span data-ttu-id="ba315-189">serviceName</span><span class="sxs-lookup"><span data-stu-id="ba315-189">serviceName</span></span>       | <span data-ttu-id="ba315-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-190">string</span></span>   | <span data-ttu-id="ba315-191">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="ba315-191">Service name</span></span>                                  |
| <span data-ttu-id="ba315-192">ukierunkowan</span><span class="sxs-lookup"><span data-stu-id="ba315-192">channel</span></span>           | <span data-ttu-id="ba315-193">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-193">string</span></span>   | <span data-ttu-id="ba315-194">Nazwa kanału, odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="ba315-194">Channel name, reseller</span></span>                        |
| <span data-ttu-id="ba315-195">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="ba315-195">customerTenantId</span></span>  | <span data-ttu-id="ba315-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-196">string</span></span>   | <span data-ttu-id="ba315-197">Unikatowy identyfikator dla klienta</span><span class="sxs-lookup"><span data-stu-id="ba315-197">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="ba315-198">customerName</span><span class="sxs-lookup"><span data-stu-id="ba315-198">customerName</span></span>      | <span data-ttu-id="ba315-199">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-199">string</span></span>   | <span data-ttu-id="ba315-200">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="ba315-200">Customer name</span></span>                                 |
| <span data-ttu-id="ba315-201">productId</span><span class="sxs-lookup"><span data-stu-id="ba315-201">productId</span></span>         | <span data-ttu-id="ba315-202">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-202">string</span></span>   | <span data-ttu-id="ba315-203">Unikatowy identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="ba315-203">Unique identifier for the product</span></span>             |
| <span data-ttu-id="ba315-204">productName</span><span class="sxs-lookup"><span data-stu-id="ba315-204">productName</span></span>       | <span data-ttu-id="ba315-205">ciąg</span><span class="sxs-lookup"><span data-stu-id="ba315-205">string</span></span>   | <span data-ttu-id="ba315-206">Nazwa produktu</span><span class="sxs-lookup"><span data-stu-id="ba315-206">Product name</span></span>                                  |
| <span data-ttu-id="ba315-207">licensesActive</span><span class="sxs-lookup"><span data-stu-id="ba315-207">licensesActive</span></span>    | <span data-ttu-id="ba315-208">długi</span><span class="sxs-lookup"><span data-stu-id="ba315-208">long</span></span>     | <span data-ttu-id="ba315-209">Liczba aktywnych licencji na obciążenie</span><span class="sxs-lookup"><span data-stu-id="ba315-209">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="ba315-210">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="ba315-210">licensesQualified</span></span> | <span data-ttu-id="ba315-211">długi</span><span class="sxs-lookup"><span data-stu-id="ba315-211">long</span></span>     | <span data-ttu-id="ba315-212">Liczba kwalifikowanych licencji dla obciążenia</span><span class="sxs-lookup"><span data-stu-id="ba315-212">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="ba315-213">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="ba315-213">processedDateTime</span></span> | <span data-ttu-id="ba315-214">DateTime</span><span class="sxs-lookup"><span data-stu-id="ba315-214">DateTime</span></span> | <span data-ttu-id="ba315-215">Data ostatniego przetworzenia danych</span><span class="sxs-lookup"><span data-stu-id="ba315-215">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ba315-216">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ba315-216">Response success and error codes</span></span>

<span data-ttu-id="ba315-217">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="ba315-217">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ba315-218">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ba315-218">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ba315-219">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ba315-219">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ba315-220">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ba315-220">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
