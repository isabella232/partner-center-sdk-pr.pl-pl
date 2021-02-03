---
title: Pobieranie listy wszystkich kont użytkowników dla klienta
description: Jak uzyskać listę wszystkich kont użytkowników należących do jednego z klientów.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f2b1bcf9926e02232b6e2cc68b71e992b015324
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768097"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a>Pobieranie listy wszystkich kont użytkowników dla klienta

**Dotyczy:**

- Centrum partnerskie

W tym artykule opisano, jak uzyskać listę wszystkich kont użytkowników należących do jednego z klientów.

Aby wyszukać jedno konto użytkownika według identyfikatora, zobacz [pobieranie konta użytkownika według identyfikatora](get-a-user-account-by-id.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby pobrać kolekcję wszystkich kont użytkowników dla określonego klienta:

1. Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta, aby zidentyfikować klienta.

2. Wywołaj metodę [**users. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) w celu pobrania kolekcji.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**
- Klasa: **GetCustomerUserCollection.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru identyfikatora URI, aby zidentyfikować odpowiedniego klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję kont użytkowników dla klienta.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
            "usageLocation": "US",
            "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "Daniel Tsai",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
