---
title: Tworzenie zamówienia klienta dla odsprzedawcy pośredniego
description: Dowiedz się, jak Partner Center api do tworzenia zamówienia dla klienta odsprzedawcy pośredniego. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba46b151e423df27f1378ac8441a23702e47746911b4e05e370bbf0aa7b53233
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991552"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Utwórz zamówienie dla klienta odsprzedawcy pośredniego

Jak utworzyć zamówienie dla klienta odsprzedawcy pośredniego.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator oferty przedmiotu do zakupu.

- Identyfikator dzierżawy odsprzedawcy pośredniego.

## <a name="c"></a>C\#

Aby utworzyć zamówienie dla klienta odsprzedawcy pośredniego:

1. Pobierz kolekcję odsprzedawców pośrednich, którzy mają relację z zalogowanym partnerem.

2. Pobierz zmienną lokalną do elementu w kolekcji, który odpowiada identyfikatorowi odsprzedawcy pośredniego. Ten krok pomaga uzyskać dostęp do właściwości [**MpnId odsprzedawcy**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) podczas tworzenia zamówienia.

3. Za pomocą wystąpienia obiektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) ustaw właściwość [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identyfikator klienta, aby zarejestrować klienta.

4. Utwórz listę obiektów [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) i przypisz listę do właściwości [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) zamówienia. Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty. Pamiętaj, aby w każdym wierszu wypełnić właściwość [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) identyfikatorem MPN odsprzedawcy pośredniego. Musisz mieć co najmniej jeden wiersz zamówienia.

5. Uzyskaj interfejs do obsługi zamówień operacji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, a następnie pobierz interfejs z [**właściwości Orders.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)

6. Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) aby utworzyć zamówienie.

### <a name="c-example"></a>Przykład w \# języku C

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

**Przykład:** [Aplikacja testowa konsoli](console-test-app.md)**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa        | Typ   | Wymagane | Opis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| identyfikator klienta | ciąg | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

#### <a name="order"></a>Zamówienie

W tej tabeli **opisano właściwości** Order w treści żądania.

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| identyfikator | ciąg | Nie | Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia. |
| referenceCustomerId | ciąg | Tak | Identyfikator klienta. |
| billingCycle | ciąg | Nie | Częstotliwość, za pomocą której partner jest rozliczany za to zamówienie. Wartość domyślna &quot; to Co miesiąc i jest stosowana po &quot; pomyślnym utworzeniu zamówienia. Obsługiwane wartości to nazwy członków w [**typie BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). Uwaga: funkcja rozliczeń rocznych nie jest jeszcze ogólnie dostępna. Obsługa rozliczeń rocznych będzie wkrótce wycześniejsza. |
| lineItems | tablica obiektów | Tak | Tablica zasobów [**OrderLineItem.**](#orderlineitem) |
| Creationdate | ciąg | Nie | Data utworzenia zamówienia w formacie data/godzina. Stosowane po pomyślnym utworzeniu zamówienia. |
| atrybuty | object | Nie | Zawiera "ObjectType": "Order". |

#### <a name="orderlineitem"></a>OrderLineItem

W tej tabeli **opisano właściwości OrderLineItem** w treści żądania.

| Nazwa | Typ | Wymagane | Opis |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Tak | Każdy element wiersza w kolekcji otrzymuje unikatowy numer wiersza, licząc od 0 do count-1. |
| offerId | ciąg | Tak | Identyfikator oferty. |
| subscriptionId | ciąg | Nie | Identyfikator subskrypcji. |
| parentSubscriptionId | ciąg | Nie | Opcjonalny. Identyfikator subskrypcji nadrzędnej w ofercie dodatku. Dotyczy tylko PATCH. |
| Friendlyname | ciąg | Nie | Opcjonalny. Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu ujednoznacznienia. |
| quantity | int | Tak | Liczba licencji dla subskrypcji opartej na licencjach. |
| partnerIdOnRecord | ciąg | Nie | Gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN tylko odsprzedawcy pośredniego **(nigdy** identyfikatorem dostawcy pośredniego). Zapewnia to odpowiednią ewidencjonowanie zachęt. **Nie podaniem identyfikatora MPN odsprzedawcy nie powoduje niepowodzenia zamówienia. Jednak odsprzedawca nie jest rejestrowany i w związku z tym obliczenia zachęt mogą nie obejmować sprzedaży.** |
| atrybuty | object | Nie | Zawiera "ObjectType":"OrderLineItem". |

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

Jeśli to się powiedzie, treść odpowiedzi zawiera wypełniony [zasób Order.](order-resources.md)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

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
