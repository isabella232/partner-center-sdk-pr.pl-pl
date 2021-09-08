---
title: Tworzenie zamówienia klienta
description: Dowiedz się, jak Partner Center api w celu utworzenia zamówienia dla klienta. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 232888ee798b4579246bbfd787e049f9f6e2e8a3
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557256"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Tworzenie zamówienia dla klienta przy użyciu interfejsów API Partner Center API

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud for US Government

Tworzenie zamówienia **dla produktów wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure** ma zastosowanie tylko *do:*

- Centrum partnerskie

Aby uzyskać informacje o tym, co jest obecnie dostępne do sprzedaży, zobacz Oferty partnerów [w Dostawca rozwiązań w chmurze programie](/partner-center/csp-offers).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator oferty.

## <a name="c"></a>C\#

Aby utworzyć zamówienie dla klienta:

1. Za pomocą wystąpienia obiektu [**Order**](order-resources.md) ustaw właściwość **ReferenceCustomerID** na identyfikator klienta, aby zarejestrować klienta.

2. Utwórz listę obiektów [**OrderLineItem**](order-resources.md#orderlineitem) i przypisz listę do właściwości **LineItems** zamówienia. Każdy element wiersza zamówienia zawiera informacje o zakupie dla jednej oferty. Musisz mieć co najmniej jeden element wiersza zamówienia.

3. Uzyskiwanie interfejsu do zamawiania operacji. Najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Następnie pobierz interfejs z właściwości [**Orders.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)

4. Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) i przekaż obiekt [**Order.**](order-resources.md)

5. Aby ukończyć zaświadczenia i uwzględnić dodatkowych odsprzedawców, zobacz następujące przykładowe przykłady żądań i odpowiedzi:

### <a name="request-example"></a>Przykład żądania

``` csharp
{
    "PartnerOnRecordAttestationAccepted":true, 
    "lineItems": [
        {
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "quantity": 1,
            "lineItemNumber": 0,
            "PartnerIdOnRecord": "873452",
            "AdditionalPartnerIdsOnRecord":["4847383","873452"]
        }
    ],
    "billingCycle": "monthly"
}
```

### <a name="response-example"></a>Przykład odpowiedzi

``` csharp
{
    "id": "5cf72f146967",
    "alternateId": "5cf72f146967",
    "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
    "billingCycle": "monthly",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "subscriptionId": "fcddfa52-1da8-4529-d347-50ea51e1e7be",
            "termDuration": "P1M",
            "transactionType": "New",
            "friendlyName": "AI Builder Capacity add-on",
            "quantity": 1,
            "partnerIdOnRecord": "873452",
            "additionalPartnerIdsOnRecord": [
                "4847383",
                "873452"
            ],
            "links": {
                "product": {
                    "uri": "/products/CFQ7TTC0LH0Z?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/CFQ7TTC0LH0Z/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/CFQ7TTC0LH0Z/skus/0001/availabilities/CFQ7TTC0K18P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2021-08-17T18:13:11.3122226Z",
    "status": "pending",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {},
    "attributes": {
        "objectType": "Order"
    }
}

```

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: CreateOrder.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa        | Typ   | Wymagane | Opis                                                |
|-------------|--------|----------|------------------------------------------------------------|
| identyfikator klienta | ciąg | Tak      | Identyfikator klienta sformatowany w formacie GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

#### <a name="order"></a>Zamówienie

W tej tabeli [opisano właściwości Order](order-resources.md) w treści żądania.

