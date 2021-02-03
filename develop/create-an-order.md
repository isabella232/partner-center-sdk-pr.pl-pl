---
title: Utwórz zamówienie klienta
description: Dowiedz się, jak utworzyć zamówienie dla klienta przy użyciu interfejsów API usługi Partner Center. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768625"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Tworzenie zamówienia dla klienta przy użyciu interfejsów API Centrum partnerskiego

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie Microsoft Cloud for US Government

Tworzenie **zamówienia na produkty wystąpień zarezerwowanych maszyn wirtualnych platformy Azure** ma zastosowanie *tylko* do:

- Centrum partnerskie

Aby uzyskać informacje o tym, co jest obecnie dostępne do sprzedawania, zobacz [oferty partnerów w programie Cloud Solution Provider](/partner-center/csp-offers).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator oferty.

## <a name="c"></a>C\#

Aby utworzyć zamówienie dla klienta:

1. Utwórz wystąpienie obiektu [**Order**](order-resources.md) i ustaw właściwość **ReferenceCustomerID** na identyfikator klienta, aby zarejestrować klienta.

2. Utwórz listę obiektów [**OrderLineItem**](order-resources.md#orderlineitem) i przypisz listę do właściwości **LineItems** zamówienia. Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty. Musisz mieć co najmniej jeden element wiersza zamówienia.

3. Uzyskaj interfejs do porządkowania operacji. Najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Następnie Pobierz interfejs z właściwości [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

4. Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) i przekaż obiekt [**Order**](order-resources.md) .

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateOrder.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa        | Typ   | Wymagane | Opis                                                |
|-------------|--------|----------|------------------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

#### <a name="order"></a>Zamówienie

W tej tabeli opisano właściwości [zamówienia](order-resources.md) w treści żądania.

| Właściwość             | Typ                        | Wymagane                        | Opis                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| identyfikator                   | ciąg                      | Nie                              | Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia.   |
| referenceCustomerId  | ciąg                      | Nie                              | Identyfikator klienta. |
| billingCycle         | ciąg                      | Nie                              | Wskazuje częstotliwość, z jaką jest rozliczany partner dla tego zamówienia. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](product-resources.md#billingcycletype). Wartość domyślna to "Monthly" lub "jednorazowej" podczas tworzenia kolejności. To pole jest stosowane po pomyślnym utworzeniu zamówienia. |
| lineItems            | Tablica zasobów [OrderLineItem](order-resources.md#orderlineitem) | Tak      | Lista elementów oferty, do których klient kupuje, wraz z ilością.        |
| currencyCode         | ciąg                      | Nie                              | Tylko do odczytu. Waluta użyta podczas umieszczania zamówienia. Stosowane po pomyślnym utworzeniu zamówienia.           |
| creationDate         | datetime                    | Nie                              | Tylko do odczytu. Data, w której zamówienie zostało utworzone, w formacie daty i godziny. Stosowane po pomyślnym utworzeniu zamówienia.                                   |
| status               | ciąg                      | Nie                              | Tylko do odczytu. Stan zamówienia.  Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [OrderStatus](order-resources.md#orderstatus).        |
| linki                | [OrderLinks](utility-resources.md#resourcelinks)              | Nie                              | Linki do zasobów odpowiadające kolejności. |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Nie                              | Atrybuty metadanych odpowiadające kolejności. |

#### <a name="orderlineitem"></a>OrderLineItem

W tej tabeli opisano właściwości [OrderLineItem](order-resources.md#orderlineitem) w treści żądania.

>[!NOTE]
>PartnerIdOnRecord należy podać tylko wtedy, gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy. Jest on używany do przechowywania tylko identyfikatora Microsoft Partner Network pośredniego Odsprzedawcy (nigdy nie jest to identyfikator dostawcy pośredniego).

| Nazwa                 | Typ   | Wymagane | Opis                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Tak      | Każdy element wiersza w kolekcji pobiera unikatowy numer wiersza, licząc do wartości z przedziału od 0 do count-1.                                                                                                                                                 |
| offerId              | ciąg | Tak      | Identyfikator oferty.                                                                                                                                                                                                                      |
| subscriptionId       | ciąg | Nie       | Identyfikator subskrypcji.                                                                                                                                                                                                               |
| parentSubscriptionId | ciąg | Nie       | Opcjonalny. Identyfikator subskrypcji nadrzędnej w ofercie dodatku. Dotyczy tylko poprawki.                                                                                                                                                     |
| friendlyName         | ciąg | Nie       | Opcjonalny. Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, która pomaga w odróżnieniu od siebie.                                                                                                                                              |
| quantity             | int    | Tak      | Liczba licencji dla subskrypcji opartej na licencji.                                                                                                                                                                                   |
| partnerIdOnRecord    | ciąg | Nie       | Gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy, Wypełnij to pole IDENTYFIKATORem MPN **pośredniego odsprzedawcy** (nigdy nie jest identyfikatorem dostawcy pośredniego). Zapewnia to odpowiednie Księgowanie zachęt. |
| provisioningContext  | Ciąg<słownika, ciąg>                | Nie       |  Informacje wymagane do aprowizacji dla niektórych elementów w wykazie. Właściwość provisioningVariables w jednostce SKU wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.                  |
| linki                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | Nie       |  Tylko do odczytu. Linki do zasobów odpowiadające elementowi wiersza zamówienia.  |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Nie       | Atrybuty metadanych odpowiadające OrderLineItem. |
| renewsTo             | Tablica obiektów                          | Nie    |Tablica zasobów [RenewsTo](order-resources.md#renewsto) .                                                                            |

##### <a name="renewsto"></a>RenewsTo

W tej tabeli opisano właściwości [RenewsTo](order-resources.md#renewsto) w treści żądania.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | ciąg           | Nie              | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok). |

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca zasób [zamówienia](order-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
