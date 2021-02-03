---
title: Pobieranie subskrypcji według identyfikatora
description: Pobiera zasób subskrypcji, który jest zgodny z IDENTYFIKATORem klienta i IDENTYFIKATORem subskrypcji.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6690a6886eeb31a78cdb556280d4bdc2b4beb124
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768293"
---
# <a name="get-a-subscription-by-id"></a><span data-ttu-id="081b6-103">Pobieranie subskrypcji według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="081b6-103">Get a subscription by ID</span></span>

<span data-ttu-id="081b6-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="081b6-104">**Applies To**</span></span>

- <span data-ttu-id="081b6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="081b6-105">Partner Center</span></span>
- <span data-ttu-id="081b6-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="081b6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="081b6-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="081b6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="081b6-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="081b6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="081b6-109">Pobiera zasób [subskrypcji](subscription-resources.md) , który jest zgodny z identyfikatorem klienta i identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="081b6-109">Gets a [Subscription](subscription-resources.md) resource that matches the customer ID and the subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="081b6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="081b6-110">Prerequisites</span></span>

- <span data-ttu-id="081b6-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="081b6-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="081b6-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="081b6-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="081b6-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="081b6-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="081b6-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="081b6-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="081b6-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="081b6-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="081b6-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="081b6-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="081b6-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="081b6-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="081b6-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="081b6-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="081b6-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="081b6-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="081b6-120">C\#</span><span class="sxs-lookup"><span data-stu-id="081b6-120">C\#</span></span>

<span data-ttu-id="081b6-121">Aby uzyskać subskrypcję według identyfikatora, Zacznij od uzyskania interfejsu do operacji subskrypcji przez wywołanie metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="081b6-121">To get a subscription by ID, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription.</span></span> <span data-ttu-id="081b6-122">Użyj tego [**interfejsu**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) , aby pobrać szczegóły subskrypcji przez wywołanie metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="081b6-122">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

<span data-ttu-id="081b6-123">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="081b6-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="081b6-124">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="081b6-124">**Project**: Partner Center SDK Samples **Class**: GetSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="081b6-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="081b6-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="081b6-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="081b6-126">Request syntax</span></span>

| <span data-ttu-id="081b6-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="081b6-127">Method</span></span>  | <span data-ttu-id="081b6-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="081b6-128">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="081b6-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="081b6-129">**GET**</span></span> | <span data-ttu-id="081b6-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="081b6-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="081b6-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="081b6-131">URI parameter</span></span>

<span data-ttu-id="081b6-132">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="081b6-132">This table lists the required query parameters to get the subscription.</span></span>

| <span data-ttu-id="081b6-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="081b6-133">Name</span></span>                    | <span data-ttu-id="081b6-134">Typ</span><span class="sxs-lookup"><span data-stu-id="081b6-134">Type</span></span>     | <span data-ttu-id="081b6-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="081b6-135">Required</span></span> | <span data-ttu-id="081b6-136">Opis</span><span class="sxs-lookup"><span data-stu-id="081b6-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="081b6-137">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="081b6-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="081b6-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="081b6-138">**guid**</span></span> | <span data-ttu-id="081b6-139">Y</span><span class="sxs-lookup"><span data-stu-id="081b6-139">Y</span></span>        | <span data-ttu-id="081b6-140">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="081b6-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="081b6-141">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="081b6-141">**id-for-subscription**</span></span> | <span data-ttu-id="081b6-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="081b6-142">**guid**</span></span> | <span data-ttu-id="081b6-143">Y</span><span class="sxs-lookup"><span data-stu-id="081b6-143">Y</span></span>        | <span data-ttu-id="081b6-144">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="081b6-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="081b6-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="081b6-145">Request headers</span></span>

<span data-ttu-id="081b6-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="081b6-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="081b6-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="081b6-147">Request body</span></span>

<span data-ttu-id="081b6-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="081b6-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="081b6-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="081b6-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="081b6-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="081b6-150">REST response</span></span>

<span data-ttu-id="081b6-151">Jeśli to się powiedzie, ta metoda zwraca zasób [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="081b6-151">If successful, this method returns a [Subscription](subscription-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="081b6-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="081b6-152">Response success and error codes</span></span>

<span data-ttu-id="081b6-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="081b6-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="081b6-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="081b6-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="081b6-155">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="081b6-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-a-standard-subscription"></a><span data-ttu-id="081b6-156">Przykład odpowiedzi dla standardowej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="081b6-156">Response example for a standard subscription</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 833
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CV: 7v11Wa//5EuGEo+A.0
MS-ServerId: 202010406
Date: Fri, 27 Jan 2017 21:51:40 GMT

{
    "id": "A356AC8C-E310-44F4-BF85-C7F29044AF99",
    "entitlementId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
    "offerId": "MS-AZR-0145P",
    "offerName": "Microsoft Azure",
    "friendlyName": "Microsoft Azure",
    "quantity": 1,
    "unitType": "Usage-based",
    "creationDate": "2016-05-10T07:30:05.427Z",
    "effectiveStartDate": "2016-05-10T00:00:00Z",
    "commitmentEndDate": "9999-12-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": false,
    "billingType": "usage",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/MS-AZR-0145P?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "B23FDEDD-D6BD-415A-8B71-3624C81C9644",
    "attributes": {
        "etag": "eyJpZCI6ImEzNTZhYzhjLWUzMTAtNDRmNC1iZjg1LWM3ZjI5MDQ0YWY5OSIsInZlcnNpb24iOjJ9",
        "objectType": "Subscription"
    }
}
```

### <a name="response-example-for-an-add-on-subscription"></a><span data-ttu-id="081b6-157">Przykład odpowiedzi dla subskrypcji dodatku</span><span class="sxs-lookup"><span data-stu-id="081b6-157">Response example for an add-on subscription</span></span>

<span data-ttu-id="081b6-158">Odpowiedź na subskrypcję dodatku zawiera identyfikator subskrypcji nadrzędnej w treści i łącza.</span><span class="sxs-lookup"><span data-stu-id="081b6-158">The response for an add-on subscription includes the parent subscription ID in the body and in the links.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6eacec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 22bfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 27 Jan 2017 00:12:53 GMT

{
    "id": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
    "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
    "offerName": "Exchange Online Archiving for Exchange Online",
    "friendlyName": "Some friendly name",
    "quantity": 2,
    "unitType": "Licenses",
    "parentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
    "creationDate": "2017-01-25T23:01:08.693Z",
    "effectiveStartDate": "2017-01-25T00:00:00Z",
    "commitmentEndDate": "2018-02-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": true,
    "billingType": "license",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
            "method": "GET",
            "headers": []
        },
        "parentSubscription": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "CF3B0E37-BE0B-4CDD-B584-D1A97D98A922",
    "attributes": {
        "etag": "eyJpZCI6Ijk2OGJhMWNmLWMxNDYtNGFkZi1hMzAwLTMwOGRjZjcxOGVlZSIsInZlcnNpb24iOjF9",
        "objectType": "Subscription"
    }
}
```
