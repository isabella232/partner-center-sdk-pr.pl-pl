---
title: Uzyskiwanie zasad samoobsługi według identyfikatora
description: Pobiera określone zasady samoobsługi przy użyciu ich identyfikatora.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873840"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="b2ced-103">Uzyskiwanie zasad samoobsługi według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="b2ced-103">Get a self-serve policy by ID</span></span>

<span data-ttu-id="b2ced-104">Pobiera określone zasady samoobsługi przy użyciu ich identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="b2ced-104">Gets the specified self-serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2ced-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2ced-105">Prerequisites</span></span>

- <span data-ttu-id="b2ced-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b2ced-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b2ced-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2ced-107">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="b2ced-108">Identyfikator zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="b2ced-108">A self-serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="b2ced-109">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b2ced-109">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="b2ced-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b2ced-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="b2ced-111">**Składnia żądania**</span><span class="sxs-lookup"><span data-stu-id="b2ced-111">**Request syntax**</span></span>

| <span data-ttu-id="b2ced-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="b2ced-112">Method</span></span>  | <span data-ttu-id="b2ced-113">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b2ced-113">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="b2ced-114">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b2ced-114">**GET**</span></span> | <span data-ttu-id="b2ced-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b2ced-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="b2ced-116">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="b2ced-116">**URI parameter**</span></span>

<span data-ttu-id="b2ced-117">Użyj następujących parametrów ścieżki, aby uzyskać określony produkt.</span><span class="sxs-lookup"><span data-stu-id="b2ced-117">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="b2ced-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b2ced-118">Name</span></span>                       | <span data-ttu-id="b2ced-119">Typ</span><span class="sxs-lookup"><span data-stu-id="b2ced-119">Type</span></span>         | <span data-ttu-id="b2ced-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b2ced-120">Required</span></span> | <span data-ttu-id="b2ced-121">Opis</span><span class="sxs-lookup"><span data-stu-id="b2ced-121">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="b2ced-122">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="b2ced-122">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="b2ced-123">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="b2ced-123">**string**</span></span>   | <span data-ttu-id="b2ced-124">Tak</span><span class="sxs-lookup"><span data-stu-id="b2ced-124">Yes</span></span>      | <span data-ttu-id="b2ced-125">Ciąg, który identyfikuje zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="b2ced-125">A string that identifies the self-serve policy.</span></span>                 |

<span data-ttu-id="b2ced-126">**Nagłówki żądań**</span><span class="sxs-lookup"><span data-stu-id="b2ced-126">**Request headers**</span></span>

- <span data-ttu-id="b2ced-127">Aby uzyskać więcej informacji, zobacz [Nagłówki](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b2ced-127">For more information, see [Headers](headers.md).</span></span>

<span data-ttu-id="b2ced-128">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="b2ced-128">**Request body**</span></span>

<span data-ttu-id="b2ced-129">Brak.</span><span class="sxs-lookup"><span data-stu-id="b2ced-129">None.</span></span>

<span data-ttu-id="b2ced-130">**Przykład żądania**</span><span class="sxs-lookup"><span data-stu-id="b2ced-130">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="b2ced-131">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b2ced-131">REST response</span></span>

<span data-ttu-id="b2ced-132">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SelfServePolicy.](self-serve-policy-resources.md#selfservepolicy)</span><span class="sxs-lookup"><span data-stu-id="b2ced-132">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="b2ced-133">**Kody powodzenia i błędów odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="b2ced-133">**Response success and error codes**</span></span>

<span data-ttu-id="b2ced-134">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="b2ced-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b2ced-135">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b2ced-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b2ced-136">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b2ced-136">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="b2ced-137">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="b2ced-137">This method returns the following error codes:</span></span>

| <span data-ttu-id="b2ced-138">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="b2ced-138">HTTP Status Code</span></span>     | <span data-ttu-id="b2ced-139">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="b2ced-139">Error code</span></span>   | <span data-ttu-id="b2ced-140">Opis</span><span class="sxs-lookup"><span data-stu-id="b2ced-140">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="b2ced-141">404</span><span class="sxs-lookup"><span data-stu-id="b2ced-141">404</span></span>                  | <span data-ttu-id="b2ced-142">600039</span><span class="sxs-lookup"><span data-stu-id="b2ced-142">600039</span></span>       | <span data-ttu-id="b2ced-143">Nie znaleziono zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="b2ced-143">Self-serve policy not found.</span></span>                                                     |

<span data-ttu-id="b2ced-144">**Przykład odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="b2ced-144">**Response example**</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```