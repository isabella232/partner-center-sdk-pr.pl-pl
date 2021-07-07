---
title: Pobieranie informacji dotyczących użycia licencji
description: Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla usług Office i Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445984"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="ac055-103">Pobieranie informacji dotyczących użycia licencji</span><span class="sxs-lookup"><span data-stu-id="ac055-103">Get licenses usage information</span></span>

<span data-ttu-id="ac055-104">Jak uzyskać informacje o użyciu licencji na poziomie obciążenia dla usług Office i Dynamics.</span><span class="sxs-lookup"><span data-stu-id="ac055-104">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac055-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac055-105">Prerequisites</span></span>

<span data-ttu-id="ac055-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ac055-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ac055-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac055-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ac055-108">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ac055-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ac055-109">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ac055-109">Request syntax</span></span>

| <span data-ttu-id="ac055-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="ac055-110">Method</span></span>  | <span data-ttu-id="ac055-111">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ac055-111">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="ac055-112">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="ac055-112">**GET**</span></span> | <span data-ttu-id="ac055-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ac055-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ac055-114">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ac055-114">Request headers</span></span>

<span data-ttu-id="ac055-115">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ac055-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="ac055-116">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="ac055-116">URI parameters</span></span>

| <span data-ttu-id="ac055-117">Parametr</span><span class="sxs-lookup"><span data-stu-id="ac055-117">Parameter</span></span>         | <span data-ttu-id="ac055-118">Typ</span><span class="sxs-lookup"><span data-stu-id="ac055-118">Type</span></span>     | <span data-ttu-id="ac055-119">Opis</span><span class="sxs-lookup"><span data-stu-id="ac055-119">Description</span></span> | <span data-ttu-id="ac055-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ac055-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="ac055-121">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="ac055-121">top</span></span>               | <span data-ttu-id="ac055-122">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-122">string</span></span>   | <span data-ttu-id="ac055-123">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="ac055-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="ac055-124">Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000.</span><span class="sxs-lookup"><span data-stu-id="ac055-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="ac055-125">Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="ac055-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="ac055-126">Nie</span><span class="sxs-lookup"><span data-stu-id="ac055-126">No</span></span> |
| <span data-ttu-id="ac055-127">Pomiń</span><span class="sxs-lookup"><span data-stu-id="ac055-127">skip</span></span>              | <span data-ttu-id="ac055-128">int</span><span class="sxs-lookup"><span data-stu-id="ac055-128">int</span></span>      | <span data-ttu-id="ac055-129">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="ac055-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="ac055-130">Ten parametr umożliwia stronicować duże zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="ac055-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="ac055-131">Na przykład wartości top=10000 i skip=0 pobierają pierwsze 10000 wierszy danych, top=10000, a skip=10000 pobiera następne 10000 wierszy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ac055-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="ac055-132">Nie</span><span class="sxs-lookup"><span data-stu-id="ac055-132">No</span></span> |
| <span data-ttu-id="ac055-133">filter</span><span class="sxs-lookup"><span data-stu-id="ac055-133">filter</span></span>            | <span data-ttu-id="ac055-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-134">string</span></span>   | <span data-ttu-id="ac055-135">Parametr *filter* żądania zawiera co najmniej jedną instrukcje filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ac055-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="ac055-136">Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje mogą być łączone przy **`eq`** **`ne`** użyciu lub **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="ac055-136">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="ac055-137">Oto kilka przykładowych *parametrów filtru:*</span><span class="sxs-lookup"><span data-stu-id="ac055-137">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="ac055-138">*filter=workloadCode eq 'SFB'*</span><span class="sxs-lookup"><span data-stu-id="ac055-138">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="ac055-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="ac055-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="ac055-140">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="ac055-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="ac055-141">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="ac055-141">**workloadCode**</span></span><br/><span data-ttu-id="ac055-142">**nazwa_obciążenia**</span><span class="sxs-lookup"><span data-stu-id="ac055-142">**workloadName**</span></span><br/><span data-ttu-id="ac055-143">**kod usługi**</span><span class="sxs-lookup"><span data-stu-id="ac055-143">**serviceCode**</span></span><br/><span data-ttu-id="ac055-144">**Servicename**</span><span class="sxs-lookup"><span data-stu-id="ac055-144">**serviceName**</span></span><br/><span data-ttu-id="ac055-145">**Kanał**</span><span class="sxs-lookup"><span data-stu-id="ac055-145">**channel**</span></span><br/><span data-ttu-id="ac055-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="ac055-146">**customerTenantId**</span></span><br/><span data-ttu-id="ac055-147">**Customername**</span><span class="sxs-lookup"><span data-stu-id="ac055-147">**customerName**</span></span><br/><span data-ttu-id="ac055-148">**Productid**</span><span class="sxs-lookup"><span data-stu-id="ac055-148">**productId**</span></span><br/><span data-ttu-id="ac055-149">**Productname**</span><span class="sxs-lookup"><span data-stu-id="ac055-149">**productName**</span></span> | <span data-ttu-id="ac055-150">Nie</span><span class="sxs-lookup"><span data-stu-id="ac055-150">No</span></span> |
| <span data-ttu-id="ac055-151">Groupby</span><span class="sxs-lookup"><span data-stu-id="ac055-151">groupby</span></span>           | <span data-ttu-id="ac055-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-152">string</span></span>   | <span data-ttu-id="ac055-153">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="ac055-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="ac055-154">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="ac055-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="ac055-155">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="ac055-155">**workloadCode**</span></span><br/><span data-ttu-id="ac055-156">**nazwa_obciążenia**</span><span class="sxs-lookup"><span data-stu-id="ac055-156">**workloadName**</span></span><br/><span data-ttu-id="ac055-157">**kod usługi**</span><span class="sxs-lookup"><span data-stu-id="ac055-157">**serviceCode**</span></span><br/><span data-ttu-id="ac055-158">**Servicename**</span><span class="sxs-lookup"><span data-stu-id="ac055-158">**serviceName**</span></span><br/><span data-ttu-id="ac055-159">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="ac055-159">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="ac055-160">**Customername**</span><span class="sxs-lookup"><span data-stu-id="ac055-160">**customerName**</span></span><br/><span data-ttu-id="ac055-161">**Productid**</span><span class="sxs-lookup"><span data-stu-id="ac055-161">**productId**</span></span><br/><span data-ttu-id="ac055-162">**Productname**</span><span class="sxs-lookup"><span data-stu-id="ac055-162">**productName**</span></span><br/><br/><span data-ttu-id="ac055-163">Zwrócone wiersze danych będą zawierać pola określone w parametrze *grupowania* i następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ac055-163">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="ac055-164">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="ac055-164">**licensesActive**</span></span><br/><span data-ttu-id="ac055-165">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="ac055-165">**licensesQualified**</span></span> | <span data-ttu-id="ac055-166">Nie</span><span class="sxs-lookup"><span data-stu-id="ac055-166">No</span></span> |
| <span data-ttu-id="ac055-167">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="ac055-167">processedDateTime</span></span> | <span data-ttu-id="ac055-168">DateTime</span><span class="sxs-lookup"><span data-stu-id="ac055-168">DateTime</span></span> | <span data-ttu-id="ac055-169">Można określić datę przetwarzania danych użycia.</span><span class="sxs-lookup"><span data-stu-id="ac055-169">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="ac055-170">Wartość domyślna to najpóźniejsza data przetwarzania danych</span><span class="sxs-lookup"><span data-stu-id="ac055-170">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="ac055-171">Nie</span><span class="sxs-lookup"><span data-stu-id="ac055-171">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="ac055-172">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ac055-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ac055-173">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ac055-173">REST response</span></span>

