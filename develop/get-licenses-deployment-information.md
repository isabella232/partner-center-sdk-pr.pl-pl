---
title: Pobieranie informacji dotyczących wdrażania licencji
description: Jak uzyskać informacje o wdrażaniu licencji dla pakietu Office i usługi Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768165"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="ecf9d-103">Pobieranie informacji dotyczących wdrażania licencji</span><span class="sxs-lookup"><span data-stu-id="ecf9d-103">Get licenses deployment information</span></span>

<span data-ttu-id="ecf9d-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-104">**Applies To**</span></span>

- <span data-ttu-id="ecf9d-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="ecf9d-105">Partner Center</span></span>

<span data-ttu-id="ecf9d-106">Jak uzyskać informacje o wdrażaniu licencji dla pakietu Office i usługi Dynamics.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-106">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecf9d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ecf9d-107">Prerequisites</span></span>

<span data-ttu-id="ecf9d-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ecf9d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ecf9d-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ecf9d-110">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ecf9d-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ecf9d-111">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ecf9d-111">Request syntax</span></span>

| <span data-ttu-id="ecf9d-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="ecf9d-112">Method</span></span>  | <span data-ttu-id="ecf9d-113">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ecf9d-113">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ecf9d-114">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-114">**GET**</span></span> | <span data-ttu-id="ecf9d-115">[*{baseURL}*](partner-center-rest-urls.md)/V1/Analytics/Commercial/Deployment/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="ecf9d-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ecf9d-116">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ecf9d-116">Request headers</span></span>

<span data-ttu-id="ecf9d-117">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ecf9d-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="ecf9d-118">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="ecf9d-118">URI parameters</span></span>

