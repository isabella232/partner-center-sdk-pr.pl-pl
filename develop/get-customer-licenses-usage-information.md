---
title: Pobieranie informacji dotyczących użycia licencji klienta
description: Jak uzyskać szczegółowe informacje dotyczące użycia licencji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1ee19e458ec65faa21034dd230b5388f7de981b2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768346"
---
# <a name="get-customer-licenses-usage-information"></a><span data-ttu-id="fb142-103">Pobieranie informacji dotyczących użycia licencji klienta</span><span class="sxs-lookup"><span data-stu-id="fb142-103">Get customer licenses usage information</span></span>

<span data-ttu-id="fb142-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="fb142-104">**Applies To**</span></span>

- <span data-ttu-id="fb142-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fb142-105">Partner Center</span></span>

<span data-ttu-id="fb142-106">Jak uzyskać szczegółowe informacje o wdrażaniu licencji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="fb142-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="fb142-107">Ten scenariusz jest zastąpiony przez [uzyskanie informacji o użyciu licencji](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="fb142-107">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb142-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fb142-108">Prerequisites</span></span>

<span data-ttu-id="fb142-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fb142-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fb142-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fb142-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="fb142-111">C\#</span><span class="sxs-lookup"><span data-stu-id="fb142-111">C\#</span></span>

<span data-ttu-id="fb142-112">Aby pobrać zagregowane dane dotyczące wdrożenia określonego klienta, najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="fb142-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="fb142-113">Następnie uzyskaj interfejs do operacji zbierania danych analitycznych na poziomie klienta z właściwości [**Analiza**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) .</span><span class="sxs-lookup"><span data-stu-id="fb142-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="fb142-114">Następnie Pobierz interfejs do kolekcji do analizy licencji na poziomie klienta z właściwości [**licencje**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="fb142-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="fb142-115">Na koniec Wywołaj metodę [**Usage. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , aby uzyskać zagregowane dane dotyczące użycia licencji.</span><span class="sxs-lookup"><span data-stu-id="fb142-115">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="fb142-116">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) .</span><span class="sxs-lookup"><span data-stu-id="fb142-116">If the method succeeds you'll get a collection of [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="fb142-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fb142-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fb142-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fb142-118">Request syntax</span></span>

| <span data-ttu-id="fb142-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="fb142-119">Method</span></span>  | <span data-ttu-id="fb142-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fb142-120">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fb142-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fb142-121">**GET**</span></span> | <span data-ttu-id="fb142-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Analytics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="fb142-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fb142-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fb142-123">URI parameter</span></span>

<span data-ttu-id="fb142-124">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="fb142-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="fb142-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fb142-125">Name</span></span>        | <span data-ttu-id="fb142-126">Typ</span><span class="sxs-lookup"><span data-stu-id="fb142-126">Type</span></span> | <span data-ttu-id="fb142-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fb142-127">Required</span></span> | <span data-ttu-id="fb142-128">Opis</span><span class="sxs-lookup"><span data-stu-id="fb142-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="fb142-129">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="fb142-129">customer-id</span></span> | <span data-ttu-id="fb142-130">guid</span><span class="sxs-lookup"><span data-stu-id="fb142-130">guid</span></span> | <span data-ttu-id="fb142-131">Tak</span><span class="sxs-lookup"><span data-stu-id="fb142-131">Yes</span></span>      | <span data-ttu-id="fb142-132">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="fb142-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fb142-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fb142-133">Request headers</span></span>

<span data-ttu-id="fb142-134">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fb142-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fb142-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fb142-135">Request body</span></span>

<span data-ttu-id="fb142-136">Brak.</span><span class="sxs-lookup"><span data-stu-id="fb142-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fb142-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fb142-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="fb142-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fb142-138">REST response</span></span>

<span data-ttu-id="fb142-139">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) , które zawierają informacje o użyciu licencji.</span><span class="sxs-lookup"><span data-stu-id="fb142-139">If successful, the response body contains a collection of [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) resources that provide information about licenses usage.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fb142-140">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fb142-140">Response success and error codes</span></span>

<span data-ttu-id="fb142-141">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="fb142-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fb142-142">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fb142-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fb142-143">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fb142-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fb142-144">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fb142-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1726
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CV: 0mufM0K1kEOoR7oI.0
MS-ServerId: 030020525
Date: Wed, 15 Mar 2017 01:19:58 GMT

{
    "totalCount": 5,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesActive": 0,
            "licensesQualified": 5,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesActive": 0,
            "licensesQualified": 2,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
