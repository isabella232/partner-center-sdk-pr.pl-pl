---
title: Pobierz listę zasad samoobsługi
description: Jak uzyskać kolekcję zasobów reprezentujących zasady samoobsługi klienta.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ff3116b8757e28e03615930ebd19bc75f34e2efe
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770243"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="dc821-103">Pobierz listę zasad samoobsługi</span><span class="sxs-lookup"><span data-stu-id="dc821-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="dc821-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="dc821-104">**Applies to:**</span></span>

- <span data-ttu-id="dc821-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="dc821-105">Partner Center</span></span>

<span data-ttu-id="dc821-106">W tym artykule opisano, jak uzyskać zbiór zasobów reprezentujących zasady samoobsługi dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="dc821-106">This article describes how to get a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc821-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dc821-107">Prerequisites</span></span>

- <span data-ttu-id="dc821-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dc821-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dc821-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dc821-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="dc821-110">C\#</span><span class="sxs-lookup"><span data-stu-id="dc821-110">C\#</span></span>

<span data-ttu-id="dc821-111">Aby uzyskać listę wszystkich zasad samoobsługi:</span><span class="sxs-lookup"><span data-stu-id="dc821-111">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="dc821-112">Wywołaj metodę [**IAggregatePartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) z identyfikatorem jednostki, aby pobrać interfejs do operacji w ramach zasad.</span><span class="sxs-lookup"><span data-stu-id="dc821-112">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="dc821-113">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="dc821-113">For an example, see the following:</span></span>

- <span data-ttu-id="dc821-114">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="dc821-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="dc821-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="dc821-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="dc821-116">Klasa: **GetSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="dc821-116">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="dc821-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="dc821-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dc821-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="dc821-118">Request syntax</span></span>

| <span data-ttu-id="dc821-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="dc821-119">Method</span></span>  | <span data-ttu-id="dc821-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="dc821-120">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="dc821-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="dc821-121">**GET**</span></span> | <span data-ttu-id="dc821-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="dc821-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="dc821-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="dc821-123">URI parameter</span></span>

<span data-ttu-id="dc821-124">Użyj następującego parametru zapytania, aby uzyskać listę klientów.</span><span class="sxs-lookup"><span data-stu-id="dc821-124">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="dc821-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dc821-125">Name</span></span>          | <span data-ttu-id="dc821-126">Typ</span><span class="sxs-lookup"><span data-stu-id="dc821-126">Type</span></span>       | <span data-ttu-id="dc821-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dc821-127">Required</span></span> | <span data-ttu-id="dc821-128">Opis</span><span class="sxs-lookup"><span data-stu-id="dc821-128">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="dc821-129">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="dc821-129">**entity_id**</span></span> | <span data-ttu-id="dc821-130">**parametry**</span><span class="sxs-lookup"><span data-stu-id="dc821-130">**string**</span></span> | <span data-ttu-id="dc821-131">Y</span><span class="sxs-lookup"><span data-stu-id="dc821-131">Y</span></span>        | <span data-ttu-id="dc821-132">Identyfikator jednostki żądającej dostępu dla.</span><span class="sxs-lookup"><span data-stu-id="dc821-132">The entity identifier requesting access for.</span></span> <span data-ttu-id="dc821-133">Będzie to identyfikator dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="dc821-133">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dc821-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="dc821-134">Request headers</span></span>

<span data-ttu-id="dc821-135">Aby uzyskać więcej informacji, zobacz [nagłówki](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dc821-135">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dc821-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="dc821-136">Request body</span></span>

<span data-ttu-id="dc821-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="dc821-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dc821-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="dc821-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="dc821-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="dc821-139">REST response</span></span>

<span data-ttu-id="dc821-140">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="dc821-140">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dc821-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dc821-141">Response success and error codes</span></span>

<span data-ttu-id="dc821-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="dc821-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dc821-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="dc821-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dc821-144">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dc821-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dc821-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dc821-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
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
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