| <span data-ttu-id="ecf9d-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="ecf9d-119">Parameter</span></span>         | <span data-ttu-id="ecf9d-120">Typ</span><span class="sxs-lookup"><span data-stu-id="ecf9d-120">Type</span></span>     | <span data-ttu-id="ecf9d-121">Opis</span><span class="sxs-lookup"><span data-stu-id="ecf9d-121">Description</span></span> | <span data-ttu-id="ecf9d-122">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ecf9d-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="ecf9d-123">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="ecf9d-123">top</span></span>               | <span data-ttu-id="ecf9d-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-124">string</span></span>   | <span data-ttu-id="ecf9d-125">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="ecf9d-126">Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="ecf9d-127">Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="ecf9d-128">Nie</span><span class="sxs-lookup"><span data-stu-id="ecf9d-128">No</span></span> |
| <span data-ttu-id="ecf9d-129">Pomiń</span><span class="sxs-lookup"><span data-stu-id="ecf9d-129">skip</span></span>              | <span data-ttu-id="ecf9d-130">int</span><span class="sxs-lookup"><span data-stu-id="ecf9d-130">int</span></span>      | <span data-ttu-id="ecf9d-131">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="ecf9d-132">Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="ecf9d-133">Na przykład: Top = 10000 i Skip = 0 pobiera pierwsze 10000 wierszy danych, Top = 10000 i Skip = 10000 pobiera następne 10000 wierszy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="ecf9d-134">Nie</span><span class="sxs-lookup"><span data-stu-id="ecf9d-134">No</span></span> |
| <span data-ttu-id="ecf9d-135">filter</span><span class="sxs-lookup"><span data-stu-id="ecf9d-135">filter</span></span>            | <span data-ttu-id="ecf9d-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-136">string</span></span>   | <span data-ttu-id="ecf9d-137">Parametr *Filter* żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="ecf9d-138">Każda instrukcja zawiera pole i wartość, które są skojarzone z `eq` `ne` operatorami or, a instrukcje można łączyć za pomocą `and` lub `or` .</span><span class="sxs-lookup"><span data-stu-id="ecf9d-138">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="ecf9d-139">Oto przykładowe parametry *filtru* :</span><span class="sxs-lookup"><span data-stu-id="ecf9d-139">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="ecf9d-140">*Filter = servicecode EQ "O365"*</span><span class="sxs-lookup"><span data-stu-id="ecf9d-140">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="ecf9d-141">*Filter = servicecode EQ "O365"* lub (*Channel EQ "Odsprzedawca"*)</span><span class="sxs-lookup"><span data-stu-id="ecf9d-141">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="ecf9d-142">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="ecf9d-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="ecf9d-143">**Kod servicecode**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-143">**serviceCode**</span></span><br/><span data-ttu-id="ecf9d-144">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-144">**serviceName**</span></span><br/><span data-ttu-id="ecf9d-145">**ukierunkowan**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-145">**channel**</span></span><br/><span data-ttu-id="ecf9d-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-146">**customerTenantId**</span></span><br/><span data-ttu-id="ecf9d-147">**customerName**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-147">**customerName**</span></span><br/><span data-ttu-id="ecf9d-148">**Produktu**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-148">**productId**</span></span><br/><span data-ttu-id="ecf9d-149">**productName**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-149">**productName**</span></span>  | <span data-ttu-id="ecf9d-150">Nie</span><span class="sxs-lookup"><span data-stu-id="ecf9d-150">No</span></span> |
| <span data-ttu-id="ecf9d-151">GroupBy</span><span class="sxs-lookup"><span data-stu-id="ecf9d-151">groupby</span></span>           | <span data-ttu-id="ecf9d-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-152">string</span></span>   | <span data-ttu-id="ecf9d-153">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="ecf9d-154">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="ecf9d-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="ecf9d-155">**Kod servicecode**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-155">**serviceCode**</span></span><br/><span data-ttu-id="ecf9d-156">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-156">**serviceName**</span></span><br/><span data-ttu-id="ecf9d-157">**ukierunkowan**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-157">**channel**</span></span><br/><span data-ttu-id="ecf9d-158">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-158">**customerTenantId**</span></span><br/><span data-ttu-id="ecf9d-159">**customerName**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-159">**customerName**</span></span><br/><span data-ttu-id="ecf9d-160">**Produktu**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-160">**productId**</span></span><br/><span data-ttu-id="ecf9d-161">**productName**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-161">**productName**</span></span><br/><br/> <span data-ttu-id="ecf9d-162">Zwracane wiersze danych będą zawierać pola określone w parametrze *GroupBy* , a także następujące:</span><span class="sxs-lookup"><span data-stu-id="ecf9d-162">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="ecf9d-163">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-163">**licensesDeployed**</span></span><br/><span data-ttu-id="ecf9d-164">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="ecf9d-164">**licensesSold**</span></span>  | <span data-ttu-id="ecf9d-165">Nie</span><span class="sxs-lookup"><span data-stu-id="ecf9d-165">No</span></span> |
| <span data-ttu-id="ecf9d-166">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="ecf9d-166">processedDateTime</span></span> | <span data-ttu-id="ecf9d-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="ecf9d-167">DateTime</span></span> | <span data-ttu-id="ecf9d-168">Jeden może określać datę przetworzenia danych użycia.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-168">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="ecf9d-169">Wartość domyślna to najnowsza Data przetworzenia danych</span><span class="sxs-lookup"><span data-stu-id="ecf9d-169">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="ecf9d-170">Nie</span><span class="sxs-lookup"><span data-stu-id="ecf9d-170">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="ecf9d-171">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ecf9d-171">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ecf9d-172">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ecf9d-172">REST response</span></span>

