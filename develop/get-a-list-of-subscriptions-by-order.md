---
title: Pobieranie listy subskrypcji według zamówienia
description: Pobiera kolekcję zasobów subskrypcji, które odpowiadają podanemu zamówieniu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 011a92500d0c7ed44f86030febd1ea83be2c6474
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873959"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="83f65-103">Pobieranie listy subskrypcji według zamówienia</span><span class="sxs-lookup"><span data-stu-id="83f65-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="83f65-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="83f65-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="83f65-105">Pobiera kolekcję [zasobów subskrypcji,](subscription-resources.md) które odpowiadają podanemu zamówieniu.</span><span class="sxs-lookup"><span data-stu-id="83f65-105">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83f65-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83f65-106">Prerequisites</span></span>

- <span data-ttu-id="83f65-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="83f65-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="83f65-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="83f65-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="83f65-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="83f65-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="83f65-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="83f65-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="83f65-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="83f65-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="83f65-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="83f65-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="83f65-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="83f65-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="83f65-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="83f65-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="83f65-115">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="83f65-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="83f65-116">C\#</span><span class="sxs-lookup"><span data-stu-id="83f65-116">C\#</span></span>

<span data-ttu-id="83f65-117">Aby uzyskać listę subskrypcji według zamówienia, użyj kolekcji **IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="83f65-117">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="83f65-118">Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę **ByOrder().**</span><span class="sxs-lookup"><span data-stu-id="83f65-118">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="83f65-119">Zakończ, wywołując [**get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) lub [**getasync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span><span class="sxs-lookup"><span data-stu-id="83f65-119">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="83f65-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="83f65-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="83f65-121">**Project:** PartnerSDK.FeatureSample, **klasa**: SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="83f65-121">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="83f65-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="83f65-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="83f65-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="83f65-123">Request syntax</span></span>

| <span data-ttu-id="83f65-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="83f65-124">Method</span></span>  | <span data-ttu-id="83f65-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="83f65-125">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="83f65-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="83f65-126">**GET**</span></span> | <span data-ttu-id="83f65-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order \_ id={id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="83f65-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="83f65-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="83f65-128">URI parameter</span></span>

<span data-ttu-id="83f65-129">W tej tabeli wymieniono parametr zapytania wymagany do uzyskania wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="83f65-129">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="83f65-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="83f65-130">Name</span></span>                   | <span data-ttu-id="83f65-131">Typ</span><span class="sxs-lookup"><span data-stu-id="83f65-131">Type</span></span>     | <span data-ttu-id="83f65-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="83f65-132">Required</span></span> | <span data-ttu-id="83f65-133">Opis</span><span class="sxs-lookup"><span data-stu-id="83f65-133">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="83f65-134">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="83f65-134">**customer-tenant-id**</span></span> | <span data-ttu-id="83f65-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="83f65-135">**guid**</span></span> | <span data-ttu-id="83f65-136">Y</span><span class="sxs-lookup"><span data-stu-id="83f65-136">Y</span></span>        | <span data-ttu-id="83f65-137">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="83f65-137">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="83f65-138">**id-for-order**</span><span class="sxs-lookup"><span data-stu-id="83f65-138">**id-for-order**</span></span>       | <span data-ttu-id="83f65-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="83f65-139">**guid**</span></span> | <span data-ttu-id="83f65-140">Y</span><span class="sxs-lookup"><span data-stu-id="83f65-140">Y</span></span>        | <span data-ttu-id="83f65-141">Identyfikator GUID odpowiadający kolejności.</span><span class="sxs-lookup"><span data-stu-id="83f65-141">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="83f65-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="83f65-142">Request headers</span></span>

<span data-ttu-id="83f65-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="83f65-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="83f65-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="83f65-144">Request body</span></span>

<span data-ttu-id="83f65-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="83f65-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="83f65-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="83f65-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="83f65-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="83f65-147">REST response</span></span>

<span data-ttu-id="83f65-148">W przypadku powodzenia ta metoda zwraca [kolekcję](subscription-resources.md) zasobów subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="83f65-148">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="83f65-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="83f65-149">Response success and error codes</span></span>

<span data-ttu-id="83f65-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="83f65-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="83f65-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="83f65-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="83f65-152">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="83f65-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="83f65-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="83f65-153">Response example</span></span>

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
