---
title: Pobierz listę wszystkich żądań użytkowników partnerskich
description: Pobierz listę wszystkich żądań użytkowników partnerskich za pomocą interfejsu API REST partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: cychua
ms.author: cychua
ms.openlocfilehash: 43b1e3d4a6220ac8adba8eed0389395113072288
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767709"
---
# <a name="get-app-and-user-api-requests"></a><span data-ttu-id="b2867-103">Pobieranie żądań interfejsu API aplikacji i użytkowników</span><span class="sxs-lookup"><span data-stu-id="b2867-103">Get App and User API requests</span></span>

<span data-ttu-id="b2867-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="b2867-104">Applies to:</span></span>

- <span data-ttu-id="b2867-105">Interfejs API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="b2867-105">Partner Center API</span></span>

<span data-ttu-id="b2867-106">W tym artykule wyjaśniono, jak uzyskać listę wszystkich żądań użytkowników partnerskich w ramach dzierżawy przy użyciu interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="b2867-106">This article explains how to obtain a list of all partner user requests within a tenant using REST APIs.</span></span>

 > [!NOTE]
 > <span data-ttu-id="b2867-107">Ten interfejs API zwraca tylko najnowsze żądania interfejsu API podejmowane przez aplikację APP + poświadczenia użytkownika z maksymalnym limitem (10 tys.).</span><span class="sxs-lookup"><span data-stu-id="b2867-107">This API only returns the most recent API requests made by APP + User credential with maximum 10K limit.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2867-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2867-108">Prerequisites</span></span>

- <span data-ttu-id="b2867-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2867-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b2867-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2867-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b2867-111">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b2867-111">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b2867-112">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b2867-112">Request syntax</span></span>

| <span data-ttu-id="b2867-113">Metoda</span><span class="sxs-lookup"><span data-stu-id="b2867-113">Method</span></span>  | <span data-ttu-id="b2867-114">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b2867-114">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="b2867-115">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b2867-115">**GET**</span></span> | <span data-ttu-id="b2867-116">[*{baseURL}*](partner-center-rest-urls.md)/V1/partnerRequests</span><span class="sxs-lookup"><span data-stu-id="b2867-116">[*{baseURL}*](partner-center-rest-urls.md)/v1/partnerRequests</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b2867-117">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b2867-117">Request headers</span></span>

- <span data-ttu-id="b2867-118">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="b2867-118">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="b2867-119">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b2867-119">Request body</span></span>

<span data-ttu-id="b2867-120">Brak.</span><span class="sxs-lookup"><span data-stu-id="b2867-120">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b2867-121">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b2867-121">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/partnerRequests HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="b2867-122">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b2867-122">REST response</span></span>

<span data-ttu-id="b2867-123">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [szczegóły żądania interfejsu API](mfa-resources.md#api-request-details) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b2867-123">If successful, this method returns a collection of [API request details](mfa-resources.md#api-request-details) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b2867-124">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b2867-124">Response success and error codes</span></span>

<span data-ttu-id="b2867-125">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b2867-125">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b2867-126">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b2867-126">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b2867-127">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b2867-127">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b2867-128">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b2867-128">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 2960
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
{
    "totalCount": 2,
    "items": [
        {
            "requestId": "6c583d8d-46cd-420c-ae3d-35b6dfdcdb21",
            "correlationId": "",
            "operationName": "Get /v{version}/nonMfaCompliantPartnerPrincipals",
            "requestDateTime": "2020-05-21T21:02:10.31",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "c69854fe-5fb4-4527-a28f-f24f1acaffd6",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "admin@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": true
        },
        {
            "requestId": "09f8e434-a9ce-43ea-a9ac-270fbb22371a",
            "correlationId": "",
            "operationName": "Get /v{version}/customers/{customer_id}/subscriptions?order_id={order_id_value}&mpn_id={mpn_id_value}",
            "requestDateTime": "2020-05-21T22:18:35.73",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": false
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
