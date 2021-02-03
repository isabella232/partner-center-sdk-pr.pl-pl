---
title: Pobieranie zamówienia według identyfikatora
description: Pobiera zasób zamówienia, który odpowiada IDENTYFIKATORowi klienta i zamówienia.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 0a39d7142e5bf97f9fb345416964d4ed6bb935ad
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768454"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="db5bf-103">Pobieranie zamówienia według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="db5bf-103">Get an order by ID</span></span>

<span data-ttu-id="db5bf-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="db5bf-104">**Applies to:**</span></span>

- <span data-ttu-id="db5bf-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="db5bf-105">Partner Center</span></span>
- <span data-ttu-id="db5bf-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="db5bf-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="db5bf-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="db5bf-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="db5bf-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="db5bf-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="db5bf-109">Pobiera zasób [zamówienia](order-resources.md) , który odpowiada identyfikatorowi klienta i zamówienia.</span><span class="sxs-lookup"><span data-stu-id="db5bf-109">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db5bf-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="db5bf-110">Prerequisites</span></span>

- <span data-ttu-id="db5bf-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="db5bf-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="db5bf-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="db5bf-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="db5bf-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db5bf-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="db5bf-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="db5bf-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="db5bf-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="db5bf-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="db5bf-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="db5bf-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="db5bf-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="db5bf-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="db5bf-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db5bf-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="db5bf-119">Identyfikator zamówienia.</span><span class="sxs-lookup"><span data-stu-id="db5bf-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="db5bf-120">C\#</span><span class="sxs-lookup"><span data-stu-id="db5bf-120">C\#</span></span>

<span data-ttu-id="db5bf-121">Aby uzyskać zamówienie klienta według identyfikatora:</span><span class="sxs-lookup"><span data-stu-id="db5bf-121">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="db5bf-122">Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="db5bf-122">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="db5bf-123">Wywołaj Właściwość [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , a następnie metodę [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) jeszcze raz.</span><span class="sxs-lookup"><span data-stu-id="db5bf-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="db5bf-124">Wywołanie [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span><span class="sxs-lookup"><span data-stu-id="db5bf-124">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="db5bf-125">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="db5bf-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="db5bf-126">**Project**: PartnerSDK. FeatureSample **Klasa**: GetOrder.cs</span><span class="sxs-lookup"><span data-stu-id="db5bf-126">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="db5bf-127">Java</span><span class="sxs-lookup"><span data-stu-id="db5bf-127">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="db5bf-128">Aby uzyskać zamówienie klienta według identyfikatora:</span><span class="sxs-lookup"><span data-stu-id="db5bf-128">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="db5bf-129">Użyj funkcji **IAggregatePartner. GetCustomers** i wywołaj funkcję **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="db5bf-129">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="db5bf-130">Wywołaj funkcję **GetOrders** , a następnie funkcję **byID ()** jeszcze raz.</span><span class="sxs-lookup"><span data-stu-id="db5bf-130">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="db5bf-131">Wywołaj funkcję **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="db5bf-131">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="db5bf-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db5bf-132">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="db5bf-133">Aby uzyskać identyfikator zamówienia klienta według identyfikatora, należy wykonać polecenie [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) i określić parametry **CustomerID** i **IDZamówienia** .</span><span class="sxs-lookup"><span data-stu-id="db5bf-133">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="db5bf-134">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="db5bf-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="db5bf-135">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="db5bf-135">Request syntax</span></span>

| <span data-ttu-id="db5bf-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="db5bf-136">Method</span></span>  | <span data-ttu-id="db5bf-137">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="db5bf-137">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="db5bf-138">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="db5bf-138">**GET**</span></span> | <span data-ttu-id="db5bf-139">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{ID-for-Order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="db5bf-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="db5bf-140">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="db5bf-140">URI parameters</span></span>

<span data-ttu-id="db5bf-141">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania identyfikatora order by.</span><span class="sxs-lookup"><span data-stu-id="db5bf-141">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="db5bf-142">Nazwa</span><span class="sxs-lookup"><span data-stu-id="db5bf-142">Name</span></span>                   | <span data-ttu-id="db5bf-143">Typ</span><span class="sxs-lookup"><span data-stu-id="db5bf-143">Type</span></span>     | <span data-ttu-id="db5bf-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="db5bf-144">Required</span></span> | <span data-ttu-id="db5bf-145">Opis</span><span class="sxs-lookup"><span data-stu-id="db5bf-145">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="db5bf-146">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="db5bf-146">customer-tenant-id</span></span>     | <span data-ttu-id="db5bf-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="db5bf-147">string</span></span>   | <span data-ttu-id="db5bf-148">Tak</span><span class="sxs-lookup"><span data-stu-id="db5bf-148">Yes</span></span>      | <span data-ttu-id="db5bf-149">Ciąg w formacie GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="db5bf-149">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="db5bf-150">Identyfikator — dla zamówienia</span><span class="sxs-lookup"><span data-stu-id="db5bf-150">id-for-order</span></span>           | <span data-ttu-id="db5bf-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="db5bf-151">string</span></span>   | <span data-ttu-id="db5bf-152">Tak</span><span class="sxs-lookup"><span data-stu-id="db5bf-152">Yes</span></span>      | <span data-ttu-id="db5bf-153">Ciąg odpowiadający IDENTYFIKATORowi zamówienia.</span><span class="sxs-lookup"><span data-stu-id="db5bf-153">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="db5bf-154">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="db5bf-154">Request headers</span></span>

<span data-ttu-id="db5bf-155">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="db5bf-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="db5bf-156">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="db5bf-156">Request body</span></span>

<span data-ttu-id="db5bf-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="db5bf-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="db5bf-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="db5bf-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="db5bf-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="db5bf-159">REST response</span></span>

<span data-ttu-id="db5bf-160">Jeśli to się powiedzie, ta metoda zwraca zasób [zamówienia](order-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="db5bf-160">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="db5bf-161">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="db5bf-161">Response success and error codes</span></span>

<span data-ttu-id="db5bf-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="db5bf-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="db5bf-163">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="db5bf-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="db5bf-164">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="db5bf-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="db5bf-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="db5bf-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
