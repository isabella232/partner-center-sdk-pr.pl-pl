---
title: Pobieranie linku aktywacji według elementu wiersza zamówienia
description: Pobiera link aktywacji subskrypcji według pozycji zamówienia.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760780"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="38d60-103">Pobieranie linku aktywacji według elementu wiersza zamówienia</span><span class="sxs-lookup"><span data-stu-id="38d60-103">Get activation link by order line item</span></span>

<span data-ttu-id="38d60-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="38d60-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="38d60-105">Pobiera link aktywacji subskrypcji platformy handlowej według numeru wiersza zamówienia.</span><span class="sxs-lookup"><span data-stu-id="38d60-105">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="38d60-106">Na pulpicie nawigacyjnym usługi Partner Center możesz wykonać tę  operację, wybierając pozycję Konkskrypcyjna subskrypcja w obszarze Subskrypcja na stronie głównej lub wybierając link Przejdź do witryny usługi **Publisher** obok subskrypcji, która ma zostać aktywowana na **stronie** Subskrypcje. </span><span class="sxs-lookup"><span data-stu-id="38d60-106">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38d60-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38d60-107">Prerequisites</span></span>

- <span data-ttu-id="38d60-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="38d60-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38d60-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38d60-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="38d60-110">Ukończono zamówienie z produktem, który wymaga aktywacji.</span><span class="sxs-lookup"><span data-stu-id="38d60-110">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="38d60-111">C\#</span><span class="sxs-lookup"><span data-stu-id="38d60-111">C\#</span></span>

<span data-ttu-id="38d60-112">Aby uzyskać link aktywacji elementu wiersza, użyj kolekcji [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z wybranym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="38d60-112">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="38d60-113">Następnie wywołaj [**właściwość Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) i metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) z określonymi  [**wartościami OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span><span class="sxs-lookup"><span data-stu-id="38d60-113">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="38d60-114">Następnie wywołaj metodę [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) z **metodą ById()** z identyfikatorem numeru elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="38d60-114">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="38d60-115">Na koniec wywołaj **metodę ActivationLinks().**</span><span class="sxs-lookup"><span data-stu-id="38d60-115">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="38d60-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="38d60-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38d60-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="38d60-117">Request syntax</span></span>

| <span data-ttu-id="38d60-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="38d60-118">Method</span></span>  | <span data-ttu-id="38d60-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="38d60-119">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="38d60-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="38d60-120">**GET**</span></span> | <span data-ttu-id="38d60-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="38d60-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="38d60-122">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="38d60-122">Request headers</span></span>

<span data-ttu-id="38d60-123">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="38d60-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38d60-124">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="38d60-124">Request body</span></span>

<span data-ttu-id="38d60-125">Brak.</span><span class="sxs-lookup"><span data-stu-id="38d60-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="38d60-126">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="38d60-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="38d60-127">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="38d60-127">REST response</span></span>

<span data-ttu-id="38d60-128">W przypadku powodzenia ta metoda zwraca kolekcję [zasobów](customer-resources.md#customer) klienta w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="38d60-128">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38d60-129">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38d60-129">Response success and error codes</span></span>

<span data-ttu-id="38d60-130">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="38d60-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38d60-131">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="38d60-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38d60-132">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="38d60-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38d60-133">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38d60-133">Response example</span></span>

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
