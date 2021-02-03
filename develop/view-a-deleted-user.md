---
title: Wyświetlanie użytkowników usuniętych dla klienta
description: Pobiera listę usuniętych zasobów CustomerUser dla klienta według identyfikatora klienta. Opcjonalnie można ustawić rozmiar strony. Musisz podać filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768230"
---
# <a name="view-deleted-users-for-a-customer"></a>Wyświetlanie użytkowników usuniętych dla klienta

**Dotyczy**

- Centrum partnerskie

Pobiera listę usuniętych zasobów CustomerUser dla klienta według identyfikatora klienta. Opcjonalnie można ustawić rozmiar strony. Musisz podać filtr.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Co się stanie po usunięciu konta użytkownika?

Po usunięciu konta użytkownika stan użytkownika ma wartość "nieaktywne". Nie jest to możliwe przez 30 dni, po upływie których konto użytkownika i powiązane z nim dane zostaną usunięte i nie można ich odzyskać. Jeśli chcesz przywrócić usunięte konto użytkownika w oknie trzydziestu dni, zobacz [Przywracanie usuniętego użytkownika dla klienta](restore-a-user-for-a-customer.md). Po usunięciu i oznaczeniu wartości "nieaktywne" konto użytkownika nie jest już zwracane jako element członkowski kolekcji użytkowników (na przykład przy użyciu opcji [Pobierz listę wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md)). Aby uzyskać listę usuniętych użytkowników, którzy nie zostali jeszcze przeczyszczeniu, należy wykonać zapytanie o konta użytkowników, które zostały ustawione jako nieaktywne.

## <a name="c"></a>C\#

Aby pobrać listę usuniętych użytkowników, należy utworzyć zapytanie filtrujące dla użytkowników klienta, których stan jest ustawiony jako nieaktywny. Najpierw utwórz filtr, tworząc wystąpienie obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) z parametrami, jak pokazano w poniższym fragmencie kodu. Następnie utwórz zapytanie przy użyciu metody [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) . Jeśli nie chcesz, aby wyniki były stronicowane, zamiast tego możesz użyć metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) . Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Na koniec Wywołaj metodę [**zapytania**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) , aby wysłać żądanie.

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users? size = {size} &Filter = {Filter} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania Użyj następującej ścieżki i parametrów zapytania.

| Nazwa        | Typ   | Wymagane | Opis                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Identyfikator klienta | guid   | Tak      | Wartość jest identyfikatorem GUID sformatowanym przez klienta, który identyfikuje klienta.                                                                                                            |
| size        | int    | Nie       | Liczba wyników do wyświetlenia w tym samym czasie. Ten parametr jest opcjonalny.                                                                                                     |
| filter      | filter | Tak      | Zapytanie filtrujące wyszukiwanie użytkownika. Aby można było pobrać usuniętych użytkowników, należy uwzględnić i zakodować następujący ciąg: {"Field": "UserState", "value": "Inactive", "operator": "Equals"}. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [CustomerUser](user-resources.md#customeruser) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
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
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