<span data-ttu-id="ac055-174">W przypadku powodzenia treść odpowiedzi zawiera następujące pola zawierające dane dotyczące użycia licencji.</span><span class="sxs-lookup"><span data-stu-id="ac055-174">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="ac055-175">Pole</span><span class="sxs-lookup"><span data-stu-id="ac055-175">Field</span></span>             | <span data-ttu-id="ac055-176">Typ</span><span class="sxs-lookup"><span data-stu-id="ac055-176">Type</span></span>     | <span data-ttu-id="ac055-177">Opis</span><span class="sxs-lookup"><span data-stu-id="ac055-177">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="ac055-178">workloadCode</span><span class="sxs-lookup"><span data-stu-id="ac055-178">workloadCode</span></span>      | <span data-ttu-id="ac055-179">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-179">string</span></span>   | <span data-ttu-id="ac055-180">Kod obciążenia</span><span class="sxs-lookup"><span data-stu-id="ac055-180">Workload code</span></span>                                 |
| <span data-ttu-id="ac055-181">nazwa_obciążenia</span><span class="sxs-lookup"><span data-stu-id="ac055-181">workloadName</span></span>      | <span data-ttu-id="ac055-182">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-182">string</span></span>   | <span data-ttu-id="ac055-183">Nazwa obciążenia</span><span class="sxs-lookup"><span data-stu-id="ac055-183">Workload name</span></span>                                 |
| <span data-ttu-id="ac055-184">kod usługi</span><span class="sxs-lookup"><span data-stu-id="ac055-184">serviceCode</span></span>       | <span data-ttu-id="ac055-185">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-185">string</span></span>   | <span data-ttu-id="ac055-186">Kod usługi</span><span class="sxs-lookup"><span data-stu-id="ac055-186">Service code</span></span>                                  |
| <span data-ttu-id="ac055-187">Servicename</span><span class="sxs-lookup"><span data-stu-id="ac055-187">serviceName</span></span>       | <span data-ttu-id="ac055-188">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-188">string</span></span>   | <span data-ttu-id="ac055-189">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="ac055-189">Service name</span></span>                                  |
| <span data-ttu-id="ac055-190">Kanał</span><span class="sxs-lookup"><span data-stu-id="ac055-190">channel</span></span>           | <span data-ttu-id="ac055-191">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-191">string</span></span>   | <span data-ttu-id="ac055-192">Nazwa kanału, odsprzedawca</span><span class="sxs-lookup"><span data-stu-id="ac055-192">Channel name, reseller</span></span>                        |
| <span data-ttu-id="ac055-193">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="ac055-193">customerTenantId</span></span>  | <span data-ttu-id="ac055-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-194">string</span></span>   | <span data-ttu-id="ac055-195">Unikatowy identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="ac055-195">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="ac055-196">Customername</span><span class="sxs-lookup"><span data-stu-id="ac055-196">customerName</span></span>      | <span data-ttu-id="ac055-197">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-197">string</span></span>   | <span data-ttu-id="ac055-198">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="ac055-198">Customer name</span></span>                                 |
| <span data-ttu-id="ac055-199">productId</span><span class="sxs-lookup"><span data-stu-id="ac055-199">productId</span></span>         | <span data-ttu-id="ac055-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-200">string</span></span>   | <span data-ttu-id="ac055-201">Unikatowy identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="ac055-201">Unique identifier for the product</span></span>             |
| <span data-ttu-id="ac055-202">Productname</span><span class="sxs-lookup"><span data-stu-id="ac055-202">productName</span></span>       | <span data-ttu-id="ac055-203">ciąg</span><span class="sxs-lookup"><span data-stu-id="ac055-203">string</span></span>   | <span data-ttu-id="ac055-204">Nazwa produktu</span><span class="sxs-lookup"><span data-stu-id="ac055-204">Product name</span></span>                                  |
| <span data-ttu-id="ac055-205">licensesActive</span><span class="sxs-lookup"><span data-stu-id="ac055-205">licensesActive</span></span>    | <span data-ttu-id="ac055-206">długi</span><span class="sxs-lookup"><span data-stu-id="ac055-206">long</span></span>     | <span data-ttu-id="ac055-207">Liczba aktywnych licencji na obciążenie</span><span class="sxs-lookup"><span data-stu-id="ac055-207">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="ac055-208">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="ac055-208">licensesQualified</span></span> | <span data-ttu-id="ac055-209">długi</span><span class="sxs-lookup"><span data-stu-id="ac055-209">long</span></span>     | <span data-ttu-id="ac055-210">Liczba kwalifikowanych licencji dla obciążenia</span><span class="sxs-lookup"><span data-stu-id="ac055-210">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="ac055-211">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="ac055-211">processedDateTime</span></span> | <span data-ttu-id="ac055-212">DateTime</span><span class="sxs-lookup"><span data-stu-id="ac055-212">DateTime</span></span> | <span data-ttu-id="ac055-213">Data ostatniego przetworzenia danych</span><span class="sxs-lookup"><span data-stu-id="ac055-213">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ac055-214">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ac055-214">Response success and error codes</span></span>

<span data-ttu-id="ac055-215">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ac055-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ac055-216">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ac055-216">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ac055-217">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ac055-217">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ac055-218">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ac055-218">Response example</span></span>

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
