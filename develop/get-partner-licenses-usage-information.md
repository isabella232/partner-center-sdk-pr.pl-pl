---
title: Pobieranie informacji dotyczących użycia licencji partnera
description: Jak uzyskać informacje o użyciu licencji partnerów zagregowane w celu uwzględnienia wszystkich klientów.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d003fb269a3421b8efd8cebe8f396f97599a10
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768477"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="0df52-103">Pobieranie informacji dotyczących użycia licencji partnera</span><span class="sxs-lookup"><span data-stu-id="0df52-103">Get partner licenses usage information</span></span>

<span data-ttu-id="0df52-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="0df52-104">**Applies To**</span></span>

- <span data-ttu-id="0df52-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0df52-105">Partner Center</span></span>

<span data-ttu-id="0df52-106">Jak uzyskać informacje o użyciu licencji partnerów zagregowane w celu uwzględnienia wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="0df52-106">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="0df52-107">Ten scenariusz jest zastąpiony przez [uzyskanie informacji o użyciu licencji](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="0df52-107">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0df52-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0df52-108">Prerequisites</span></span>

<span data-ttu-id="0df52-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0df52-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0df52-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0df52-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="0df52-111">C\#</span><span class="sxs-lookup"><span data-stu-id="0df52-111">C\#</span></span>

<span data-ttu-id="0df52-112">Aby pobrać zagregowane dane dotyczące wdrożenia licencji, należy najpierw pobrać interfejs do operacji zbierania danych analitycznych na poziomie partnera ze [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) właściwości.</span><span class="sxs-lookup"><span data-stu-id="0df52-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="0df52-113">Następnie można pobrać interfejs do kolekcji analizy licencji poziomu partnera z właściwości [**licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="0df52-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="0df52-114">Na koniec Wywołaj metodę [**Usage. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , aby uzyskać zagregowane dane dotyczące użycia licencji.</span><span class="sxs-lookup"><span data-stu-id="0df52-114">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="0df52-115">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) .</span><span class="sxs-lookup"><span data-stu-id="0df52-115">If the method succeeds you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="0df52-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0df52-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0df52-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0df52-117">Request syntax</span></span>

| <span data-ttu-id="0df52-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="0df52-118">Method</span></span>  | <span data-ttu-id="0df52-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0df52-119">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="0df52-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="0df52-120">**GET**</span></span> | <span data-ttu-id="0df52-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Analytics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="0df52-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0df52-122">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0df52-122">Request headers</span></span>

<span data-ttu-id="0df52-123">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0df52-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0df52-124">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0df52-124">Request body</span></span>

<span data-ttu-id="0df52-125">Brak.</span><span class="sxs-lookup"><span data-stu-id="0df52-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0df52-126">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0df52-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0df52-127">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0df52-127">REST response</span></span>

<span data-ttu-id="0df52-128">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) , które zawierają informacje na temat używanych licencji.</span><span class="sxs-lookup"><span data-stu-id="0df52-128">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0df52-129">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0df52-129">Response success and error codes</span></span>

<span data-ttu-id="0df52-130">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="0df52-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0df52-131">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0df52-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0df52-132">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0df52-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0df52-133">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0df52-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
