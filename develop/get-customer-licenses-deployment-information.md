---
title: Pobieranie informacji dotyczących wdrażania licencji klienta
description: Jak uzyskać szczegółowe informacje o wdrażaniu licencji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3a39c6c908048305ff2dabf85a29d7ddc3628500
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768445"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="c98f3-103">Pobieranie informacji dotyczących wdrażania licencji klienta</span><span class="sxs-lookup"><span data-stu-id="c98f3-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="c98f3-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="c98f3-104">**Applies To**</span></span>

- <span data-ttu-id="c98f3-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c98f3-105">Partner Center</span></span>

<span data-ttu-id="c98f3-106">Jak uzyskać szczegółowe informacje o wdrażaniu licencji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="c98f3-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="c98f3-107">Ten scenariusz został zastąpiony przez [uzyskanie informacji o wdrożeniu licencji](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="c98f3-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c98f3-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c98f3-108">Prerequisites</span></span>

<span data-ttu-id="c98f3-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c98f3-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c98f3-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c98f3-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="c98f3-111">C\#</span><span class="sxs-lookup"><span data-stu-id="c98f3-111">C\#</span></span>

<span data-ttu-id="c98f3-112">Aby pobrać zagregowane dane dotyczące wdrożenia określonego klienta, najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="c98f3-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="c98f3-113">Następnie uzyskaj interfejs do operacji zbierania danych analitycznych na poziomie klienta z właściwości [**Analiza**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) .</span><span class="sxs-lookup"><span data-stu-id="c98f3-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="c98f3-114">Następnie Pobierz interfejs do kolekcji do analizy licencji na poziomie klienta z właściwości [**licencje**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="c98f3-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="c98f3-115">Na koniec Wywołaj metodę [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , aby uzyskać zagregowane dane dotyczące wdrożenia licencji.</span><span class="sxs-lookup"><span data-stu-id="c98f3-115">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="c98f3-116">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) .</span><span class="sxs-lookup"><span data-stu-id="c98f3-116">If the method succeeds you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="c98f3-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c98f3-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c98f3-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c98f3-118">Request syntax</span></span>

| <span data-ttu-id="c98f3-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="c98f3-119">Method</span></span>  | <span data-ttu-id="c98f3-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c98f3-120">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c98f3-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c98f3-121">**GET**</span></span> | <span data-ttu-id="c98f3-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Analytics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="c98f3-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c98f3-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c98f3-123">URI parameter</span></span>

<span data-ttu-id="c98f3-124">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="c98f3-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="c98f3-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c98f3-125">Name</span></span>        | <span data-ttu-id="c98f3-126">Typ</span><span class="sxs-lookup"><span data-stu-id="c98f3-126">Type</span></span> | <span data-ttu-id="c98f3-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c98f3-127">Required</span></span> | <span data-ttu-id="c98f3-128">Opis</span><span class="sxs-lookup"><span data-stu-id="c98f3-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="c98f3-129">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="c98f3-129">customer-id</span></span> | <span data-ttu-id="c98f3-130">guid</span><span class="sxs-lookup"><span data-stu-id="c98f3-130">guid</span></span> | <span data-ttu-id="c98f3-131">Tak</span><span class="sxs-lookup"><span data-stu-id="c98f3-131">Yes</span></span>      | <span data-ttu-id="c98f3-132">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="c98f3-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c98f3-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c98f3-133">Request headers</span></span>

<span data-ttu-id="c98f3-134">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c98f3-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c98f3-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c98f3-135">Request body</span></span>

<span data-ttu-id="c98f3-136">Brak.</span><span class="sxs-lookup"><span data-stu-id="c98f3-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c98f3-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c98f3-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c98f3-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c98f3-138">REST response</span></span>

<span data-ttu-id="c98f3-139">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) , które zawierają informacje na temat wdrożonych licencji.</span><span class="sxs-lookup"><span data-stu-id="c98f3-139">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c98f3-140">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c98f3-140">Response success and error codes</span></span>

<span data-ttu-id="c98f3-141">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="c98f3-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c98f3-142">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c98f3-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c98f3-143">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c98f3-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c98f3-144">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c98f3-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
