---
title: Pobieranie subskrypcji klienta
description: Jak uzyskać kolekcję subskrypcji klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a037e4a81fccbff0a02b0bdf6d93478ee15fd50f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768353"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="8b204-103">Pobieranie subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="8b204-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="8b204-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="8b204-104">**Applies To**</span></span>

- <span data-ttu-id="8b204-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="8b204-105">Partner Center</span></span>
- <span data-ttu-id="8b204-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8b204-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8b204-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="8b204-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8b204-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8b204-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8b204-109">Jak uzyskać kolekcję subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="8b204-109">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b204-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b204-110">Prerequisites</span></span>

- <span data-ttu-id="8b204-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8b204-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8b204-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b204-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8b204-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8b204-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8b204-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="8b204-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8b204-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="8b204-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8b204-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="8b204-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8b204-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="8b204-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8b204-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8b204-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8b204-119">C\#</span><span class="sxs-lookup"><span data-stu-id="8b204-119">C\#</span></span>

<span data-ttu-id="8b204-120">Aby uzyskać listę wszystkich subskrypcji klienta, należy najpierw użyć metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="8b204-120">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="8b204-121">Następnie użyj właściwości [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , aby pobrać interfejs do operacji zbierania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8b204-121">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="8b204-122">Na koniec wywołaj metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby pobrać kolekcję subskrypcje klienta.</span><span class="sxs-lookup"><span data-stu-id="8b204-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="8b204-123">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b204-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8b204-124">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="8b204-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8b204-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8b204-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8b204-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8b204-126">Request syntax</span></span>

| <span data-ttu-id="8b204-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="8b204-127">Method</span></span>  | <span data-ttu-id="8b204-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8b204-128">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b204-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="8b204-129">**GET**</span></span> | <span data-ttu-id="8b204-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions http/1.1</span><span class="sxs-lookup"><span data-stu-id="8b204-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8b204-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8b204-131">URI parameter</span></span>

<span data-ttu-id="8b204-132">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8b204-132">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="8b204-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8b204-133">Name</span></span>               | <span data-ttu-id="8b204-134">Typ</span><span class="sxs-lookup"><span data-stu-id="8b204-134">Type</span></span>   | <span data-ttu-id="8b204-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8b204-135">Required</span></span> | <span data-ttu-id="8b204-136">Opis</span><span class="sxs-lookup"><span data-stu-id="8b204-136">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8b204-137">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="8b204-137">customer-tenant-id</span></span> | <span data-ttu-id="8b204-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="8b204-138">string</span></span> | <span data-ttu-id="8b204-139">Tak</span><span class="sxs-lookup"><span data-stu-id="8b204-139">Yes</span></span>      | <span data-ttu-id="8b204-140">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="8b204-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8b204-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8b204-141">Request headers</span></span>

<span data-ttu-id="8b204-142">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8b204-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8b204-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8b204-143">Request body</span></span>

<span data-ttu-id="8b204-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="8b204-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8b204-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8b204-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8b204-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8b204-146">REST response</span></span>

<span data-ttu-id="8b204-147">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8b204-147">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8b204-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b204-148">Response success and error codes</span></span>

<span data-ttu-id="8b204-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="8b204-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8b204-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8b204-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8b204-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8b204-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8b204-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b204-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
Date: Wed, 25 Nov 2015 05:43:06 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "nickname",
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
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
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
