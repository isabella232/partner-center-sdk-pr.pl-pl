---
title: Aktualizowanie koszyka
description: Jak zaktualizować zamówienie klienta w koszyku.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 48fec2d9fb72d1a58fe79969e48ccd39a32c5ccc
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557290"
---
# <a name="update-a-cart"></a>Aktualizowanie koszyka

Jak zaktualizować zamówienie klienta w koszyku.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator koszyka dla istniejącego koszyka.

## <a name="c"></a>C\#

Aby zaktualizować zamówienie klienta, pobierz koszyk przy użyciu metody **Get(),** przekazując identyfikatory klienta i koszyka przy użyciu **funkcji ById().** Wprowadzić niezbędne zmiany w koszyku. Teraz wywołaj **metodę Put** przy użyciu identyfikatorów klientów i koszyka przy użyciu **metody ById().**

Na koniec wywołaj **metodę Put()** lub **PutAsync(),** aby utworzyć zamówienie.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

Aby ukończyć zaświadczenia i uwzględnić dodatkowych odsprzedawców, zobacz poniższy przykład.

### <a name="api-sample---check-out-cart"></a>Przykład interfejsu API — wyewidencjij koszyk

``` csharp
{
    "orders": [
        {
            "id": "f76c6b7f449d",
            "alternateId": "f76c6b7f449d",
            "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
                    "subscriptionId": "ebc0beef-7ffb-4044-c074-16f324432139",
                    "termDuration": "P1M",
                    "transactionType": "New",
                    "friendlyName": "AI Builder Capacity add-on",
                    "quantity": 1,
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
                },
                {
                    "lineItemNumber": 1,
                    "offerId": "CFQ7TTC0LFLS:0002:CFQ7TTC0KDLJ",
                    "subscriptionId": "261bac40-7d88-4327-dfa3-dacd09222d62",
                    "termDuration": "P1Y",
                    "transactionType": "New",
                    "friendlyName": "Azure Active Directory Premium P1",
                    "quantity": 2,
                    "partnerIdOnRecord": "517285",
                    "additionalPartnerIdsOnRecord": 
                        "5357564",
                        "5357563"
                    ],
                 
   "links": {
                        "product": {
                            "uri": "/products/CFQ7TTC0LFLS?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "availability": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002/availabilities/CFQ7TTC0KDLJ?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2021-08-18T07:52:23.1921872Z",
            "status": "pending",
            "transactionType": "UserPurchase",
            "links": {
                "self": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "GET",
                    "headers": []
                },
                "provisioningStatus": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "patchOperation": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "PATCH",
                    "headers": []
                }
            },
            "client": {},
            "attributes": {
                "objectType": "Order"
            }
        }
    ],
    "attributes": {
        "objectType": "CartCheckoutResult"
    }
}

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i określić koszyk do zaktualizowania.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.             |
| **identyfikator koszyka**     | ciąg   | Tak      | Identyfikator GUID sformatowany jako cart-id, który identyfikuje koszyk.                     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli [opisano](cart-resources.md) właściwości koszyka w treści żądania.

| Właściwość              | Typ             | Wymagane        | Opis                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Nie              | Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.                                  |
| creationTimeStamp     | DateTime         | Nie              | Data utworzenia koszyka w formacie data/godzina. Stosowane po pomyślnym utworzeniu koszyka.        |
| lastModifiedTimeStamp | DateTime         | Nie              | Data ostatniej aktualizacji koszyka w formacie data/godzina. Stosowane po pomyślnym utworzeniu koszyka.    |
| expirationTimeStamp   | DateTime         | Nie              | Data wygaśnięcia koszyka w formacie data/godzina.  Stosowane po pomyślnym utworzeniu koszyka.            |
| lastModifiedUser      | ciąg           | Nie              | Użytkownik, który ostatnio zaktualizował koszyk. Stosowane po pomyślnym utworzeniu koszyka.                             |
| lineItems             | Tablica obiektów | Tak             | Tablica [zasobów CartLineItem.](cart-resources.md#cartlineitem)                                               |

W tej tabeli [opisano właściwości CartLineItem](cart-resources.md#cartlineitem) w treści żądania.

| Właściwość             | Typ                        | Wymagane     | Opis                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                      | Nie           | Unikatowy identyfikator elementu wiersza koszyka. Stosowane po pomyślnym utworzeniu koszyka.                |
| catalogId            | ciąg                      | Tak          | Identyfikator elementu katalogu.                                                                       |
| Friendlyname         | ciąg                      | Nie           | Opcjonalny. Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.              |
| quantity             | int                         | Tak          | Liczba licencji lub wystąpień.     |
| currencyCode         | ciąg                      | Nie           | Kod waluty.                                                                                 |
| billingCycle         | Obiekt                      | Tak          | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                              |
| uczestnicy         | Lista par ciągów obiektów | Nie           | Kolekcja uczestników zakupu.                                                      |
| provisioningContext  | Słownik<ciąg, ciąg>  | Nie           | Kontekst używany do aprowizowania oferty.                                                          |
| orderGroup           | ciąg                      | Nie           | Grupa wskazująca, które elementy można ze sobą umieścić.                                            |
| error                | Obiekt                      | Nie           | Zastosowane po utworzeniu koszyka w przypadku błędu.                                                 |
| AdditionalPartnerIdsOnRecord | Ciąg | Nie | Gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN tylko dodatkowego odsprzedawcy pośredniego **(nigdy** identyfikatora dostawcy pośredniego). Zachęty nie mają zastosowania do tych dodatkowych odsprzedawców. Można wprowadzić maksymalnie 5 odsprzedawców pośrednich. Dotyczy to tylko partnerów, którzy mogą się do tego dokarmiać w obrębie krajów UNII/EFTA.  |

### <a name="request-example"></a>Przykład żądania

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca wypełniony zasób [koszyka](cart-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