<span data-ttu-id="ecf9d-173">Jeśli to się powiedzie, treść odpowiedzi zawiera następujące pola zawierające dane dotyczące wdrożonych licencji.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-173">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="ecf9d-174">Pole</span><span class="sxs-lookup"><span data-stu-id="ecf9d-174">Field</span></span>             | <span data-ttu-id="ecf9d-175">Typ</span><span class="sxs-lookup"><span data-stu-id="ecf9d-175">Type</span></span>     | <span data-ttu-id="ecf9d-176">Opis</span><span class="sxs-lookup"><span data-stu-id="ecf9d-176">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="ecf9d-177">Kod servicecode</span><span class="sxs-lookup"><span data-stu-id="ecf9d-177">serviceCode</span></span>       | <span data-ttu-id="ecf9d-178">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-178">string</span></span>   | <span data-ttu-id="ecf9d-179">Kod usługi</span><span class="sxs-lookup"><span data-stu-id="ecf9d-179">Service code</span></span>                          |
| <span data-ttu-id="ecf9d-180">serviceName</span><span class="sxs-lookup"><span data-stu-id="ecf9d-180">serviceName</span></span>       | <span data-ttu-id="ecf9d-181">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-181">string</span></span>   | <span data-ttu-id="ecf9d-182">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="ecf9d-182">Service name</span></span>                          |
| <span data-ttu-id="ecf9d-183">ukierunkowan</span><span class="sxs-lookup"><span data-stu-id="ecf9d-183">channel</span></span>           | <span data-ttu-id="ecf9d-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-184">string</span></span>   | <span data-ttu-id="ecf9d-185">Nazwa kanału, odsprzedawcy</span><span class="sxs-lookup"><span data-stu-id="ecf9d-185">Channel name, reseller</span></span>                |
| <span data-ttu-id="ecf9d-186">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="ecf9d-186">customerTenantId</span></span>  | <span data-ttu-id="ecf9d-187">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-187">string</span></span>   | <span data-ttu-id="ecf9d-188">Unikatowy identyfikator dla klienta</span><span class="sxs-lookup"><span data-stu-id="ecf9d-188">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="ecf9d-189">customerName</span><span class="sxs-lookup"><span data-stu-id="ecf9d-189">customerName</span></span>      | <span data-ttu-id="ecf9d-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-190">string</span></span>   | <span data-ttu-id="ecf9d-191">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="ecf9d-191">Customer name</span></span>                         |
| <span data-ttu-id="ecf9d-192">productId</span><span class="sxs-lookup"><span data-stu-id="ecf9d-192">productId</span></span>         | <span data-ttu-id="ecf9d-193">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-193">string</span></span>   | <span data-ttu-id="ecf9d-194">Unikatowy identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="ecf9d-194">Unique identifier for the product</span></span>     |
| <span data-ttu-id="ecf9d-195">productName</span><span class="sxs-lookup"><span data-stu-id="ecf9d-195">productName</span></span>       | <span data-ttu-id="ecf9d-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="ecf9d-196">string</span></span>   | <span data-ttu-id="ecf9d-197">Nazwa produktu</span><span class="sxs-lookup"><span data-stu-id="ecf9d-197">Product name</span></span>                          |
| <span data-ttu-id="ecf9d-198">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="ecf9d-198">licensesDeployed</span></span>  | <span data-ttu-id="ecf9d-199">długi</span><span class="sxs-lookup"><span data-stu-id="ecf9d-199">long</span></span>     | <span data-ttu-id="ecf9d-200">Liczba wdrożonych licencji</span><span class="sxs-lookup"><span data-stu-id="ecf9d-200">Number of licenses deployed</span></span>           |
| <span data-ttu-id="ecf9d-201">licensesSold</span><span class="sxs-lookup"><span data-stu-id="ecf9d-201">licensesSold</span></span>      | <span data-ttu-id="ecf9d-202">długi</span><span class="sxs-lookup"><span data-stu-id="ecf9d-202">long</span></span>     | <span data-ttu-id="ecf9d-203">Liczba sprzedanych licencji</span><span class="sxs-lookup"><span data-stu-id="ecf9d-203">Number of licenses sold</span></span>               |
| <span data-ttu-id="ecf9d-204">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="ecf9d-204">processedDateTime</span></span> | <span data-ttu-id="ecf9d-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="ecf9d-205">DateTime</span></span> | <span data-ttu-id="ecf9d-206">Data ostatniego przetworzenia danych</span><span class="sxs-lookup"><span data-stu-id="ecf9d-206">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ecf9d-207">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ecf9d-207">Response success and error codes</span></span>

<span data-ttu-id="ecf9d-208">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-208">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ecf9d-209">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ecf9d-209">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ecf9d-210">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ecf9d-210">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ecf9d-211">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ecf9d-211">Response example</span></span>

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
