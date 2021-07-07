---
title: Pobieranie listy odsprzedawców pośrednich
description: Jak pobrać listę pośrednich odsprzedawców partnerów zalogowanych.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 58f5c3378b5b941fdc9dafcf28f5efbc58c29c7c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446568"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="40911-103">Pobieranie listy odsprzedawców pośrednich</span><span class="sxs-lookup"><span data-stu-id="40911-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="40911-104">Jak pobrać listę pośrednich odsprzedawców partnerów zalogowanych.</span><span class="sxs-lookup"><span data-stu-id="40911-104">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40911-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="40911-105">Prerequisites</span></span>

- <span data-ttu-id="40911-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="40911-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="40911-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40911-107">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="40911-108">C\#</span><span class="sxs-lookup"><span data-stu-id="40911-108">C\#</span></span>

<span data-ttu-id="40911-109">Aby pobrać listę odsprzedawców pośrednich, z którymi jest relacja między zalogowanym partnerem, najpierw uzyskaj interfejs do operacji zbierania relacji z właściwości [**partnerOperations.Relationships.**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships)</span><span class="sxs-lookup"><span data-stu-id="40911-109">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="40911-110">Następnie wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) lub [**Get \_ Async,**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) przekazując członek wyliczenia [**PartnerRelationshipType,**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) aby zidentyfikować typ relacji.</span><span class="sxs-lookup"><span data-stu-id="40911-110">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="40911-111">Aby pobrać odsprzedawców pośrednich, należy użyć funkcji IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="40911-111">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="40911-112">**Przykład:** [Aplikacja testowa konsoli](console-test-app.md)**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: GetIndirectResellers.cs</span><span class="sxs-lookup"><span data-stu-id="40911-112">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="40911-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="40911-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="40911-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="40911-114">Request syntax</span></span>

| <span data-ttu-id="40911-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="40911-115">Method</span></span>  | <span data-ttu-id="40911-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="40911-116">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40911-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="40911-117">**GET**</span></span> | <span data-ttu-id="40911-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="40911-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="40911-119">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="40911-119">URI parameter</span></span>

<span data-ttu-id="40911-120">Użyj następującego parametru zapytania, aby zidentyfikować typ relacji.</span><span class="sxs-lookup"><span data-stu-id="40911-120">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="40911-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="40911-121">Name</span></span>               | <span data-ttu-id="40911-122">Typ</span><span class="sxs-lookup"><span data-stu-id="40911-122">Type</span></span>    | <span data-ttu-id="40911-123">Wymagane</span><span class="sxs-lookup"><span data-stu-id="40911-123">Required</span></span>  | <span data-ttu-id="40911-124">Opis</span><span class="sxs-lookup"><span data-stu-id="40911-124">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="40911-125">relationship_type</span><span class="sxs-lookup"><span data-stu-id="40911-125">relationship_type</span></span>  | <span data-ttu-id="40911-126">ciąg</span><span class="sxs-lookup"><span data-stu-id="40911-126">string</span></span>  | <span data-ttu-id="40911-127">Tak</span><span class="sxs-lookup"><span data-stu-id="40911-127">Yes</span></span>       | <span data-ttu-id="40911-128">Wartość jest ciągiem reprezentacji jednej z nazw członków znalezionych w [typie PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span><span class="sxs-lookup"><span data-stu-id="40911-128">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="40911-129">Jeśli partner jest zalogowany jako dostawca i chcesz uzyskać listę odsprzedawców pośrednich, z którymi nawiążą relację, użyj funkcji IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="40911-129">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="40911-130">Jeśli partner jest zalogowany jako odsprzedawca i chcesz uzyskać listę dostawców pośrednich, z którymi nawiążą relację, użyj funkcji IsIndirectResellerOf.</span><span class="sxs-lookup"><span data-stu-id="40911-130">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="40911-131">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="40911-131">Request headers</span></span>

<span data-ttu-id="40911-132">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="40911-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="40911-133">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="40911-133">Request body</span></span>

<span data-ttu-id="40911-134">Brak.</span><span class="sxs-lookup"><span data-stu-id="40911-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="40911-135">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="40911-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="40911-136">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="40911-136">REST response</span></span>

<span data-ttu-id="40911-137">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerRelationship](relationships-resources.md) w celu zidentyfikowania odsprzedawców.</span><span class="sxs-lookup"><span data-stu-id="40911-137">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="40911-138">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40911-138">Response success and error codes</span></span>

<span data-ttu-id="40911-139">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="40911-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="40911-140">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="40911-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="40911-141">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="40911-141">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="40911-142">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40911-142">Response example</span></span>

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