| Właściwość             | Typ                        | Wymagane                        | Opis                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| identyfikator                   | ciąg                      | Nie                              | Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia.   |
| referenceCustomerId  | ciąg                      | Nie                              | Identyfikator klienta. |
| billingCycle         | ciąg                      | Nie                              | Wskazuje częstotliwość, z jaką partner jest rozliczany za to zamówienie. Obsługiwane wartości to nazwy członków w [typie BillingCycleType](product-resources.md#billingcycletype). Wartość domyślna to "Monthly" lub "OneTime" podczas tworzenia zamówienia. To pole jest stosowane po pomyślnym utworzeniu zamówienia. |
| lineItems            | tablica [zasobów OrderLineItem](order-resources.md#orderlineitem) | Tak      | Lista ofert, które klient kupuje, wraz z ilością.        |
| currencyCode         | ciąg                      | Nie                              | Tylko do odczytu. Waluta używana podczas składania zamówienia. Stosowane po pomyślnym utworzeniu zamówienia.           |
| Creationdate         | datetime                    | Nie                              | Tylko do odczytu. Data utworzenia zamówienia w formacie data/godzina. Stosowane po pomyślnym utworzeniu zamówienia.                                   |
| status               | ciąg                      | Nie                              | Tylko do odczytu. Stan zamówienia.  Obsługiwane wartości to nazwy członków w [orderstatus](order-resources.md#orderstatus).        |
| Linki                | [OrderLinks](utility-resources.md#resourcelinks)              | Nie                              | Zasób łączy się z zamówieniem. |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Nie                              | Atrybuty metadanych odpowiadające kolejności. |
| PartnerOnRecordAttestationAccepted | Wartość logiczna | Tak | Potwierdza ukończenie zatwierdzeń |


#### <a name="orderlineitem"></a>OrderLineItem

W tej tabeli [opisano właściwości OrderLineItem](order-resources.md#orderlineitem) w treści żądania.

>[!NOTE]
>Rekord partnerIdOnRecord powinien być podany tylko wtedy, gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego. Jest on używany do przechowywania Microsoft Partner Network tylko odsprzedawcy pośredniego (nigdy identyfikatora dostawcy pośredniego).

| Nazwa                 | Typ   | Wymagane | Opis                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Tak      | Każdy element wiersza w kolekcji otrzymuje unikatowy numer wiersza, licząc od 0 do count-1.                                                                                                                                                 |
| offerId              | ciąg | Tak      | Identyfikator oferty.                                                                                                                                                                                                                      |
| subscriptionId       | ciąg | Nie       | Identyfikator subskrypcji.                                                                                                                                                                                                               |
| parentSubscriptionId | ciąg | Nie       | Opcjonalny. Identyfikator subskrypcji nadrzędnej w ofercie dodatku. Dotyczy tylko PATCH.                                                                                                                                                     |
| Friendlyname         | ciąg | Nie       | Opcjonalny. Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu ujednoznacznienia.                                                                                                                                              |
| quantity             | int    | Tak      | Liczba licencji dla subskrypcji opartej na licencjach.                                                                                                                                                                                   |
| partnerIdOnRecord    | ciąg | Nie       | Gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN tylko odsprzedawcy pośredniego **(nigdy** identyfikatorem dostawcy pośredniego). Zapewnia to odpowiednią ewidencjonowanie zachęt. |
| provisioningContext  | Ciąg<, ciąg>                | Nie       |  Informacje wymagane do aprowizowania niektórych elementów w wykazie. Właściwość provisioningVariables w sku wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.                  |
| Linki                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | Nie       |  Tylko do odczytu. Zasób łączy się z elementem wiersza Zamówienia.  |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Nie       | Atrybuty metadanych odpowiadające OrderLineItem. |
| renewsTo             | Tablica obiektów                          | Nie    |Tablica zasobów [RenewsTo.](order-resources.md#renewsto)                                                                            |
| AttestationAccepted             | bool                 | Nie   |  Wskazuje umowę na ofertę lub warunki dotyczące sku. Wymagane tylko w przypadku ofert lub jednostki SKU, gdzie SkuAttestationProperties lub OfferAttestationProperties wymuszaJednacja ma wartość True.          |
| AdditionalPartnerIdsOnRecord | Ciąg | Nie | Gdy dostawca pośredni umieszcza zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN tylko dodatkowego odsprzedawcy pośredniego **(nigdy** nie identyfikatorem dostawcy pośredniego). Zachęty nie mają zastosowania do tych dodatkowych odsprzedawców. Można wprowadzić maksymalnie 5 odsprzedawców pośrednich. Dotyczy to tylko partnerów, którzy mają transakcje w obrębie krajów UNII/UNII EUROPEJSKIEJ. |

##### <a name="renewsto"></a>RenewsTo

W tej tabeli [opisano właściwości RenewsTo](order-resources.md#renewsto) w treści żądania.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | ciąg           | Nie              | Reprezentacja czasu trwania okresu odnowienia w standardach ISO 8601. Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok). |

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

W przypadku powodzenia metoda zwraca [zasób Order](order-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

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
