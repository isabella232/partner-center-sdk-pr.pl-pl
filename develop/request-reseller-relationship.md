---
title: Pobieranie adresu URL żądania relacji
description: Jak pobrać adres URL żądania relacji do wysłania do klienta.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5f899734b774ff460e005e20df8658275b2ce9d5
ms.sourcegitcommit: d4e652e3b73c6137704d43d4a472cc5aa5549f11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/09/2020
ms.locfileid: "97770275"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="a7100-103">Pobieranie adresu URL żądania relacji</span><span class="sxs-lookup"><span data-stu-id="a7100-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="a7100-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="a7100-104">**Applies To**</span></span>

- <span data-ttu-id="a7100-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a7100-105">Partner Center</span></span>
- <span data-ttu-id="a7100-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a7100-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a7100-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="a7100-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="a7100-108">Jak pobrać adres URL żądania relacji do wysłania do klienta.</span><span class="sxs-lookup"><span data-stu-id="a7100-108">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7100-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a7100-109">Prerequisites</span></span>

- <span data-ttu-id="a7100-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a7100-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a7100-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a7100-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="a7100-112">C\#</span><span class="sxs-lookup"><span data-stu-id="a7100-112">C\#</span></span>

<span data-ttu-id="a7100-113">Aby pobrać adres URL żądania relacji, najpierw Użyj [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby uzyskać interfejs do operacji klienta partnera.</span><span class="sxs-lookup"><span data-stu-id="a7100-113">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="a7100-114">Następnie użyj właściwości [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) , aby uzyskać interfejs do operacji żądania relacji klienta.</span><span class="sxs-lookup"><span data-stu-id="a7100-114">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="a7100-115">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) w celu pobrania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a7100-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="a7100-116">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a7100-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a7100-117">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="a7100-117">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a7100-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a7100-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a7100-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a7100-119">Request syntax</span></span>

| <span data-ttu-id="a7100-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="a7100-120">Method</span></span>  | <span data-ttu-id="a7100-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a7100-121">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="a7100-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a7100-122">**GET**</span></span> | <span data-ttu-id="a7100-123">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/relationshiprequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="a7100-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a7100-124">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a7100-124">Request headers</span></span>

<span data-ttu-id="a7100-125">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a7100-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a7100-126">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a7100-126">Request body</span></span>

<span data-ttu-id="a7100-127">Brak</span><span class="sxs-lookup"><span data-stu-id="a7100-127">None</span></span>

### <a name="request-example"></a><span data-ttu-id="a7100-128">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a7100-128">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a7100-129">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a7100-129">REST response</span></span>

<span data-ttu-id="a7100-130">Jeśli to się powiedzie, odpowiedź zawiera obiekt [RelationshipRequest](relationships-resources.md#relationshiprequest) .</span><span class="sxs-lookup"><span data-stu-id="a7100-130">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a7100-131">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a7100-131">Response success and error codes</span></span>

<span data-ttu-id="a7100-132">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="a7100-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a7100-133">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a7100-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a7100-134">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a7100-134">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a7100-135">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a7100-135">Response example</span></span>

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
