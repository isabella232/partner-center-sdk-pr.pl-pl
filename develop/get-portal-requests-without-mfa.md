---
title: Pobieranie żądań portalu bez uwierzytelniania wieloskładnikowego
description: Pobierz listę żądań użytkowników bez uwierzytelniania wieloskładnikowego (MFA) przy użyciu interfejsu API REST partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: fd350aa3301f00926942ae6c6af359b0d0edc423
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767925"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="9c9f3-103">Pobieranie żądań portalu bez uwierzytelniania wieloskładnikowego</span><span class="sxs-lookup"><span data-stu-id="9c9f3-103">Get portal requests without MFA</span></span>

<span data-ttu-id="9c9f3-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="9c9f3-104">Applies to:</span></span>

- <span data-ttu-id="9c9f3-105">Interfejs API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="9c9f3-105">Partner Center API</span></span>

<span data-ttu-id="9c9f3-106">W tym artykule wyjaśniono, jak uzyskać listę najnowszych żądań od użytkowników, którzy uzyskują dostęp do portalu usługi Partner Center bez wykonywania uwierzytelniania wieloskładnikowego (MFA).</span><span class="sxs-lookup"><span data-stu-id="9c9f3-106">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c9f3-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c9f3-107">Prerequisites</span></span>

- <span data-ttu-id="9c9f3-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9c9f3-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9c9f3-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c9f3-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="9c9f3-110">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9c9f3-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9c9f3-111">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9c9f3-111">Request syntax</span></span>

| <span data-ttu-id="9c9f3-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="9c9f3-112">Method</span></span>  | <span data-ttu-id="9c9f3-113">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9c9f3-113">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="9c9f3-114">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9c9f3-114">**GET**</span></span> | <span data-ttu-id="9c9f3-115">[*{baseURL}*](partner-center-rest-urls.md)/V1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="9c9f3-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9c9f3-116">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9c9f3-116">Request headers</span></span>

- <span data-ttu-id="9c9f3-117">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="9c9f3-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="9c9f3-118">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9c9f3-118">Request body</span></span>

<span data-ttu-id="9c9f3-119">Brak.</span><span class="sxs-lookup"><span data-stu-id="9c9f3-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9c9f3-120">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9c9f3-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="9c9f3-121">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9c9f3-121">REST response</span></span>

<span data-ttu-id="9c9f3-122">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [żądania portalu](mfa-resources.md#portal-request-without-mfa) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9c9f3-122">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9c9f3-123">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9c9f3-123">Response success and error codes</span></span>

<span data-ttu-id="9c9f3-124">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9c9f3-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9c9f3-125">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9c9f3-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9c9f3-126">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9c9f3-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9c9f3-127">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9c9f3-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 296
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 23 Apr 2020 22:10:30 GMT
{
    "totalCount": 1,
    "items": [
        {
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "lastNonMfaCompliantRequestDateTime": "2020-04-21T22:09:53.051"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
