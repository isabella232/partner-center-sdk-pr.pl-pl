---
title: Pobieranie informacji dotyczących wdrażania licencji
description: How to get deployment information for Office and Dynamics licenses (Jak uzyskać informacje o wdrażaniu Office licencji usługi Dynamics).
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445667"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="e2b61-103">Pobieranie informacji dotyczących wdrażania licencji</span><span class="sxs-lookup"><span data-stu-id="e2b61-103">Get licenses deployment information</span></span>

<span data-ttu-id="e2b61-104">How to get deployment information for Office and Dynamics licenses (Jak uzyskać informacje o wdrażaniu Office licencji usługi Dynamics).</span><span class="sxs-lookup"><span data-stu-id="e2b61-104">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2b61-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e2b61-105">Prerequisites</span></span>

<span data-ttu-id="e2b61-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e2b61-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e2b61-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e2b61-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e2b61-108">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e2b61-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e2b61-109">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e2b61-109">Request syntax</span></span>

| <span data-ttu-id="e2b61-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="e2b61-110">Method</span></span>  | <span data-ttu-id="e2b61-111">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e2b61-111">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e2b61-112">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e2b61-112">**GET**</span></span> | <span data-ttu-id="e2b61-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e2b61-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e2b61-114">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e2b61-114">Request headers</span></span>

<span data-ttu-id="e2b61-115">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e2b61-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="e2b61-116">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="e2b61-116">URI parameters</span></span>

