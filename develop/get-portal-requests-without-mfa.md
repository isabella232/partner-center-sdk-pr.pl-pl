---
title: Pobieranie żądań portalu bez uwierzytelniania wieloskładnikowego
description: Pobierz listę żądań użytkowników bez uwierzytelniania wieloskładnikowego (MFA) przy użyciu interfejsu API REST partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 41627751d3402d7712d96c15c4281a25ed9a44a7
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445582"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="bc973-103">Pobieranie żądań portalu bez uwierzytelniania wieloskładnikowego</span><span class="sxs-lookup"><span data-stu-id="bc973-103">Get portal requests without MFA</span></span>

<span data-ttu-id="bc973-104">W tym artykule wyjaśniono, jak uzyskać listę najnowszych żądań od użytkowników, którzy mają dostęp do portalu Partner Center bez ukończenia uwierzytelniania wieloskładnikowego (MFA).</span><span class="sxs-lookup"><span data-stu-id="bc973-104">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc973-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc973-105">Prerequisites</span></span>

- <span data-ttu-id="bc973-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bc973-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bc973-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc973-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="bc973-108">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="bc973-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bc973-109">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="bc973-109">Request syntax</span></span>

| <span data-ttu-id="bc973-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="bc973-110">Method</span></span>  | <span data-ttu-id="bc973-111">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="bc973-111">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="bc973-112">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="bc973-112">**GET**</span></span> | <span data-ttu-id="bc973-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="bc973-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bc973-114">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="bc973-114">Request headers</span></span>

- <span data-ttu-id="bc973-115">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bc973-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bc973-116">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="bc973-116">Request body</span></span>

<span data-ttu-id="bc973-117">Brak.</span><span class="sxs-lookup"><span data-stu-id="bc973-117">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bc973-118">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="bc973-118">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="bc973-119">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="bc973-119">REST response</span></span>

<span data-ttu-id="bc973-120">W przypadku powodzenia ta metoda zwraca kolekcję zasobów żądania [portalu](mfa-resources.md#portal-request-without-mfa) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bc973-120">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bc973-121">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bc973-121">Response success and error codes</span></span>

<span data-ttu-id="bc973-122">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="bc973-122">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bc973-123">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="bc973-123">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bc973-124">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bc973-124">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bc973-125">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bc973-125">Response example</span></span>

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
