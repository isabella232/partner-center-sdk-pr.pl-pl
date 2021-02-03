---
title: Pobieranie wszystkich zamówień klienta
description: Pobiera kolekcję wszystkich zamówień dla określonego klienta.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4d71cd138421704d94a55a9fe21e074d92638815
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768358"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="22618-103">Pobieranie wszystkich zamówień klienta</span><span class="sxs-lookup"><span data-stu-id="22618-103">Get all of a customer's orders</span></span>

<span data-ttu-id="22618-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="22618-104">**Applies to:**</span></span>

- <span data-ttu-id="22618-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="22618-105">Partner Center</span></span>
- <span data-ttu-id="22618-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="22618-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="22618-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="22618-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="22618-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="22618-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="22618-109">Pobiera kolekcję wszystkich zamówień dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="22618-109">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="22618-110">Istnieje opóźnienie do 15 minut od momentu, gdy zamówienie zostanie przesłane i pojawi się w kolekcji zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="22618-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22618-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22618-111">Prerequisites</span></span>

- <span data-ttu-id="22618-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="22618-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="22618-113">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22618-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="22618-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="22618-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="22618-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="22618-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="22618-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="22618-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="22618-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="22618-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="22618-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="22618-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="22618-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="22618-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="22618-120">C\#</span><span class="sxs-lookup"><span data-stu-id="22618-120">C\#</span></span>

<span data-ttu-id="22618-121">Aby uzyskać kolekcję wszystkich zamówień klienta:</span><span class="sxs-lookup"><span data-stu-id="22618-121">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="22618-122">Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="22618-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="22618-123">Wywołaj Właściwość [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , a następnie metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="22618-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="22618-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="22618-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="22618-125">**Project**: PartnerSDK. FeatureSamples **Klasa**: GetOrders.cs</span><span class="sxs-lookup"><span data-stu-id="22618-125">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="22618-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="22618-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="22618-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="22618-127">Request syntax</span></span>

| <span data-ttu-id="22618-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="22618-128">Method</span></span>  | <span data-ttu-id="22618-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="22618-129">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="22618-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="22618-130">**GET**</span></span> | <span data-ttu-id="22618-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="22618-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="22618-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="22618-132">URI parameter</span></span>

<span data-ttu-id="22618-133">Użyj następującego parametru zapytania, aby pobrać wszystkie zamówienia.</span><span class="sxs-lookup"><span data-stu-id="22618-133">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="22618-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="22618-134">Name</span></span>                   | <span data-ttu-id="22618-135">Typ</span><span class="sxs-lookup"><span data-stu-id="22618-135">Type</span></span>     | <span data-ttu-id="22618-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="22618-136">Required</span></span> | <span data-ttu-id="22618-137">Opis</span><span class="sxs-lookup"><span data-stu-id="22618-137">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="22618-138">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="22618-138">customer-tenant-id</span></span>     | <span data-ttu-id="22618-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="22618-139">string</span></span>   | <span data-ttu-id="22618-140">Tak</span><span class="sxs-lookup"><span data-stu-id="22618-140">Yes</span></span>      | <span data-ttu-id="22618-141">Ciąg w formacie GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="22618-141">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="22618-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="22618-142">Request headers</span></span>

<span data-ttu-id="22618-143">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="22618-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="22618-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="22618-144">Request body</span></span>

<span data-ttu-id="22618-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="22618-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="22618-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="22618-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="22618-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="22618-147">REST response</span></span>

<span data-ttu-id="22618-148">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [zamówienia](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="22618-148">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="22618-149">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="22618-149">Response success and error codes</span></span>

<span data-ttu-id="22618-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="22618-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="22618-151">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="22618-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="22618-152">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="22618-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="22618-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="22618-153">Response example</span></span>

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
