---
title: Pobieranie zasad samoobsługi według identyfikatora
description: Pobiera określone zasady samoobsługowe za pomocą jej identyfikatora.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767933"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="e5381-103">Pobieranie zasad samoobsługi według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="e5381-103">Get a self serve policy by ID</span></span>

<span data-ttu-id="e5381-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="e5381-104">**Applies To**</span></span>

- <span data-ttu-id="e5381-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e5381-105">Partner Center</span></span>

<span data-ttu-id="e5381-106">Pobiera określone zasady samoobsługowe za pomocą jej identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="e5381-106">Gets the specified self serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5381-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e5381-107">Prerequisites</span></span>

- <span data-ttu-id="e5381-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e5381-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e5381-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e5381-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="e5381-110">Identyfikator zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e5381-110">A self serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="e5381-111">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e5381-111">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="e5381-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e5381-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="e5381-113">**Składnia żądania**</span><span class="sxs-lookup"><span data-stu-id="e5381-113">**Request syntax**</span></span>

| <span data-ttu-id="e5381-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="e5381-114">Method</span></span>  | <span data-ttu-id="e5381-115">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e5381-115">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="e5381-116">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e5381-116">**GET**</span></span> | <span data-ttu-id="e5381-117">[*{baseURL}*](partner-center-rest-urls.md)/V1/SelfServePolicy/{ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e5381-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="e5381-118">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="e5381-118">**URI parameter**</span></span>

<span data-ttu-id="e5381-119">Aby uzyskać określony produkt, użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="e5381-119">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="e5381-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e5381-120">Name</span></span>                       | <span data-ttu-id="e5381-121">Typ</span><span class="sxs-lookup"><span data-stu-id="e5381-121">Type</span></span>         | <span data-ttu-id="e5381-122">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5381-122">Required</span></span> | <span data-ttu-id="e5381-123">Opis</span><span class="sxs-lookup"><span data-stu-id="e5381-123">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="e5381-124">**SelfServePolicy — identyfikator**</span><span class="sxs-lookup"><span data-stu-id="e5381-124">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="e5381-125">**parametry**</span><span class="sxs-lookup"><span data-stu-id="e5381-125">**string**</span></span>   | <span data-ttu-id="e5381-126">Tak</span><span class="sxs-lookup"><span data-stu-id="e5381-126">Yes</span></span>      | <span data-ttu-id="e5381-127">Ciąg, który identyfikuje zasady samoobsługowe.</span><span class="sxs-lookup"><span data-stu-id="e5381-127">A string that identifies the self serve policy.</span></span>                 |

<span data-ttu-id="e5381-128">**Nagłówki żądań**</span><span class="sxs-lookup"><span data-stu-id="e5381-128">**Request headers**</span></span>

- <span data-ttu-id="e5381-129">Zobacz [nagłówki](headers.md) , aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e5381-129">See [Headers](headers.md) for more information.</span></span>

<span data-ttu-id="e5381-130">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="e5381-130">**Request body**</span></span>

<span data-ttu-id="e5381-131">Brak.</span><span class="sxs-lookup"><span data-stu-id="e5381-131">None.</span></span>

<span data-ttu-id="e5381-132">**Przykład żądania**</span><span class="sxs-lookup"><span data-stu-id="e5381-132">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="e5381-133">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e5381-133">REST response</span></span>

<span data-ttu-id="e5381-134">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) .</span><span class="sxs-lookup"><span data-stu-id="e5381-134">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="e5381-135">**Kody sukcesu i błędów odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="e5381-135">**Response success and error codes**</span></span>

<span data-ttu-id="e5381-136">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e5381-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e5381-137">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e5381-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e5381-138">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e5381-138">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="e5381-139">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="e5381-139">This method returns the following error codes:</span></span>

| <span data-ttu-id="e5381-140">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="e5381-140">HTTP Status Code</span></span>     | <span data-ttu-id="e5381-141">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="e5381-141">Error code</span></span>   | <span data-ttu-id="e5381-142">Opis</span><span class="sxs-lookup"><span data-stu-id="e5381-142">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="e5381-143">404</span><span class="sxs-lookup"><span data-stu-id="e5381-143">404</span></span>                  | <span data-ttu-id="e5381-144">600039</span><span class="sxs-lookup"><span data-stu-id="e5381-144">600039</span></span>       | <span data-ttu-id="e5381-145">Nie znaleziono zasad samoobsługowych.</span><span class="sxs-lookup"><span data-stu-id="e5381-145">Self serve policy not found.</span></span>                                                     |

<span data-ttu-id="e5381-146">**Przykład odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="e5381-146">**Response example**</span></span>

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