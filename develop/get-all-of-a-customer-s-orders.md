---
title: Pobieranie wszystkich zamówień klienta
description: Pobiera kolekcję wszystkich zamówień dla określonego klienta.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e8f23e90cbb5afb45e519e2c58fd0d3b9ea2de6a
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760304"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="52842-103">Pobieranie wszystkich zamówień klienta</span><span class="sxs-lookup"><span data-stu-id="52842-103">Get all of a customer's orders</span></span>

<span data-ttu-id="52842-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="52842-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52842-105">Pobiera kolekcję wszystkich zamówień dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="52842-105">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="52842-106">Istnieje opóźnienie do 15 minut od czasu, w którym zamówienie zostanie przesłane, a kiedy pojawi się w kolekcji zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="52842-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52842-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52842-107">Prerequisites</span></span>

- <span data-ttu-id="52842-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="52842-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="52842-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="52842-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="52842-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="52842-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="52842-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="52842-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="52842-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="52842-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="52842-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="52842-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="52842-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="52842-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="52842-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="52842-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="52842-116">C\#</span><span class="sxs-lookup"><span data-stu-id="52842-116">C\#</span></span>

<span data-ttu-id="52842-117">Aby uzyskać kolekcję wszystkich zamówień klienta:</span><span class="sxs-lookup"><span data-stu-id="52842-117">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="52842-118">Użyj [**kolekcji IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="52842-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="52842-119">Wywołaj [**właściwość Orders,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a następnie metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="52842-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="52842-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="52842-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="52842-121">**Project:** Klasa PartnerSDK.FeatureSamples: GetOrders.cs </span><span class="sxs-lookup"><span data-stu-id="52842-121">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="52842-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="52842-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52842-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="52842-123">Request syntax</span></span>

| <span data-ttu-id="52842-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="52842-124">Method</span></span>  | <span data-ttu-id="52842-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="52842-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="52842-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="52842-126">**GET**</span></span> | <span data-ttu-id="52842-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="52842-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="52842-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="52842-128">URI parameter</span></span>

<span data-ttu-id="52842-129">Użyj następującego parametru zapytania, aby uzyskać wszystkie zamówienia.</span><span class="sxs-lookup"><span data-stu-id="52842-129">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="52842-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="52842-130">Name</span></span>                   | <span data-ttu-id="52842-131">Typ</span><span class="sxs-lookup"><span data-stu-id="52842-131">Type</span></span>     | <span data-ttu-id="52842-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="52842-132">Required</span></span> | <span data-ttu-id="52842-133">Opis</span><span class="sxs-lookup"><span data-stu-id="52842-133">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="52842-134">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="52842-134">customer-tenant-id</span></span>     | <span data-ttu-id="52842-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="52842-135">string</span></span>   | <span data-ttu-id="52842-136">Tak</span><span class="sxs-lookup"><span data-stu-id="52842-136">Yes</span></span>      | <span data-ttu-id="52842-137">Ciąg sformatowany identyfikatora GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="52842-137">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="52842-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="52842-138">Request headers</span></span>

<span data-ttu-id="52842-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="52842-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52842-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="52842-140">Request body</span></span>

<span data-ttu-id="52842-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="52842-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52842-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="52842-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="52842-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="52842-143">REST response</span></span>

<span data-ttu-id="52842-144">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [Order](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="52842-144">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52842-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52842-145">Response success and error codes</span></span>

<span data-ttu-id="52842-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="52842-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52842-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="52842-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52842-148">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="52842-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52842-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52842-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
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
            "id": "eeba9d00-7b46-443a-917e-22887a8fc993",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "E59159FC-6F67-4599-B3CB-17FF4020F643",
                    "subscriptionId": "DB8C695B-1C3C-4C55-B697-771503DD46BF",
                    "friendlyName": "Azure Active Directory Premium P2",
                    "quantity": 1,
                    "links": {
                        "subscription": {
                            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/84A661C4-E949-4BD2-A560-ED7766FCAF2B/skus/E59159FC-6F67-4599-B3CB-17FF4020F643",
                            "method": "GET",
                            "headers": []
                        },
                        "provisioningStatus": {
                            "uri": "/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF/provisioningstatus",
                            "method": "GET",
                            "headers": []
                        }
                    }
            ],
            "creationDate": "2018-03-06T17:37:05.253-08:00",
            "status": "completed",
            "links": {
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/eeba9d00-7b46-443a-917e-22887a8fc993",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "etag": "eyJpZCI6ImVlYmE5ZDAwLTdiNDYtNDQzYS05MTdlLTIyODg3YThmYzk5MyIsInZlcnNpb24iOjF9",
                "objectType": "Order"
            }
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
         "objectType": "Collection"
    }
}
```
