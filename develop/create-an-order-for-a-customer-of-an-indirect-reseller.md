---
title: Utwórz zamówienie klienta na potrzeby pośredniego odsprzedawcy
description: Dowiedz się, jak za pomocą interfejsów API usługi Partner Center utworzyć zamówienie dla klienta pośredniego odsprzedawcy. Artykuł zawiera wymagania wstępne, kroki i Exmaples.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770155"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Utwórz zamówienie dla klienta odsprzedawcy pośredniego

**Dotyczy:**

- Centrum partnerskie

Jak utworzyć zamówienie dla klienta pośredniego odsprzedawcy.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator oferty elementu do zakupu.

- Identyfikator dzierżawy pośredniego odsprzedawcy.

## <a name="c"></a>C\#

Aby utworzyć zamówienie dla klienta pośredniego odsprzedawcy:

1. Pobierz kolekcję pośrednich odsprzedawcaów, które mają relację z zalogowanym partnerem.

2. Pobierz zmienną lokalną do elementu w kolekcji, który jest zgodny z IDENTYFIKATORem pośredniego odsprzedawcy. Ten krok pozwala uzyskać dostęp do właściwości [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) odsprzedawcy podczas tworzenia zamówienia.

3. Utwórz wystąpienie obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) i ustaw właściwość [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identyfikator klienta, aby zarejestrować klienta.

4. Utwórz listę obiektów [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) i przypisz listę do właściwości [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) zamówienia. Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty. Upewnij się, że właściwość [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) w każdym wierszu jest WYpełniona IDENTYFIKATORem MPN pośredniego odsprzedawcy. Musisz mieć co najmniej jeden element wiersza zamówienia.

5. Uzyskaj interfejs do porządkowania operacji, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta, a następnie pobrać interfejs z właściwości [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

6. Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) , aby utworzyć zamówienie.

### <a name="c-example"></a>\#Przykład C

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa        | Typ   | Wymagane | Opis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

#### <a name="order"></a>Zamówienie

W tej tabeli opisano właściwości **zamówienia** w treści żądania.

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| identyfikator | ciąg | Nie | Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia. |
| referenceCustomerId | ciąg | Tak | Identyfikator klienta. |
| billingCycle | ciąg | Nie | Częstotliwość, z jaką jest rozliczany partner dla tego zamówienia. Wartość domyślna to &quot; miesiąc &quot; i jest stosowana po pomyślnym utworzeniu zamówienia. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). Uwaga: funkcja rocznego rozliczania nie jest jeszcze ogólnie dostępna. Pomoc techniczna dotycząca rozliczeń rocznych jest dostępna wkrótce. |
| lineItems | Tablica obiektów | Tak | Tablica zasobów [**OrderLineItem**](#orderlineitem) . |
| creationDate | ciąg | Nie | Data, w której zamówienie zostało utworzone, w formacie daty i godziny. Stosowane po pomyślnym utworzeniu zamówienia. |
| atrybuty | object | Nie | Zawiera "ObjectType": "Order". |

#### <a name="orderlineitem"></a>OrderLineItem

W tej tabeli opisano właściwości **OrderLineItem** w treści żądania.

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Tak | Każdy element wiersza w kolekcji pobiera unikatowy numer wiersza, licząc do wartości z przedziału od 0 do count-1. |
| offerId | ciąg | Tak | Identyfikator oferty. |
| subscriptionId | ciąg | Nie | Identyfikator subskrypcji. |
| parentSubscriptionId | ciąg | Nie | Opcjonalny. Identyfikator subskrypcji nadrzędnej w ofercie dodatku. Dotyczy tylko poprawki. |
| friendlyName | ciąg | Nie | Opcjonalny. Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, która pomaga w odróżnieniu od siebie. |
| quantity | int | Tak | Liczba licencji dla subskrypcji opartej na licencji. |
| partnerIdOnRecord | ciąg | Nie | Gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy, Wypełnij to pole IDENTYFIKATORem MPN **pośredniego odsprzedawcy** (nigdy nie jest identyfikatorem dostawcy pośredniego). Zapewnia to odpowiednie Księgowanie zachęt. **Niedostarczenie identyfikatora MPN odsprzedawcy nie powoduje błędu zamówienia. Jednak odsprzedawca nie jest zarejestrowany i w związku z tym, że obliczenia bodźce mogą nie uwzględniać sprzedaży.** |
| atrybuty | object | Nie | Zawiera "ObjectType": "OrderLineItem". |

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

Jeśli to się powiedzie, treść odpowiedzi zawiera zapełnione [zamówione](order-resources.md) zasoby.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
