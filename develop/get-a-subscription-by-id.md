---
title: Pobieranie subskrypcji według identyfikatora
description: Pobiera zasób subskrypcji, który odpowiada identyfikatorowi klienta i identyfikatorowi subskrypcji.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 75f21a3f76e5502ba40b89995aa26bd0e668b3fa
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873823"
---
# <a name="get-a-subscription-by-id"></a><span data-ttu-id="e7c9b-103">Pobieranie subskrypcji według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="e7c9b-103">Get a subscription by ID</span></span>

<span data-ttu-id="e7c9b-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e7c9b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e7c9b-105">Pobiera [zasób subskrypcji,](subscription-resources.md) który odpowiada identyfikatorowi klienta i identyfikatorowi subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-105">Gets a [Subscription](subscription-resources.md) resource that matches the customer ID and the subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7c9b-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e7c9b-106">Prerequisites</span></span>

- <span data-ttu-id="e7c9b-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e7c9b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e7c9b-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e7c9b-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e7c9b-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e7c9b-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e7c9b-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e7c9b-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="e7c9b-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e7c9b-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e7c9b-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e7c9b-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e7c9b-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e7c9b-115">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-115">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="e7c9b-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e7c9b-116">C\#</span></span>

<span data-ttu-id="e7c9b-117">Aby uzyskać subskrypcję według identyfikatora, zacznij od uzyskania interfejsu dla operacji subskrypcji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, oraz metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) w celu zidentyfikowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-117">To get a subscription by ID, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription.</span></span> <span data-ttu-id="e7c9b-118">Użyj tego [**interfejsu,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) aby pobrać szczegóły subskrypcji, wywołując [**get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="e7c9b-118">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

<span data-ttu-id="e7c9b-119">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e7c9b-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e7c9b-120">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa:** GetSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="e7c9b-120">**Project**: Partner Center SDK Samples **Class**: GetSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e7c9b-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e7c9b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e7c9b-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e7c9b-122">Request syntax</span></span>

| <span data-ttu-id="e7c9b-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="e7c9b-123">Method</span></span>  | <span data-ttu-id="e7c9b-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e7c9b-124">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e7c9b-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e7c9b-125">**GET**</span></span> | <span data-ttu-id="e7c9b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e7c9b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e7c9b-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e7c9b-127">URI parameter</span></span>

<span data-ttu-id="e7c9b-128">Ta tabela zawiera listę parametrów zapytania wymaganych do uzyskania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-128">This table lists the required query parameters to get the subscription.</span></span>

| <span data-ttu-id="e7c9b-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e7c9b-129">Name</span></span>                    | <span data-ttu-id="e7c9b-130">Typ</span><span class="sxs-lookup"><span data-stu-id="e7c9b-130">Type</span></span>     | <span data-ttu-id="e7c9b-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e7c9b-131">Required</span></span> | <span data-ttu-id="e7c9b-132">Opis</span><span class="sxs-lookup"><span data-stu-id="e7c9b-132">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="e7c9b-133">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="e7c9b-133">**customer-tenant-id**</span></span>  | <span data-ttu-id="e7c9b-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="e7c9b-134">**guid**</span></span> | <span data-ttu-id="e7c9b-135">Y</span><span class="sxs-lookup"><span data-stu-id="e7c9b-135">Y</span></span>        | <span data-ttu-id="e7c9b-136">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-136">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="e7c9b-137">**identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="e7c9b-137">**id-for-subscription**</span></span> | <span data-ttu-id="e7c9b-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="e7c9b-138">**guid**</span></span> | <span data-ttu-id="e7c9b-139">Y</span><span class="sxs-lookup"><span data-stu-id="e7c9b-139">Y</span></span>        | <span data-ttu-id="e7c9b-140">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-140">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e7c9b-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e7c9b-141">Request headers</span></span>

<span data-ttu-id="e7c9b-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e7c9b-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e7c9b-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e7c9b-143">Request body</span></span>

<span data-ttu-id="e7c9b-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e7c9b-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e7c9b-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e7c9b-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e7c9b-146">REST response</span></span>

<span data-ttu-id="e7c9b-147">W przypadku powodzenia ta metoda zwraca [zasób Subscription](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-147">If successful, this method returns a [Subscription](subscription-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e7c9b-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e7c9b-148">Response success and error codes</span></span>

<span data-ttu-id="e7c9b-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e7c9b-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e7c9b-151">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e7c9b-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-a-standard-subscription"></a><span data-ttu-id="e7c9b-152">Przykład odpowiedzi dla subskrypcji standardowej</span><span class="sxs-lookup"><span data-stu-id="e7c9b-152">Response example for a standard subscription</span></span>

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

### <a name="response-example-for-an-add-on-subscription"></a><span data-ttu-id="e7c9b-153">Przykład odpowiedzi dla subskrypcji dodatku</span><span class="sxs-lookup"><span data-stu-id="e7c9b-153">Response example for an add-on subscription</span></span>

<span data-ttu-id="e7c9b-154">Odpowiedź na subskrypcję dodatku zawiera identyfikator subskrypcji nadrzędnej w treści i linkach.</span><span class="sxs-lookup"><span data-stu-id="e7c9b-154">The response for an add-on subscription includes the parent subscription ID in the body and in the links.</span></span>

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
