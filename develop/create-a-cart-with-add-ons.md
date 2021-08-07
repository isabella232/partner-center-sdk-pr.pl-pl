---
title: Tworzenie koszyka z dodatkami
description: Dowiedz się, jak używać Partner Center API do dodawania zamówienia klienta z dodatkimi za pośrednictwem koszyka. Artykuł udostępnia wymagania wstępne i kroki tworzenia koszyka z dodatków.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: ed4b8be5171493f83aefef08253c748a7bfd90dc5f2b1e325e5ceba78e36bdc2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991807"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Tworzenie koszyka z dodatkimi do zamówienia klienta

Dodatki można kupić za pośrednictwem koszyka. Aby uzyskać więcej informacji o tym, co jest obecnie dostępne do sprzedaży, zobacz [Oferty partnerów w Dostawca rozwiązań w chmurze sprzedaży.](/partner-center/csp-offers)

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Koszyk umożliwia zakup oferty podstawowej i odpowiadających jej dodatków. Wykonaj następujące kroki, aby utworzyć koszyk:

1. Utworzyć wystąpienia obiektu [**koszyka.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)

2. Utwórz listę obiektów [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) reprezentujących oferty podstawowe i przypisz listę do właściwości [**LineItems koszyka.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)

3. W obszarze każdego elementu koszyka oferty podstawowej wypełnij listę elementów **AddOnItems** innymi obiektami **CartLineItem,** z których każdy reprezentuje dodatek, który zostanie zakupiony względem tej oferty podstawowej.

4. Uzyskaj interfejs do obsługi operacji koszyka przy użyciu narzędzia [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) w celu wywołania metody [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, a następnie pobierania interfejsu z właściwości **Cart.**

5. Na koniec wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) aby utworzyć koszyk.

### <a name="c-example"></a>Przykład w \# języku C

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

Wykonaj następujące kroki, aby utworzyć koszyk, który umożliwi zakup dodatków dla istniejących subskrypcji podstawowych:

1. Utwórz koszyk **z** nowym elementem **CartLineItem** zawierającym identyfikator subskrypcji we właściwości **ProvisioningContext z** kluczem "ParentSubscriptionId".

2. Wywołaj **metodę Create** lub **CreateAsync.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.             |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli [opisano](cart-resources.md) właściwości koszyka w treści żądania.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Nie              | Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.                                  |
| creationTimeStamp     | DateTime         | Nie              | Data utworzenia koszyka w formacie data/godzina. Stosowane po pomyślnym utworzeniu koszyka.         |
| lastModifiedTimeStamp | DateTime         | Nie              | Data ostatniej aktualizacji koszyka w formacie data/godzina. Stosowane po pomyślnym utworzeniu koszyka.    |
| expirationTimeStamp   | DateTime         | Nie              | Data wygaśnięcia koszyka w formacie data/godzina.  Stosowane po pomyślnym utworzeniu koszyka.            |
| lastModifiedUser      | ciąg           | Nie              | Użytkownik, który ostatnio zaktualizował koszyk. Stosowane po pomyślnym utworzeniu koszyka.                             |
| lineItems             | Tablica obiektów | Tak             | Tablica [zasobów CartLineItem.](cart-resources.md#cartlineitem)                                             |

W tej tabeli [opisano właściwości CartLineItem](cart-resources.md#cartlineitem) w treści żądania.

| Właściwość             | Typ                             | Opis                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                           | Unikatowy identyfikator elementu wiersza koszyka. Stosowane po pomyślnym utworzeniu koszyka.                                                                   |
| catalogId            | ciąg                           | Identyfikator elementu katalogu.                                                                                                                          |
| Friendlyname         | ciąg                           | Opcjonalny. Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.                                                                 |
| quantity             | int                              | Liczba licencji lub wystąpień.                                                                                                                  |
| currencyCode         | ciąg                           | Kod waluty.                                                                                                                                    |
| billingCycle         | Obiekt                           | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                                                                 |
| uczestnicy         | Lista par ciągów obiektów      | Kolekcja identyfikatorów PartnerId w rekordzie (identyfikator MPN) podczas zakupu.                                                                                          |
| provisioningContext  | Słownik<ciąg, ciąg>       | Kontekst używany do aprowizowania oferty.                                                                                                             |
| orderGroup           | ciąg                           | Grupa wskazująca, które elementy można ze sobą umieścić.                                                                                               |
| addonItems           | Lista obiektów **CartLineItem** | Kolekcja elementów wiersza koszyka dla dodatków, które zostaną zakupione w ramach subskrypcji podstawowej, która wynika z zakupu elementu wiersza koszyka nadrzędnego. |
| error                | Obiekt                           | Zastosowane po utworzeniu koszyka, jeśli wystąpi błąd.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Przykład żądania (nowa subskrypcja podstawowa)

W poniższym przykładzie rest pokazano, jak utworzyć koszyk z elementami dodatków dla nowej subskrypcji podstawowej.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>Przykład żądania (istniejąca subskrypcja podstawowa)

W poniższym przykładzie rest pokazano, jak dołączać dodatki do istniejącej subskrypcji podstawowej.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca wypełniony zasób [koszyka](cart-resources.md) w treści odpowiedzi.

#### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

#### <a name="response-example-new-base-subscription"></a>Przykład odpowiedzi (nowa subskrypcja podstawowa)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>Przykład odpowiedzi (istniejąca subskrypcja podstawowa)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
