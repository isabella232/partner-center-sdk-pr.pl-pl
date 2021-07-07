---
title: Pobieranie informacji dotyczących użycia licencji klienta
description: Jak uzyskać szczegółowe informacje o użyciu licencji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: cfec12d37ce4f5f50baad57bfd45770388f8a2dc
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446432"
---
# <a name="get-customer-licenses-usage-information"></a><span data-ttu-id="4a003-103">Pobieranie informacji dotyczących użycia licencji klienta</span><span class="sxs-lookup"><span data-stu-id="4a003-103">Get customer licenses usage information</span></span>

<span data-ttu-id="4a003-104">Jak uzyskać szczegółowe informacje o wdrażaniu licencji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="4a003-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="4a003-105">Ten scenariusz został wyzłoszony przez informacje [o użyciu funkcji Get licenses](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="4a003-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a003-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4a003-106">Prerequisites</span></span>

<span data-ttu-id="4a003-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4a003-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a003-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4a003-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="4a003-109">C\#</span><span class="sxs-lookup"><span data-stu-id="4a003-109">C\#</span></span>

<span data-ttu-id="4a003-110">Aby pobrać zagregowane dane dotyczące wdrożenia dla określonego klienta, najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="4a003-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4a003-111">Następnie pobierz interfejs do operacji zbierania danych analitycznych na poziomie klienta z [**właściwości Analytics.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics)</span><span class="sxs-lookup"><span data-stu-id="4a003-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="4a003-112">Następnie pobierz interfejs do kolekcji analizy licencji na poziomie klienta z [**właściwości Licencje.**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses)</span><span class="sxs-lookup"><span data-stu-id="4a003-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="4a003-113">Na koniec wywołaj [**metodę Usage.Get,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) aby uzyskać zagregowane dane dotyczące użycia licencji.</span><span class="sxs-lookup"><span data-stu-id="4a003-113">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="4a003-114">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**CustomerLicensesUsageInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights)</span><span class="sxs-lookup"><span data-stu-id="4a003-114">If the method succeeds, you'll get a collection of [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="4a003-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4a003-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a003-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4a003-116">Request syntax</span></span>

| <span data-ttu-id="4a003-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="4a003-117">Method</span></span>  | <span data-ttu-id="4a003-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4a003-118">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4a003-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="4a003-119">**GET**</span></span> | <span data-ttu-id="4a003-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/analytics/licenses/usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4a003-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4a003-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4a003-121">URI parameter</span></span>

<span data-ttu-id="4a003-122">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="4a003-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="4a003-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4a003-123">Name</span></span>        | <span data-ttu-id="4a003-124">Typ</span><span class="sxs-lookup"><span data-stu-id="4a003-124">Type</span></span> | <span data-ttu-id="4a003-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4a003-125">Required</span></span> | <span data-ttu-id="4a003-126">Opis</span><span class="sxs-lookup"><span data-stu-id="4a003-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="4a003-127">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="4a003-127">customer-id</span></span> | <span data-ttu-id="4a003-128">guid</span><span class="sxs-lookup"><span data-stu-id="4a003-128">guid</span></span> | <span data-ttu-id="4a003-129">Tak</span><span class="sxs-lookup"><span data-stu-id="4a003-129">Yes</span></span>      | <span data-ttu-id="4a003-130">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="4a003-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4a003-131">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4a003-131">Request headers</span></span>

<span data-ttu-id="4a003-132">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4a003-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4a003-133">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4a003-133">Request body</span></span>

<span data-ttu-id="4a003-134">Brak.</span><span class="sxs-lookup"><span data-stu-id="4a003-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4a003-135">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4a003-135">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4a003-136">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4a003-136">REST response</span></span>

<span data-ttu-id="4a003-137">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [CustomerLicensesUsageInsights,](analytics-resources.md#customerlicensesusageinsights) które zawierają informacje o użyciu licencji.</span><span class="sxs-lookup"><span data-stu-id="4a003-137">If successful, the response body contains a collection of [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) resources that provide information about licenses usage.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a003-138">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4a003-138">Response success and error codes</span></span>

<span data-ttu-id="4a003-139">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="4a003-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a003-140">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4a003-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a003-141">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4a003-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4a003-142">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4a003-142">Response example</span></span>

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
