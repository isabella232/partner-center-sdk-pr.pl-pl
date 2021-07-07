---
title: Pobieranie informacji dotyczących wdrażania licencji partnera
description: Jak uzyskać zagregowane informacje o wdrażaniu licencji partnerów, aby uwzględnić wszystkich klientów.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2464242fc6dc4e7464511eac5d4197630e22fac0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445987"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="8de5a-103">Pobieranie informacji dotyczących wdrażania licencji partnera</span><span class="sxs-lookup"><span data-stu-id="8de5a-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="8de5a-104">Jak uzyskać zagregowane informacje o wdrażaniu licencji partnerów, aby uwzględnić wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="8de5a-104">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="8de5a-105">Ten scenariusz jest przesłoowany przez uzyskiwanie [informacji o wdrożeniu licencji.](get-licenses-deployment-information.md)</span><span class="sxs-lookup"><span data-stu-id="8de5a-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8de5a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8de5a-106">Prerequisites</span></span>

<span data-ttu-id="8de5a-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8de5a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8de5a-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8de5a-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="8de5a-109">C\#</span><span class="sxs-lookup"><span data-stu-id="8de5a-109">C\#</span></span>

<span data-ttu-id="8de5a-110">Aby pobrać zagregowane dane dotyczące wdrożenia licencji, najpierw uzyskaj interfejs do operacji zbierania danych analitycznych na poziomie partnera z właściwości [**IAggregatePartner.Analytics.**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)</span><span class="sxs-lookup"><span data-stu-id="8de5a-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="8de5a-111">Następnie pobierz interfejs do kolekcji analizy licencji na poziomie partnera z [**właściwości Licencje.**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses)</span><span class="sxs-lookup"><span data-stu-id="8de5a-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="8de5a-112">Na koniec wywołaj [**metodę Deployment.Get,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) aby uzyskać zagregowane dane dotyczące wdrożenia licencji.</span><span class="sxs-lookup"><span data-stu-id="8de5a-112">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="8de5a-113">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**PartnerLicensesDeploymentInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights)</span><span class="sxs-lookup"><span data-stu-id="8de5a-113">If the method succeeds, you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="8de5a-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8de5a-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8de5a-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8de5a-115">Request syntax</span></span>

| <span data-ttu-id="8de5a-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="8de5a-116">Method</span></span>  | <span data-ttu-id="8de5a-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8de5a-117">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="8de5a-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="8de5a-118">**GET**</span></span> | <span data-ttu-id="8de5a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8de5a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8de5a-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8de5a-120">Request headers</span></span>

<span data-ttu-id="8de5a-121">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8de5a-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8de5a-122">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8de5a-122">Request body</span></span>

<span data-ttu-id="8de5a-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="8de5a-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8de5a-124">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8de5a-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8de5a-125">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8de5a-125">REST response</span></span>

<span data-ttu-id="8de5a-126">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [PartnerLicensesDeploymentInsights,](analytics-resources.md#partnerlicensesdeploymentinsights) które zawierają informacje o wdrożonych licencjach.</span><span class="sxs-lookup"><span data-stu-id="8de5a-126">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8de5a-127">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8de5a-127">Response success and error codes</span></span>

<span data-ttu-id="8de5a-128">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8de5a-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8de5a-129">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8de5a-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8de5a-130">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8de5a-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8de5a-131">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8de5a-131">Response example</span></span>

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
