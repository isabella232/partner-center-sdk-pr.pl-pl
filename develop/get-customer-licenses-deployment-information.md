---
title: Pobieranie informacji dotyczących wdrażania licencji klienta
description: Jak uzyskać szczegółowe informacje o wdrażaniu licencji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 91fe9da185aa59025d4dc8263257b207edb4a5be
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446466"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="d442f-103">Pobieranie informacji dotyczących wdrażania licencji klienta</span><span class="sxs-lookup"><span data-stu-id="d442f-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="d442f-104">Jak uzyskać szczegółowe informacje o wdrażaniu licencji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="d442f-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="d442f-105">Ten scenariusz jest przesłoowany przez uzyskiwanie [informacji o wdrożeniu licencji.](get-licenses-deployment-information.md)</span><span class="sxs-lookup"><span data-stu-id="d442f-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d442f-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d442f-106">Prerequisites</span></span>

<span data-ttu-id="d442f-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d442f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d442f-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d442f-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d442f-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d442f-109">C\#</span></span>

<span data-ttu-id="d442f-110">Aby pobrać zagregowane dane dotyczące wdrożenia dla określonego klienta, najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="d442f-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="d442f-111">Następnie uzyskaj interfejs do operacji zbierania danych analitycznych na poziomie klienta z [**właściwości**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) Analytics.</span><span class="sxs-lookup"><span data-stu-id="d442f-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="d442f-112">Następnie pobierz interfejs do kolekcji analizy licencji na poziomie klienta z [**właściwości Licencje.**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses)</span><span class="sxs-lookup"><span data-stu-id="d442f-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="d442f-113">Na koniec wywołaj [**metodę Deployment.Get,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) aby uzyskać zagregowane dane dotyczące wdrożenia licencji.</span><span class="sxs-lookup"><span data-stu-id="d442f-113">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="d442f-114">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**CustomerLicensesDeploymentInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights)</span><span class="sxs-lookup"><span data-stu-id="d442f-114">If the method succeeds, you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="d442f-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d442f-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d442f-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d442f-116">Request syntax</span></span>

| <span data-ttu-id="d442f-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="d442f-117">Method</span></span>  | <span data-ttu-id="d442f-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d442f-118">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d442f-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d442f-119">**GET**</span></span> | <span data-ttu-id="d442f-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d442f-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d442f-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d442f-121">URI parameter</span></span>

<span data-ttu-id="d442f-122">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="d442f-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="d442f-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d442f-123">Name</span></span>        | <span data-ttu-id="d442f-124">Typ</span><span class="sxs-lookup"><span data-stu-id="d442f-124">Type</span></span> | <span data-ttu-id="d442f-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d442f-125">Required</span></span> | <span data-ttu-id="d442f-126">Opis</span><span class="sxs-lookup"><span data-stu-id="d442f-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="d442f-127">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="d442f-127">customer-id</span></span> | <span data-ttu-id="d442f-128">guid</span><span class="sxs-lookup"><span data-stu-id="d442f-128">guid</span></span> | <span data-ttu-id="d442f-129">Tak</span><span class="sxs-lookup"><span data-stu-id="d442f-129">Yes</span></span>      | <span data-ttu-id="d442f-130">Identyfikator klienta sformatowany w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="d442f-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d442f-131">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d442f-131">Request headers</span></span>

<span data-ttu-id="d442f-132">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d442f-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d442f-133">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d442f-133">Request body</span></span>

<span data-ttu-id="d442f-134">Brak.</span><span class="sxs-lookup"><span data-stu-id="d442f-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d442f-135">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d442f-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d442f-136">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d442f-136">REST response</span></span>

<span data-ttu-id="d442f-137">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [CustomerLicensesDeploymentInsights,](analytics-resources.md#customerlicensesdeploymentinsights) które zawierają informacje o wdrożonych licencjach.</span><span class="sxs-lookup"><span data-stu-id="d442f-137">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d442f-138">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d442f-138">Response success and error codes</span></span>

<span data-ttu-id="d442f-139">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d442f-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d442f-140">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d442f-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d442f-141">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d442f-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d442f-142">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d442f-142">Response example</span></span>

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
