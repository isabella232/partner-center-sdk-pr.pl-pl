---
title: Pobieranie adresu URL żądania relacji
description: Jak pobrać adres URL żądania relacji do wysłania do klienta.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07804b36dfe0892cf8b531e0731188260c014f49
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547458"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="60dd5-103">Pobieranie adresu URL żądania relacji</span><span class="sxs-lookup"><span data-stu-id="60dd5-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="60dd5-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="60dd5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="60dd5-105">Jak pobrać adres URL żądania relacji do wysłania do klienta.</span><span class="sxs-lookup"><span data-stu-id="60dd5-105">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60dd5-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="60dd5-106">Prerequisites</span></span>

- <span data-ttu-id="60dd5-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="60dd5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="60dd5-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="60dd5-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="60dd5-109">C\#</span><span class="sxs-lookup"><span data-stu-id="60dd5-109">C\#</span></span>

<span data-ttu-id="60dd5-110">Aby pobrać adres URL żądania relacji, najpierw użyj funkcji [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby uzyskać interfejs do operacji klienta partnera.</span><span class="sxs-lookup"><span data-stu-id="60dd5-110">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="60dd5-111">Następnie użyj właściwości [**RelationshipRequest,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) aby uzyskać interfejs do operacji żądania relacji z klientem.</span><span class="sxs-lookup"><span data-stu-id="60dd5-111">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="60dd5-112">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) aby pobrać adres URL.</span><span class="sxs-lookup"><span data-stu-id="60dd5-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="60dd5-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="60dd5-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="60dd5-114">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="60dd5-114">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="60dd5-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="60dd5-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="60dd5-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="60dd5-116">Request syntax</span></span>

| <span data-ttu-id="60dd5-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="60dd5-117">Method</span></span>  | <span data-ttu-id="60dd5-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="60dd5-118">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="60dd5-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="60dd5-119">**GET**</span></span> | <span data-ttu-id="60dd5-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="60dd5-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="60dd5-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="60dd5-121">Request headers</span></span>

<span data-ttu-id="60dd5-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="60dd5-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="60dd5-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60dd5-123">Request body</span></span>

<span data-ttu-id="60dd5-124">Brak</span><span class="sxs-lookup"><span data-stu-id="60dd5-124">None</span></span>

### <a name="request-example"></a><span data-ttu-id="60dd5-125">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="60dd5-125">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="60dd5-126">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="60dd5-126">REST response</span></span>

<span data-ttu-id="60dd5-127">Jeśli to się powiedzie, odpowiedź zawiera [obiekt RelationshipRequest.](relationships-resources.md#relationshiprequest)</span><span class="sxs-lookup"><span data-stu-id="60dd5-127">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="60dd5-128">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="60dd5-128">Response success and error codes</span></span>

<span data-ttu-id="60dd5-129">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="60dd5-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="60dd5-130">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="60dd5-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="60dd5-131">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="60dd5-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="60dd5-132">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="60dd5-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
