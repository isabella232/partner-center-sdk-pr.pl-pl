---
title: Wyświetlanie użytkowników usuniętych dla klienta
description: Pobiera listę usuniętych zasobów CustomerUser klienta według identyfikatora klienta. Opcjonalnie możesz ustawić rozmiar strony. Musisz podać filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f7e94d5e360075378e1895e586690597baaf66237f0b93bb526baee0c5d84ae
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989818"
---
# <a name="view-deleted-users-for-a-customer"></a>Wyświetlanie użytkowników usuniętych dla klienta

Pobiera listę usuniętych zasobów CustomerUser klienta według identyfikatora klienta. Opcjonalnie możesz ustawić rozmiar strony. Musisz podać filtr.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Co się stanie po usunięciu konta użytkownika?

Stan użytkownika jest ustawiany na "nieaktywny" podczas usuwania konta użytkownika. Pozostanie w ten sposób przez 30 dni, po upływie których konto użytkownika i skojarzone z nim dane zostaną przeczyszwiązane i nie będzie można ich uzyskać. Jeśli chcesz przywrócić usunięte konto użytkownika w 30-dniowym oknie, zobacz Restore a deleted user for a customer (Przywracanie usuniętego [użytkownika dla klienta).](restore-a-user-for-a-customer.md) Gdy konto użytkownika zostanie usunięte i oznaczone jako "nieaktywne", nie będzie już zwracane jako członek kolekcji użytkowników (na przykład przy użyciu funkcji Pobierz listę wszystkich kont użytkowników [dla klienta).](get-a-list-of-all-user-accounts-for-a-customer.md) Aby uzyskać listę usuniętych użytkowników, którzy nie zostały jeszcze usunięte, należy wykonać zapytanie dotyczące kont użytkowników, dla których ustawiono nieaktywność.

## <a name="c"></a>C\#

Aby pobrać listę usuniętych użytkowników, skonstruuj zapytanie, które filtruje użytkowników klientów, których stan jest ustawiony na nieaktywny. Najpierw utwórz filtr, tworząc wystąpienia obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) z parametrami, jak pokazano w poniższym fragmencie kodu. Następnie utwórz zapytanie przy użyciu [**metody BuildIndexedQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) Jeśli nie chcesz uzyskać stronicowania wyników, możesz zamiast tego użyć metody [**BuildSimpleQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Na koniec wywołaj [**metodę Query,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) aby wysłać żądanie.

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples Class : GetCustomerInactiveUsers.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: GetCustomerInactiveUsers.cs)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/users?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania użyj następującej ścieżki i parametrów zapytania.

| Nazwa        | Typ   | Wymagane | Opis                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator klienta | guid   | Tak      | Wartość to identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.                                                                                                            |
| size        | int    | Nie       | Liczba wyników do wyświetlania jednocześnie. Ten parametr jest opcjonalny.                                                                                                     |
| filter      | filter | Tak      | Zapytanie filtruje wyszukiwanie użytkownika. Aby pobrać usuniętych użytkowników, musisz dołączyć i zakodować następujący ciąg: {"Field":"UserState","Value":"Inactive","Operator":"equals"}. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca kolekcję [zasobów CustomerUser](user-resources.md#customeruser) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

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
