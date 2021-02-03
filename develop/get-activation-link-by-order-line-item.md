---
title: Pobieranie linku aktywacji według elementu wiersza zamówienia
description: Pobiera link aktywacji subskrypcji według elementu Order line.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768053"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="81b16-103">Pobieranie linku aktywacji według elementu wiersza zamówienia</span><span class="sxs-lookup"><span data-stu-id="81b16-103">Get activation link by order line item</span></span>

<span data-ttu-id="81b16-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="81b16-104">**Applies To**</span></span>

- <span data-ttu-id="81b16-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="81b16-105">Partner Center</span></span>
- <span data-ttu-id="81b16-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="81b16-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="81b16-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="81b16-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="81b16-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="81b16-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="81b16-109">Pobiera komercyjne łącze aktywacji subskrypcji portalu Marketplace według numeru elementu wiersza zamówienia.</span><span class="sxs-lookup"><span data-stu-id="81b16-109">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="81b16-110">Na pulpicie nawigacyjnym Centrum partnerskiego możesz wykonać tę operację, wybierając wybraną **subskrypcję** w obszarze **subskrypcja** na stronie głównej lub klikając link **do witryny przejdź do wydawcy** obok subskrypcji w celu aktywowania na stronie **subskrypcje** .</span><span class="sxs-lookup"><span data-stu-id="81b16-110">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81b16-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="81b16-111">Prerequisites</span></span>

- <span data-ttu-id="81b16-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="81b16-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="81b16-113">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="81b16-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="81b16-114">Zakończono zamówienie z produktem, który wymaga aktywacji.</span><span class="sxs-lookup"><span data-stu-id="81b16-114">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="81b16-115">C\#</span><span class="sxs-lookup"><span data-stu-id="81b16-115">C\#</span></span>

<span data-ttu-id="81b16-116">Aby uzyskać łącze aktywacji elementu wiersza, Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu wybranego identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="81b16-116">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="81b16-117">Następnie Wywołaj Właściwość [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) i metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) z określonym identyfikatorem  [**IDZamówienia**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span><span class="sxs-lookup"><span data-stu-id="81b16-117">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="81b16-118">Następnie Wywołaj metodę [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) z **ById ()** z identyfikatorem numeru elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="81b16-118">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="81b16-119">Na koniec Wywołaj metodę **ActivationLinks ()** .</span><span class="sxs-lookup"><span data-stu-id="81b16-119">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="81b16-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="81b16-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="81b16-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="81b16-121">Request syntax</span></span>

| <span data-ttu-id="81b16-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="81b16-122">Method</span></span>  | <span data-ttu-id="81b16-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="81b16-123">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="81b16-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="81b16-124">**GET**</span></span> | <span data-ttu-id="81b16-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{customerId}/Orders/{OrderID}/LineItems/{lineItemNumber}/activationlinks http/1.1</span><span class="sxs-lookup"><span data-stu-id="81b16-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="81b16-126">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="81b16-126">Request headers</span></span>

<span data-ttu-id="81b16-127">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="81b16-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="81b16-128">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="81b16-128">Request body</span></span>

<span data-ttu-id="81b16-129">Brak.</span><span class="sxs-lookup"><span data-stu-id="81b16-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="81b16-130">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="81b16-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="81b16-131">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="81b16-131">REST response</span></span>

<span data-ttu-id="81b16-132">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [klienta](customer-resources.md#customer) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="81b16-132">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="81b16-133">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="81b16-133">Response success and error codes</span></span>

<span data-ttu-id="81b16-134">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="81b16-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="81b16-135">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="81b16-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="81b16-136">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="81b16-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="81b16-137">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="81b16-137">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
