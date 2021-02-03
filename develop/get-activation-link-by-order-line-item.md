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
# <a name="get-activation-link-by-order-line-item"></a>Pobieranie linku aktywacji według elementu wiersza zamówienia

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Pobiera komercyjne łącze aktywacji subskrypcji portalu Marketplace według numeru elementu wiersza zamówienia.

Na pulpicie nawigacyjnym Centrum partnerskiego możesz wykonać tę operację, wybierając wybraną **subskrypcję** w obszarze **subskrypcja** na stronie głównej lub klikając link **do witryny przejdź do wydawcy** obok subskrypcji w celu aktywowania na stronie **subskrypcje** .

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Zakończono zamówienie z produktem, który wymaga aktywacji.

## <a name="c"></a>C\#

Aby uzyskać łącze aktywacji elementu wiersza, Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu wybranego identyfikatora klienta. Następnie Wywołaj Właściwość [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) i metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) z określonym identyfikatorem  [**IDZamówienia**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id). Następnie Wywołaj metodę [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) z **ById ()** z identyfikatorem numeru elementu wiersza.  Na koniec Wywołaj metodę **ActivationLinks ()** .

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{customerId}/Orders/{OrderID}/LineItems/{lineItemNumber}/activationlinks http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [klienta](customer-resources.md#customer) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

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
