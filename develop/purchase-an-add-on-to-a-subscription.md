---
title: Zakup dodatku do subskrypcji
description: Jak kupić dodatek do istniejącej subskrypcji.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768313"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Zakup dodatku do subskrypcji

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie Microsoft Cloud for US Government

Jak kupić dodatek do istniejącej subskrypcji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji. Jest to istniejąca subskrypcja, dla której ma zostać nabyta oferta dodatku.

- Identyfikator oferty identyfikujący ofertę dodatku do zakupu.

## <a name="purchasing-an-add-on-through-code"></a>Kupowanie dodatku poprzez kod

W przypadku zakupu dodatku do subskrypcji aktualizowana jest oryginalna kolejność subskrypcji z kolejnością dla dodatku. W poniższym przypadku IDKlienta jest IDENTYFIKATORem klienta, Identyfikator subskrypcji oznacza subskrypcję, a addOnOfferId to identyfikator oferty dla dodatku.

Oto konkretne kroki:

1.  Pobierz interfejs do operacji dla subskrypcji.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Użyj tego interfejsu, aby utworzyć wystąpienie obiektu subskrypcji. Spowoduje to pobranie szczegółów subskrypcji nadrzędnej, w tym identyfikatora zamówienia.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Tworzenie wystąpienia nowego obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) . To wystąpienie zamówienia służy do aktualizowania oryginalnego zamówienia używanego do zakupu subskrypcji. Dodaj pojedynczy wiersz elementu do kolejności, która reprezentuje dodatek.
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

4.  Zaktualizuj oryginalne zamówienie dla subskrypcji za pomocą nowej kolejności dla dodatku.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Aby kupić dodatek, Zacznij od uzyskania interfejsu do operacji subskrypcji przez wywołanie metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować subskrypcję z ofertą dodatku. Użyj tego [**interfejsu**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) , aby pobrać szczegóły subskrypcji przez wywołanie metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Dlaczego są potrzebne szczegóły subskrypcji? Ponieważ potrzebujesz identyfikatora zamówienia w kolejności subskrypcji. Jest to zamówienie, które ma zostać zaktualizowane przy użyciu dodatku.

Następnie Utwórz wystąpienie nowego obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) i wypełnij je pojedynczym wystąpieniem [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) zawierającym informacje umożliwiające zidentyfikowanie dodatku, jak pokazano w poniższym fragmencie kodu. Ten nowy obiekt zostanie użyty do zaktualizowania zamówienia subskrypcji z dodatkiem. Na koniec Wywołaj metodę [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) , aby zaktualizować kolejność subskrypcji, po pierwszym zidentyfikowaniu klienta z [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) i Order with [**Orders. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

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

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: AddSubscriptionAddOn.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Aby zidentyfikować klienta i zamówienie, użyj następujących parametrów.

| Nazwa                   | Typ     | Wymagane | Opis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , który identyfikuje klienta. |
| **Identyfikator zamówienia**           | **guid** | Y        | Identyfikator zamówienia.                                                              |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W poniższych tabelach opisano właściwości w treści żądania.

## <a name="order"></a>Zamówienie

| Nazwa                | Typ             | Wymagane | Opis                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | ciąg           | N        | Identyfikator zamówienia.                                        |
| ReferenceCustomerId | ciąg           | Y        | Identyfikator klienta.                                     |
| LineItems           | Tablica obiektów | Y        | Tablica obiektów [OrderLineItem](#orderlineitem) . |
| CreationDate        | ciąg           | N        | Data, w której zamówienie zostało utworzone, w formacie daty i godziny. |
| Atrybuty          | object           | N        | Zawiera "ObjectType": "Order".                      |

## <a name="orderlineitem"></a>OrderLineItem

| Nazwa                 | Typ   | Wymagane | Opis                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | liczba | Y        | Numer elementu wiersza, zaczynając od 0.                       |
| OfferId              | ciąg | Y        | Identyfikator oferty dodatku.                                  |
| SubscriptionId       | ciąg | N        | Identyfikator zakupionej subskrypcji dodatku.                 |
| ParentSubscriptionId | ciąg | Y        | Identyfikator subskrypcji nadrzędnej z ofertą dodatku. |
| FriendlyName         | ciąg | N        | Przyjazna nazwa dla tego elementu wiersza.                        |
| Ilość             | liczba | Y        | Liczba licencji.                                      |
| PartnerIdOnRecord    | ciąg | N        | IDENTYFIKATOR MPN partnera rekordu.                         |
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

Jeśli to się powiedzie, ta metoda zwraca zaktualizowany porządek subskrypcji w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

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
