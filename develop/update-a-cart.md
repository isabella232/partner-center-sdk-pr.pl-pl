---
title: Aktualizowanie koszyka
description: Jak zaktualizować zamówienie dla klienta w koszyku.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767834"
---
# <a name="update-a-cart"></a>Aktualizowanie koszyka

**Dotyczy**

- Centrum partnerskie

Jak zaktualizować zamówienie dla klienta w koszyku.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator koszyka dla istniejącego koszyka.

## <a name="c"></a>C\#

Aby zaktualizować zamówienie dla klienta, należy uzyskać koszyk przy użyciu metody **Get ()** przez przekazanie identyfikatora klienta i koszyka przy użyciu funkcji **ById ()** . Wprowadź niezbędne zmiany w koszyku. Teraz Wywołaj metodę **Put** przy użyciu identyfikatora klienta i koszyka przy użyciu metody **ById ()** .

Na koniec Wywołaj metodę **Put ()** lub **PutAsync ()** , aby utworzyć zamówienie.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Carts/{Cart-ID} http/1.1              |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i określić koszyk do zaktualizowania.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **Identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.             |
| **Identyfikator koszyka**     | ciąg   | Tak      | Identyfikator koszyka w formacie GUID, który identyfikuje koszyk.                     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano właściwości [koszyka](cart-resources.md) w treści żądania.

| Właściwość              | Typ             | Wymagane        | Opis                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Nie              | Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.                                  |
| creationTimeStamp     | DateTime         | Nie              | Data i godzina utworzenia koszyka. Stosowane po pomyślnym utworzeniu koszyka.        |
| lastModifiedTimeStamp | DateTime         | Nie              | Data ostatniej aktualizacji koszyka w formacie daty i godziny. Stosowane po pomyślnym utworzeniu koszyka.    |
| expirationTimeStamp   | DateTime         | Nie              | Data wygaśnięcia koszyka w formacie daty i godziny.  Stosowane po pomyślnym utworzeniu koszyka.            |
| lastModifiedUser      | ciąg           | Nie              | Użytkownik, który ostatnio zaktualizował koszyk. Stosowane po pomyślnym utworzeniu koszyka.                             |
| lineItems             | Tablica obiektów | Tak             | Tablica zasobów [CartLineItem](cart-resources.md#cartlineitem) .                                               |

W tej tabeli opisano właściwości [CartLineItem](cart-resources.md#cartlineitem) w treści żądania.

| Właściwość             | Typ                        | Wymagane     | Opis                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                      | Nie           | Unikatowy identyfikator dla elementu w wierszu koszyka. Stosowane po pomyślnym utworzeniu koszyka.                |
| catalogId            | ciąg                      | Tak          | Identyfikator elementu katalogu.                                                                       |
| friendlyName         | ciąg                      | Nie           | Opcjonalny. Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.              |
| quantity             | int                         | Tak          | Liczba licencji lub wystąpień.     |
| currencyCode         | ciąg                      | Nie           | Kod waluty.                                                                                 |
| billingCycle         | Obiekt                      | Tak          | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                              |
| uczestnicy         | Lista par ciągów obiektów | Nie           | Kolekcja uczestników zakupu.                                                      |
| provisioningContext  | Ciąg<słownika, ciąg>  | Nie           | Kontekst używany do aprowizacji oferty.                                                          |
| kolejność           | ciąg                      | Nie           | Grupa wskazująca, które elementy mogą być umieszczone razem.                                            |
| error                | Obiekt                      | Nie           | Zastosowano po utworzeniu koszyka w przypadku błędu.                                                 |

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

Jeśli to się powiedzie, ta metoda zwraca zasób [koszyka](cart-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

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
