---
title: Pobieranie listy subskrypcji według zamówienia
description: Pobiera kolekcję zasobów subskrypcji, które odpowiadają danej kolejności.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 56b9c80021cace03976d410b2a6cd4c0eee18398
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768242"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="f7781-103">Pobieranie listy subskrypcji według zamówienia</span><span class="sxs-lookup"><span data-stu-id="f7781-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="f7781-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="f7781-104">**Applies To**</span></span>

- <span data-ttu-id="f7781-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="f7781-105">Partner Center</span></span>
- <span data-ttu-id="f7781-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f7781-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f7781-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="f7781-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f7781-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f7781-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f7781-109">Pobiera kolekcję zasobów [subskrypcji](subscription-resources.md) , które odpowiadają danej kolejności.</span><span class="sxs-lookup"><span data-stu-id="f7781-109">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7781-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7781-110">Prerequisites</span></span>

- <span data-ttu-id="f7781-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f7781-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7781-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7781-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f7781-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7781-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f7781-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="f7781-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f7781-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="f7781-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f7781-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="f7781-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f7781-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="f7781-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f7781-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7781-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f7781-119">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="f7781-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="f7781-120">C\#</span><span class="sxs-lookup"><span data-stu-id="f7781-120">C\#</span></span>

<span data-ttu-id="f7781-121">Aby uzyskać listę subskrypcji według kolejności, Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="f7781-121">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="f7781-122">Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę **ByOrder ()** .</span><span class="sxs-lookup"><span data-stu-id="f7781-122">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="f7781-123">Zakończ, wywołując metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span><span class="sxs-lookup"><span data-stu-id="f7781-123">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="f7781-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7781-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f7781-125">**Project**: PartnerSDK. FeatureSample **Klasa**: SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="f7781-125">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f7781-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f7781-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7781-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f7781-127">Request syntax</span></span>

| <span data-ttu-id="f7781-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="f7781-128">Method</span></span>  | <span data-ttu-id="f7781-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f7781-129">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f7781-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f7781-130">**GET**</span></span> | <span data-ttu-id="f7781-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions? \_ Identyfikator zamówienia = {ID-for-Order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f7781-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f7781-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f7781-132">URI parameter</span></span>

<span data-ttu-id="f7781-133">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f7781-133">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="f7781-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f7781-134">Name</span></span>                   | <span data-ttu-id="f7781-135">Typ</span><span class="sxs-lookup"><span data-stu-id="f7781-135">Type</span></span>     | <span data-ttu-id="f7781-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f7781-136">Required</span></span> | <span data-ttu-id="f7781-137">Opis</span><span class="sxs-lookup"><span data-stu-id="f7781-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="f7781-138">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="f7781-138">**customer-tenant-id**</span></span> | <span data-ttu-id="f7781-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7781-139">**guid**</span></span> | <span data-ttu-id="f7781-140">Y</span><span class="sxs-lookup"><span data-stu-id="f7781-140">Y</span></span>        | <span data-ttu-id="f7781-141">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="f7781-141">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="f7781-142">**Identyfikator — dla zamówienia**</span><span class="sxs-lookup"><span data-stu-id="f7781-142">**id-for-order**</span></span>       | <span data-ttu-id="f7781-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7781-143">**guid**</span></span> | <span data-ttu-id="f7781-144">Y</span><span class="sxs-lookup"><span data-stu-id="f7781-144">Y</span></span>        | <span data-ttu-id="f7781-145">Identyfikator GUID odpowiadający kolejności.</span><span class="sxs-lookup"><span data-stu-id="f7781-145">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="f7781-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f7781-146">Request headers</span></span>

<span data-ttu-id="f7781-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f7781-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7781-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f7781-148">Request body</span></span>

<span data-ttu-id="f7781-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="f7781-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f7781-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f7781-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="f7781-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f7781-151">REST response</span></span>

<span data-ttu-id="f7781-152">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f7781-152">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7781-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f7781-153">Response success and error codes</span></span>

<span data-ttu-id="f7781-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="f7781-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7781-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f7781-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7781-156">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f7781-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f7781-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f7781-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "{id-for-order}",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
