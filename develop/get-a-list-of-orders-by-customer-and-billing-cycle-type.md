---
title: Pobieranie listy zamówień według klienta i typu cyklu rozliczeń
description: Pobiera kolekcję zasobów zamówień dla określonego typu klienta i cyklu rozliczeniowego.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c52a556887dba065c4ccd1a82d6223624d0ad1f2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874231"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="1aabe-103">Pobieranie listy zamówień według klienta i typu cyklu rozliczeń</span><span class="sxs-lookup"><span data-stu-id="1aabe-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="1aabe-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1aabe-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1aabe-105">Pobiera kolekcję zasobów zamówienia, które odpowiadają danemu typowi klienta i cyklu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="1aabe-105">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="1aabe-106">Istnieje opóźnienie do 15 minut od czasu, w którym zamówienie zostanie przesłane, a kiedy pojawi się w kolekcji zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="1aabe-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aabe-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1aabe-107">Prerequisites</span></span>

- <span data-ttu-id="1aabe-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1aabe-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1aabe-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1aabe-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1aabe-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1aabe-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1aabe-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1aabe-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1aabe-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="1aabe-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1aabe-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="1aabe-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1aabe-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="1aabe-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1aabe-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1aabe-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1aabe-116">C\#</span><span class="sxs-lookup"><span data-stu-id="1aabe-116">C\#</span></span>

<span data-ttu-id="1aabe-117">Aby uzyskać kolekcję zamówień klienta:</span><span class="sxs-lookup"><span data-stu-id="1aabe-117">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="1aabe-118">Użyj [**kolekcji IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z wybranym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="1aabe-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="1aabe-119">Wywołaj [**właściwość Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) i metodę **ByBillingCycleType() przy** użyciu określonego typu  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="1aabe-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="1aabe-120">Wywołaj [**metodę Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="1aabe-120">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="1aabe-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1aabe-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1aabe-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1aabe-122">Request syntax</span></span>

| <span data-ttu-id="1aabe-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="1aabe-123">Method</span></span>  | <span data-ttu-id="1aabe-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1aabe-124">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1aabe-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1aabe-125">**GET**</span></span> | <span data-ttu-id="1aabe-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1aabe-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="1aabe-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="1aabe-127">URI parameters</span></span>

<span data-ttu-id="1aabe-128">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania kolekcji zamówień według identyfikatora klienta i typu cyklu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="1aabe-128">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="1aabe-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1aabe-129">Name</span></span>                   | <span data-ttu-id="1aabe-130">Typ</span><span class="sxs-lookup"><span data-stu-id="1aabe-130">Type</span></span>     | <span data-ttu-id="1aabe-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1aabe-131">Required</span></span> | <span data-ttu-id="1aabe-132">Opis</span><span class="sxs-lookup"><span data-stu-id="1aabe-132">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="1aabe-133">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="1aabe-133">customer-tenant-id</span></span>     | <span data-ttu-id="1aabe-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aabe-134">string</span></span>   | <span data-ttu-id="1aabe-135">Tak</span><span class="sxs-lookup"><span data-stu-id="1aabe-135">Yes</span></span>      | <span data-ttu-id="1aabe-136">Ciąg sformatowany identyfikatora GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="1aabe-136">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="1aabe-137">typ cyklu rozliczeniowego</span><span class="sxs-lookup"><span data-stu-id="1aabe-137">billing-cycle-type</span></span>     | <span data-ttu-id="1aabe-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aabe-138">string</span></span>   | <span data-ttu-id="1aabe-139">Nie</span><span class="sxs-lookup"><span data-stu-id="1aabe-139">No</span></span>       | <span data-ttu-id="1aabe-140">Ciąg odpowiadający typowi cyklu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="1aabe-140">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="1aabe-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1aabe-141">Request headers</span></span>

<span data-ttu-id="1aabe-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1aabe-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1aabe-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1aabe-143">Request body</span></span>

<span data-ttu-id="1aabe-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="1aabe-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1aabe-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1aabe-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="1aabe-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1aabe-146">REST response</span></span>

<span data-ttu-id="1aabe-147">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [Order](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1aabe-147">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1aabe-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1aabe-148">Response success and error codes</span></span>

<span data-ttu-id="1aabe-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1aabe-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1aabe-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1aabe-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1aabe-151">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1aabe-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1aabe-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1aabe-152">Response example</span></span>

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