| <span data-ttu-id="e2b61-117">Parametr</span><span class="sxs-lookup"><span data-stu-id="e2b61-117">Parameter</span></span>         | <span data-ttu-id="e2b61-118">Typ</span><span class="sxs-lookup"><span data-stu-id="e2b61-118">Type</span></span>     | <span data-ttu-id="e2b61-119">Opis</span><span class="sxs-lookup"><span data-stu-id="e2b61-119">Description</span></span> | <span data-ttu-id="e2b61-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e2b61-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="e2b61-121">top (pierwsze)</span><span class="sxs-lookup"><span data-stu-id="e2b61-121">top</span></span>               | <span data-ttu-id="e2b61-122">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-122">string</span></span>   | <span data-ttu-id="e2b61-123">Liczba wierszy danych do zwrócenia w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="e2b61-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="e2b61-124">Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000.</span><span class="sxs-lookup"><span data-stu-id="e2b61-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="e2b61-125">Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.</span><span class="sxs-lookup"><span data-stu-id="e2b61-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="e2b61-126">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b61-126">No</span></span> |
| <span data-ttu-id="e2b61-127">Pomiń</span><span class="sxs-lookup"><span data-stu-id="e2b61-127">skip</span></span>              | <span data-ttu-id="e2b61-128">int</span><span class="sxs-lookup"><span data-stu-id="e2b61-128">int</span></span>      | <span data-ttu-id="e2b61-129">Liczba wierszy do pominięcia w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="e2b61-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="e2b61-130">Ten parametr umożliwia stronicować duże zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="e2b61-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="e2b61-131">Na przykład wartości top=10000 i skip=0 pobierają pierwsze 10000 wierszy danych, top=10000, a skip=10000 pobiera następne 10000 wierszy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e2b61-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="e2b61-132">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b61-132">No</span></span> |
| <span data-ttu-id="e2b61-133">filter</span><span class="sxs-lookup"><span data-stu-id="e2b61-133">filter</span></span>            | <span data-ttu-id="e2b61-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-134">string</span></span>   | <span data-ttu-id="e2b61-135">Parametr *filter* żądania zawiera co najmniej jedną instrukcje filtrują wiersze w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e2b61-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="e2b61-136">Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje mogą być łączone przy `eq` `ne` użyciu lub `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="e2b61-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="e2b61-137">Oto kilka przykładowych *parametrów filtru:*</span><span class="sxs-lookup"><span data-stu-id="e2b61-137">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="e2b61-138">*filter=serviceCode eq 'O365'*</span><span class="sxs-lookup"><span data-stu-id="e2b61-138">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="e2b61-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="e2b61-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="e2b61-140">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="e2b61-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="e2b61-141">**kod usługi**</span><span class="sxs-lookup"><span data-stu-id="e2b61-141">**serviceCode**</span></span><br/><span data-ttu-id="e2b61-142">**Servicename**</span><span class="sxs-lookup"><span data-stu-id="e2b61-142">**serviceName**</span></span><br/><span data-ttu-id="e2b61-143">**Kanał**</span><span class="sxs-lookup"><span data-stu-id="e2b61-143">**channel**</span></span><br/><span data-ttu-id="e2b61-144">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="e2b61-144">**customerTenantId**</span></span><br/><span data-ttu-id="e2b61-145">**Customername**</span><span class="sxs-lookup"><span data-stu-id="e2b61-145">**customerName**</span></span><br/><span data-ttu-id="e2b61-146">**Productid**</span><span class="sxs-lookup"><span data-stu-id="e2b61-146">**productId**</span></span><br/><span data-ttu-id="e2b61-147">**Productname**</span><span class="sxs-lookup"><span data-stu-id="e2b61-147">**productName**</span></span>  | <span data-ttu-id="e2b61-148">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b61-148">No</span></span> |
| <span data-ttu-id="e2b61-149">Groupby</span><span class="sxs-lookup"><span data-stu-id="e2b61-149">groupby</span></span>           | <span data-ttu-id="e2b61-150">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-150">string</span></span>   | <span data-ttu-id="e2b61-151">Instrukcja, która stosuje agregację danych tylko do określonych pól.</span><span class="sxs-lookup"><span data-stu-id="e2b61-151">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="e2b61-152">Można określić następujące pola:</span><span class="sxs-lookup"><span data-stu-id="e2b61-152">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="e2b61-153">**kod usługi**</span><span class="sxs-lookup"><span data-stu-id="e2b61-153">**serviceCode**</span></span><br/><span data-ttu-id="e2b61-154">**Servicename**</span><span class="sxs-lookup"><span data-stu-id="e2b61-154">**serviceName**</span></span><br/><span data-ttu-id="e2b61-155">**Kanał**</span><span class="sxs-lookup"><span data-stu-id="e2b61-155">**channel**</span></span><br/><span data-ttu-id="e2b61-156">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="e2b61-156">**customerTenantId**</span></span><br/><span data-ttu-id="e2b61-157">**Customername**</span><span class="sxs-lookup"><span data-stu-id="e2b61-157">**customerName**</span></span><br/><span data-ttu-id="e2b61-158">**Productid**</span><span class="sxs-lookup"><span data-stu-id="e2b61-158">**productId**</span></span><br/><span data-ttu-id="e2b61-159">**Productname**</span><span class="sxs-lookup"><span data-stu-id="e2b61-159">**productName**</span></span><br/><br/> <span data-ttu-id="e2b61-160">Zwrócone wiersze danych będą zawierać pola określone w parametrze *grupowania* i następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e2b61-160">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="e2b61-161">**licencjeWdeployed**</span><span class="sxs-lookup"><span data-stu-id="e2b61-161">**licensesDeployed**</span></span><br/><span data-ttu-id="e2b61-162">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="e2b61-162">**licensesSold**</span></span>  | <span data-ttu-id="e2b61-163">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b61-163">No</span></span> |
| <span data-ttu-id="e2b61-164">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="e2b61-164">processedDateTime</span></span> | <span data-ttu-id="e2b61-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="e2b61-165">DateTime</span></span> | <span data-ttu-id="e2b61-166">Można określić datę przetwarzania danych użycia.</span><span class="sxs-lookup"><span data-stu-id="e2b61-166">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="e2b61-167">Wartość domyślna to najpóźniejsza data przetwarzania danych</span><span class="sxs-lookup"><span data-stu-id="e2b61-167">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="e2b61-168">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b61-168">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="e2b61-169">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e2b61-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e2b61-170">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e2b61-170">REST response</span></span>

<span data-ttu-id="e2b61-171">W przypadku powodzenia treść odpowiedzi zawiera następujące pola zawierające dane dotyczące wdrożonych licencji.</span><span class="sxs-lookup"><span data-stu-id="e2b61-171">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="e2b61-172">Pole</span><span class="sxs-lookup"><span data-stu-id="e2b61-172">Field</span></span>             | <span data-ttu-id="e2b61-173">Typ</span><span class="sxs-lookup"><span data-stu-id="e2b61-173">Type</span></span>     | <span data-ttu-id="e2b61-174">Opis</span><span class="sxs-lookup"><span data-stu-id="e2b61-174">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="e2b61-175">kod usługi</span><span class="sxs-lookup"><span data-stu-id="e2b61-175">serviceCode</span></span>       | <span data-ttu-id="e2b61-176">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-176">string</span></span>   | <span data-ttu-id="e2b61-177">Kod usługi</span><span class="sxs-lookup"><span data-stu-id="e2b61-177">Service code</span></span>                          |
| <span data-ttu-id="e2b61-178">Servicename</span><span class="sxs-lookup"><span data-stu-id="e2b61-178">serviceName</span></span>       | <span data-ttu-id="e2b61-179">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-179">string</span></span>   | <span data-ttu-id="e2b61-180">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="e2b61-180">Service name</span></span>                          |
| <span data-ttu-id="e2b61-181">Kanał</span><span class="sxs-lookup"><span data-stu-id="e2b61-181">channel</span></span>           | <span data-ttu-id="e2b61-182">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-182">string</span></span>   | <span data-ttu-id="e2b61-183">Nazwa kanału, odsprzedawca</span><span class="sxs-lookup"><span data-stu-id="e2b61-183">Channel name, reseller</span></span>                |
| <span data-ttu-id="e2b61-184">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="e2b61-184">customerTenantId</span></span>  | <span data-ttu-id="e2b61-185">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-185">string</span></span>   | <span data-ttu-id="e2b61-186">Unikatowy identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="e2b61-186">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="e2b61-187">Customername</span><span class="sxs-lookup"><span data-stu-id="e2b61-187">customerName</span></span>      | <span data-ttu-id="e2b61-188">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-188">string</span></span>   | <span data-ttu-id="e2b61-189">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="e2b61-189">Customer name</span></span>                         |
| <span data-ttu-id="e2b61-190">productId</span><span class="sxs-lookup"><span data-stu-id="e2b61-190">productId</span></span>         | <span data-ttu-id="e2b61-191">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-191">string</span></span>   | <span data-ttu-id="e2b61-192">Unikatowy identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="e2b61-192">Unique identifier for the product</span></span>     |
| <span data-ttu-id="e2b61-193">Productname</span><span class="sxs-lookup"><span data-stu-id="e2b61-193">productName</span></span>       | <span data-ttu-id="e2b61-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="e2b61-194">string</span></span>   | <span data-ttu-id="e2b61-195">Nazwa produktu</span><span class="sxs-lookup"><span data-stu-id="e2b61-195">Product name</span></span>                          |
| <span data-ttu-id="e2b61-196">licencjeWdeployed</span><span class="sxs-lookup"><span data-stu-id="e2b61-196">licensesDeployed</span></span>  | <span data-ttu-id="e2b61-197">długi</span><span class="sxs-lookup"><span data-stu-id="e2b61-197">long</span></span>     | <span data-ttu-id="e2b61-198">Liczba wdrożonych licencji</span><span class="sxs-lookup"><span data-stu-id="e2b61-198">Number of licenses deployed</span></span>           |
| <span data-ttu-id="e2b61-199">licensesSold</span><span class="sxs-lookup"><span data-stu-id="e2b61-199">licensesSold</span></span>      | <span data-ttu-id="e2b61-200">długi</span><span class="sxs-lookup"><span data-stu-id="e2b61-200">long</span></span>     | <span data-ttu-id="e2b61-201">Liczba sprzedanych licencji</span><span class="sxs-lookup"><span data-stu-id="e2b61-201">Number of licenses sold</span></span>               |
| <span data-ttu-id="e2b61-202">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="e2b61-202">processedDateTime</span></span> | <span data-ttu-id="e2b61-203">DateTime</span><span class="sxs-lookup"><span data-stu-id="e2b61-203">DateTime</span></span> | <span data-ttu-id="e2b61-204">Data ostatniego przetworzenia danych</span><span class="sxs-lookup"><span data-stu-id="e2b61-204">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e2b61-205">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e2b61-205">Response success and error codes</span></span>

<span data-ttu-id="e2b61-206">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e2b61-206">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e2b61-207">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e2b61-207">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e2b61-208">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e2b61-208">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e2b61-209">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e2b61-209">Response example</span></span>

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
