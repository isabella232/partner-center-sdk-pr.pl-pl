---
title: Pobieranie listy odsprzedawców pośrednich
description: Jak pobrać listę pośrednich odsprzedawcaów zalogowanego partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768398"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="f259b-103">Pobieranie listy odsprzedawców pośrednich</span><span class="sxs-lookup"><span data-stu-id="f259b-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="f259b-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="f259b-104">**Applies To**</span></span>

- <span data-ttu-id="f259b-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="f259b-105">Partner Center</span></span>

<span data-ttu-id="f259b-106">Jak pobrać listę pośrednich odsprzedawcaów zalogowanego partnera.</span><span class="sxs-lookup"><span data-stu-id="f259b-106">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f259b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f259b-107">Prerequisites</span></span>

- <span data-ttu-id="f259b-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f259b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f259b-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f259b-109">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="f259b-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f259b-110">C\#</span></span>

<span data-ttu-id="f259b-111">Aby pobrać listę pośrednich odsprzedawcaów, z którymi partner zalogowany ma relację, należy najpierw uzyskać interfejs do operacji kolekcji relacji z właściwości [**partnerOperations. Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) .</span><span class="sxs-lookup"><span data-stu-id="f259b-111">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="f259b-112">Następnie Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) lub [**get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , przekazując element członkowski wyliczenia [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) , aby zidentyfikować typ relacji.</span><span class="sxs-lookup"><span data-stu-id="f259b-112">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="f259b-113">Aby pobrać pośrednich odsprzedawcaów, musisz użyć IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="f259b-113">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="f259b-114">**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: GetIndirectResellers.cs</span><span class="sxs-lookup"><span data-stu-id="f259b-114">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f259b-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f259b-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f259b-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f259b-116">Request syntax</span></span>

| <span data-ttu-id="f259b-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="f259b-117">Method</span></span>  | <span data-ttu-id="f259b-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f259b-118">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f259b-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f259b-119">**GET**</span></span> | <span data-ttu-id="f259b-120">[*{baseURL}*](partner-center-rest-urls.md)/V1/Relationships? \_ Typ relacji = IsIndirectCloudSolutionProviderOf http/1.1</span><span class="sxs-lookup"><span data-stu-id="f259b-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f259b-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f259b-121">URI parameter</span></span>

<span data-ttu-id="f259b-122">Użyj następującego parametru zapytania, aby zidentyfikować typ relacji.</span><span class="sxs-lookup"><span data-stu-id="f259b-122">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="f259b-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f259b-123">Name</span></span>               | <span data-ttu-id="f259b-124">Typ</span><span class="sxs-lookup"><span data-stu-id="f259b-124">Type</span></span>    | <span data-ttu-id="f259b-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f259b-125">Required</span></span>  | <span data-ttu-id="f259b-126">Opis</span><span class="sxs-lookup"><span data-stu-id="f259b-126">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="f259b-127">relationship_type</span><span class="sxs-lookup"><span data-stu-id="f259b-127">relationship_type</span></span>  | <span data-ttu-id="f259b-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="f259b-128">string</span></span>  | <span data-ttu-id="f259b-129">Tak</span><span class="sxs-lookup"><span data-stu-id="f259b-129">Yes</span></span>       | <span data-ttu-id="f259b-130">Wartość jest reprezentacją ciągu jednej z nazw składowych znalezionych w [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span><span class="sxs-lookup"><span data-stu-id="f259b-130">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="f259b-131">Jeśli partner jest zalogowany jako dostawca i chcesz uzyskać listę pośrednich odsprzedawcaów, z którymi ustanowiono relację, użyj IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="f259b-131">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="f259b-132">Jeśli partner jest zalogowany jako odsprzedawca i chcesz uzyskać listę dostawców pośrednich, którym ustanowiono relację, użyj IsIndirectResellerOf.</span><span class="sxs-lookup"><span data-stu-id="f259b-132">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="f259b-133">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f259b-133">Request headers</span></span>

<span data-ttu-id="f259b-134">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f259b-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f259b-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f259b-135">Request body</span></span>

<span data-ttu-id="f259b-136">Brak.</span><span class="sxs-lookup"><span data-stu-id="f259b-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f259b-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f259b-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f259b-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f259b-138">REST response</span></span>

<span data-ttu-id="f259b-139">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerRelationship](relationships-resources.md) , aby zidentyfikować odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="f259b-139">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f259b-140">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f259b-140">Response success and error codes</span></span>

<span data-ttu-id="f259b-141">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="f259b-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f259b-142">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f259b-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f259b-143">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f259b-143">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f259b-144">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f259b-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```