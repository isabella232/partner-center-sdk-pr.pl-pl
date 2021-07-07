---
title: Pobieranie informacji dotyczących użycia licencji partnera
description: Jak uzyskać zagregowane informacje o użyciu licencji partnerów, aby uwzględnić wszystkich klientów.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f3d05d61ac4f2c90b0d8a4bfd93fe24e94bd5c1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445599"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="d130f-103">Pobieranie informacji dotyczących użycia licencji partnera</span><span class="sxs-lookup"><span data-stu-id="d130f-103">Get partner licenses usage information</span></span>

<span data-ttu-id="d130f-104">Jak uzyskać zagregowane informacje o użyciu licencji partnerów, aby uwzględnić wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="d130f-104">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="d130f-105">Ten scenariusz został wyzłoszony przez informacje [o użyciu funkcji Get licenses](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="d130f-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d130f-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d130f-106">Prerequisites</span></span>

<span data-ttu-id="d130f-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d130f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d130f-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d130f-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d130f-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d130f-109">C\#</span></span>

<span data-ttu-id="d130f-110">Aby pobrać zagregowane dane dotyczące wdrożenia licencji, najpierw pobierz interfejs do operacji zbierania danych analitycznych na poziomie partnera z właściwości [**IAggregatePartner.Analytics.**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)</span><span class="sxs-lookup"><span data-stu-id="d130f-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="d130f-111">Następnie pobierz interfejs do kolekcji analitycznej licencji na poziomie partnera z [**właściwości Licencje.**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses)</span><span class="sxs-lookup"><span data-stu-id="d130f-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="d130f-112">Na koniec wywołaj [**metodę Usage.Get,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) aby uzyskać zagregowane dane dotyczące użycia licencji.</span><span class="sxs-lookup"><span data-stu-id="d130f-112">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="d130f-113">Jeśli metoda powiedzie się, otrzymasz kolekcję obiektów [**PartnerLicensesUsageInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights)</span><span class="sxs-lookup"><span data-stu-id="d130f-113">If the method succeeds, you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="d130f-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d130f-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d130f-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d130f-115">Request syntax</span></span>

| <span data-ttu-id="d130f-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="d130f-116">Method</span></span>  | <span data-ttu-id="d130f-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d130f-117">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="d130f-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d130f-118">**GET**</span></span> | <span data-ttu-id="d130f-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d130f-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d130f-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d130f-120">Request headers</span></span>

<span data-ttu-id="d130f-121">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d130f-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d130f-122">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d130f-122">Request body</span></span>

<span data-ttu-id="d130f-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="d130f-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d130f-124">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d130f-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d130f-125">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d130f-125">REST response</span></span>

<span data-ttu-id="d130f-126">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [PartnerLicensesUsageInsights,](analytics-resources.md#partnerlicensesusageinsights) które zawierają informacje o używanych licencjach.</span><span class="sxs-lookup"><span data-stu-id="d130f-126">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d130f-127">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d130f-127">Response success and error codes</span></span>

<span data-ttu-id="d130f-128">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d130f-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d130f-129">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d130f-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d130f-130">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d130f-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d130f-131">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d130f-131">Response example</span></span>

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
