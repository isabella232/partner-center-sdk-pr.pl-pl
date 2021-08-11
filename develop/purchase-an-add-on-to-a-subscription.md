---
title: Zakup dodatku do subskrypcji
description: Jak kupić dodatek do istniejącej subskrypcji.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5227b917faf663c129b1abed1d10318620667e9b47524eb8c91867fb6b453ee8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997366"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Zakup dodatku do subskrypcji

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud for US Government

Jak kupić dodatek do istniejącej subskrypcji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji. Jest to istniejąca subskrypcja, dla której ma być zakupiona oferta dodatku.

- Identyfikator oferty, który identyfikuje ofertę dodatku do zakupu.

## <a name="purchasing-an-add-on-through-code"></a>Kupowanie dodatku za pomocą kodu

Po zakupie dodatku do subskrypcji aktualizujesz oryginalne zamówienie subskrypcji przy użyciu zamówienia na dodatek. Poniżej identyfikator customerId jest identyfikatorem klienta, subscriptionId to identyfikator subskrypcji, a addOnOfferId to identyfikator oferty dla dodatku.

Oto konkretne kroki:

1.  Uzyskaj interfejs do operacji dla subskrypcji.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Użyj tego interfejsu, aby utworzyć wystąpienia obiektu subskrypcji. W ten sposób uzyskujesz szczegóły subskrypcji nadrzędnej, w tym identyfikator zamówienia.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Utworzyć wystąpienia nowego [**obiektu Order.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) To wystąpienie zamówienia służy do aktualizowania oryginalnego zamówienia użytego do zakupu subskrypcji. Dodaj element jedno wierszowy do kolejności, która reprezentuje dodatek.
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  Zaktualizuj oryginalne zamówienie subskrypcji przy użyciu nowego zamówienia dla dodatku.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Aby kupić dodatek, zacznij od uzyskania interfejsu do operacji subskrypcji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, oraz metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) w celu zidentyfikowania subskrypcji, która ma ofertę dodatku. Użyj tego [**interfejsu,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) aby pobrać szczegóły subskrypcji, wywołując wywołanie [**get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Szczegóły subskrypcji zawierają identyfikator zamówienia subskrypcji, czyli zamówienie, które ma zostać zaktualizowane przy użyciu dodatku.

Następnie należy utworzyć wystąpienie nowego obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) i wypełnić go pojedynczym wystąpieniem [**LineItem,**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) które zawiera informacje identyfikujące dodatek, jak pokazano w poniższym fragmencie kodu. Użyjesz tego nowego obiektu, aby zaktualizować zamówienie subskrypcji przy użyciu dodatku. Na koniec wywołaj metodę [**Patch,**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) aby zaktualizować zamówienie subskrypcji, po pierwszym zidentyfikowaniu klienta za pomocą metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) i z zamówieniem [**orders.ById.**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: AddSubscriptionAddOn.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów, aby zidentyfikować klienta i zamówienie.

| Nazwa                   | Typ     | Wymagane | Opis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość to identyfikator GUID sformatowany **jako customer-tenant-id,** który identyfikuje klienta. |
| **order-id**           | **guid** | Y        | Identyfikator zamówienia.                                                              |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W poniższych tabelach opisano właściwości w treści żądania.

## <a name="order"></a>Zamówienie

| Nazwa                | Typ             | Wymagane | Opis                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | ciąg           | N        | Identyfikator zamówienia.                                        |
| ReferenceCustomerId | ciąg           | Y        | Identyfikator klienta.                                     |
| LineItems           | tablica obiektów | Y        | Tablica obiektów [OrderLineItem.](#orderlineitem) |
| Creationdate        | ciąg           | N        | Data utworzenia zamówienia w formacie data/godzina. |
| Atrybuty          | object           | N        | Zawiera "ObjectType": "Order".                      |

## <a name="orderlineitem"></a>OrderLineItem

| Nazwa                 | Typ   | Wymagane | Opis                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | liczba | Y        | Numer elementu wiersza, zaczynając od 0.                       |
| OfferId              | ciąg | Y        | Identyfikator oferty dodatku.                                  |
| SubscriptionId       | ciąg | N        | Identyfikator zakupionej subskrypcji dodatku.                 |
| ParentSubscriptionId | ciąg | Y        | Identyfikator subskrypcji nadrzędnej, która ma ofertę dodatku. |
| FriendlyName         | ciąg | N        | Przyjazna nazwa dla tego elementu wiersza.                        |
| Liczba             | liczba | Y        | Liczba licencji.                                      |
| PartnerIdOnRecord    | ciąg | N        | Identyfikator MPN partnera rekordu.                         |
| Atrybuty           | object | N        | Zawiera "ObjectType": "OrderLineItem".                      |

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca zaktualizowaną kolejność subskrypcji w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
