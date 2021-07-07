---
title: Uzyskiwanie listy zasad samoobsługi
description: Jak uzyskać kolekcję zasobów reprezentujących zasady samoobsługi klienta.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b18fde8a11d3ed3dd31e50fdba746dd6b0bf3f97
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025737"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="e6f13-103">Uzyskiwanie listy zasad samoobsługi</span><span class="sxs-lookup"><span data-stu-id="e6f13-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="e6f13-104">Pobiera kolekcję zasobów, która reprezentuje zasady samoobsługi dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="e6f13-104">Gets a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f13-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6f13-105">Prerequisites</span></span>

- <span data-ttu-id="e6f13-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e6f13-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6f13-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e6f13-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e6f13-108">C\#</span><span class="sxs-lookup"><span data-stu-id="e6f13-108">C\#</span></span>

<span data-ttu-id="e6f13-109">Aby uzyskać listę wszystkich zasad samoobsługi:</span><span class="sxs-lookup"><span data-stu-id="e6f13-109">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="e6f13-110">Wywołaj [**metodę IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) z identyfikatorem jednostki, aby pobrać interfejs do operacji na zasadach.</span><span class="sxs-lookup"><span data-stu-id="e6f13-110">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="e6f13-111">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="e6f13-111">For an example, see the following:</span></span>

- <span data-ttu-id="e6f13-112">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e6f13-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e6f13-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="e6f13-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="e6f13-114">Klasa: **GetSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="e6f13-114">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e6f13-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e6f13-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6f13-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e6f13-116">Request syntax</span></span>

| <span data-ttu-id="e6f13-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="e6f13-117">Method</span></span>  | <span data-ttu-id="e6f13-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e6f13-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="e6f13-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e6f13-119">**GET**</span></span> | <span data-ttu-id="e6f13-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e6f13-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e6f13-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e6f13-121">URI parameter</span></span>

<span data-ttu-id="e6f13-122">Użyj następującego parametru zapytania, aby uzyskać listę klientów.</span><span class="sxs-lookup"><span data-stu-id="e6f13-122">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="e6f13-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e6f13-123">Name</span></span>          | <span data-ttu-id="e6f13-124">Typ</span><span class="sxs-lookup"><span data-stu-id="e6f13-124">Type</span></span>       | <span data-ttu-id="e6f13-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e6f13-125">Required</span></span> | <span data-ttu-id="e6f13-126">Opis</span><span class="sxs-lookup"><span data-stu-id="e6f13-126">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="e6f13-127">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="e6f13-127">**entity_id**</span></span> | <span data-ttu-id="e6f13-128">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="e6f13-128">**string**</span></span> | <span data-ttu-id="e6f13-129">Y</span><span class="sxs-lookup"><span data-stu-id="e6f13-129">Y</span></span>        | <span data-ttu-id="e6f13-130">Identyfikator jednostki żądający dostępu.</span><span class="sxs-lookup"><span data-stu-id="e6f13-130">The entity identifier requesting access for.</span></span> <span data-ttu-id="e6f13-131">Będzie to identyfikator dzierżawy klienta.</span><span class="sxs-lookup"><span data-stu-id="e6f13-131">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e6f13-132">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e6f13-132">Request headers</span></span>

<span data-ttu-id="e6f13-133">Aby uzyskać więcej informacji, zobacz [Nagłówki](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e6f13-133">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6f13-134">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e6f13-134">Request body</span></span>

<span data-ttu-id="e6f13-135">Brak.</span><span class="sxs-lookup"><span data-stu-id="e6f13-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e6f13-136">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e6f13-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="e6f13-137">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e6f13-137">REST response</span></span>

<span data-ttu-id="e6f13-138">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e6f13-138">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6f13-139">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e6f13-139">Response success and error codes</span></span>

<span data-ttu-id="e6f13-140">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e6f13-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6f13-141">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e6f13-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6f13-142">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e6f13-142">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e6f13-143">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e6f13-143">Response example</span></span>

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
