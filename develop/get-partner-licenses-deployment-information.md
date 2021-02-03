---
title: Pobieranie informacji dotyczących wdrażania licencji partnera
description: Jak uzyskać informacje o wdrożeniu licencji partnerów zagregowane w celu uwzględnienia wszystkich klientów.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768433"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="1a4fc-103">Pobieranie informacji dotyczących wdrażania licencji partnera</span><span class="sxs-lookup"><span data-stu-id="1a4fc-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="1a4fc-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="1a4fc-104">**Applies To**</span></span>

- <span data-ttu-id="1a4fc-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="1a4fc-105">Partner Center</span></span>

<span data-ttu-id="1a4fc-106">Jak uzyskać informacje o wdrożeniu licencji partnerów zagregowane w celu uwzględnienia wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-106">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="1a4fc-107">Ten scenariusz został zastąpiony przez [uzyskanie informacji o wdrożeniu licencji](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fc-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a4fc-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a4fc-108">Prerequisites</span></span>

<span data-ttu-id="1a4fc-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fc-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a4fc-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1a4fc-111">C\#</span><span class="sxs-lookup"><span data-stu-id="1a4fc-111">C\#</span></span>

<span data-ttu-id="1a4fc-112">Aby pobrać zagregowane dane dotyczące wdrożenia licencji, należy najpierw pobrać interfejs do operacji zbierania danych analitycznych na poziomie partnera ze [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="1a4fc-113">Następnie można pobrać interfejs do kolekcji analizy licencji poziomu partnera z właściwości [**licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="1a4fc-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="1a4fc-114">Na koniec Wywołaj metodę [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , aby uzyskać zagregowane dane dotyczące wdrożenia licencji.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-114">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="1a4fc-115">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) .</span><span class="sxs-lookup"><span data-stu-id="1a4fc-115">If the method succeeds you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="1a4fc-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1a4fc-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a4fc-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1a4fc-117">Request syntax</span></span>

| <span data-ttu-id="1a4fc-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="1a4fc-118">Method</span></span>  | <span data-ttu-id="1a4fc-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1a4fc-119">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="1a4fc-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1a4fc-120">**GET**</span></span> | <span data-ttu-id="1a4fc-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Analytics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="1a4fc-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a4fc-122">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1a4fc-122">Request headers</span></span>

<span data-ttu-id="1a4fc-123">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fc-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a4fc-124">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1a4fc-124">Request body</span></span>

<span data-ttu-id="1a4fc-125">Brak.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1a4fc-126">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1a4fc-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1a4fc-127">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1a4fc-127">REST response</span></span>

<span data-ttu-id="1a4fc-128">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) , które zawierają informacje na temat wdrożonych licencji.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-128">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a4fc-129">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1a4fc-129">Response success and error codes</span></span>

<span data-ttu-id="1a4fc-130">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a4fc-131">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1a4fc-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a4fc-132">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fc-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a4fc-133">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1a4fc-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
