---
title: Pobieranie linku aktywacji według elementu wiersza zamówienia
description: Pobiera link aktywacji subskrypcji według pozycji zamówienia.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 61cb6659961cfeb22d3b0fe7ad5dd8533d5f72dda76fe96e64b4c64f39ece397
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994153"
---
# <a name="get-activation-link-by-order-line-item"></a>Pobieranie linku aktywacji według elementu wiersza zamówienia

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Pobiera link aktywacji subskrypcji platformy handlowej według numeru wiersza zamówienia.

Na pulpicie nawigacyjnym usługi Partner Center możesz wykonać tę  operację, wybierając pozycję Konkskrypcyjna subskrypcja w obszarze Subskrypcja na stronie głównej lub wybierając link przejdź do witryny usługi **Publisher** obok subskrypcji do aktywowania na **stronie** Subskrypcje. 

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Ukończono zamówienie z produktem, który wymaga aktywacji.

## <a name="c"></a>C\#

Aby uzyskać link aktywacji elementu wiersza, użyj kolekcji [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z wybranym identyfikatorem klienta. Następnie wywołaj [**właściwość Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) i metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) z określonym przez siebie  [**wartością OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id). Następnie wywołaj metodę [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) z **metodą ById()** z identyfikatorem numeru elementu wiersza.  Na koniec wywołaj **metodę ActivationLinks().**

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
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca [kolekcję](customer-resources.md#customer) zasobów klienta w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
