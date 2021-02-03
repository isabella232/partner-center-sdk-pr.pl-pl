---
title: Pobieranie listy zamówień według klienta i typu cyklu rozliczeń
description: Pobiera kolekcję zasobów zamówienia dla określonego typu cyklu klienta i rozliczeń.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 43fe08b0791851f915e2b39a25394db5ffd022ca
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768233"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="75861-103">Pobieranie listy zamówień według klienta i typu cyklu rozliczeń</span><span class="sxs-lookup"><span data-stu-id="75861-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="75861-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="75861-104">**Applies to:**</span></span>

- <span data-ttu-id="75861-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="75861-105">Partner Center</span></span>
- <span data-ttu-id="75861-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="75861-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="75861-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="75861-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="75861-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="75861-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="75861-109">Pobiera kolekcję zasobów zamówienia, które odpowiadają danemu typowi cyklu klienta i rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="75861-109">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="75861-110">Istnieje opóźnienie do 15 minut od momentu, gdy zamówienie zostanie przesłane i pojawi się w kolekcji zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="75861-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75861-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="75861-111">Prerequisites</span></span>

- <span data-ttu-id="75861-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="75861-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75861-113">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75861-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="75861-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="75861-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="75861-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="75861-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="75861-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="75861-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="75861-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="75861-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="75861-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="75861-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="75861-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="75861-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="75861-120">C\#</span><span class="sxs-lookup"><span data-stu-id="75861-120">C\#</span></span>

<span data-ttu-id="75861-121">Aby uzyskać kolekcję zamówień klienta:</span><span class="sxs-lookup"><span data-stu-id="75861-121">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="75861-122">Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu wybranego identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="75861-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="75861-123">Wywołaj Właściwość [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) i metodę **ByBillingCycleType ()** z określonym  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="75861-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="75861-124">Wywołaj metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="75861-124">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="75861-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="75861-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="75861-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="75861-126">Request syntax</span></span>

| <span data-ttu-id="75861-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="75861-127">Method</span></span>  | <span data-ttu-id="75861-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="75861-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="75861-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="75861-129">**GET**</span></span> | <span data-ttu-id="75861-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders? rozliczenia = {rozliczanie-typ cyklu} http/1.1</span><span class="sxs-lookup"><span data-stu-id="75861-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="75861-131">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="75861-131">URI parameters</span></span>

<span data-ttu-id="75861-132">W tej tabeli wymieniono wymagane parametry zapytania umożliwiające pobranie kolekcji zamówień według identyfikatora klienta i typu cyklu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="75861-132">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="75861-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="75861-133">Name</span></span>                   | <span data-ttu-id="75861-134">Typ</span><span class="sxs-lookup"><span data-stu-id="75861-134">Type</span></span>     | <span data-ttu-id="75861-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="75861-135">Required</span></span> | <span data-ttu-id="75861-136">Opis</span><span class="sxs-lookup"><span data-stu-id="75861-136">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="75861-137">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="75861-137">customer-tenant-id</span></span>     | <span data-ttu-id="75861-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="75861-138">string</span></span>   | <span data-ttu-id="75861-139">Tak</span><span class="sxs-lookup"><span data-stu-id="75861-139">Yes</span></span>      | <span data-ttu-id="75861-140">Ciąg w formacie GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="75861-140">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="75861-141">rozliczenia — typ cyklu</span><span class="sxs-lookup"><span data-stu-id="75861-141">billing-cycle-type</span></span>     | <span data-ttu-id="75861-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="75861-142">string</span></span>   | <span data-ttu-id="75861-143">Nie</span><span class="sxs-lookup"><span data-stu-id="75861-143">No</span></span>       | <span data-ttu-id="75861-144">Ciąg odpowiadający typowi cyklu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="75861-144">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="75861-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="75861-145">Request headers</span></span>

<span data-ttu-id="75861-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="75861-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="75861-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="75861-147">Request body</span></span>

<span data-ttu-id="75861-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="75861-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="75861-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="75861-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="75861-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="75861-150">REST response</span></span>

<span data-ttu-id="75861-151">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [zamówienia](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="75861-151">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="75861-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="75861-152">Response success and error codes</span></span>

<span data-ttu-id="75861-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="75861-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="75861-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="75861-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="75861-155">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="75861-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="75861-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="75861-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```
