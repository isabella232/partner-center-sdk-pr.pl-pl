---
title: Przywracanie usuniętego użytkownika dla klienta
description: Jak przywrócić usuniętego użytkownika według identyfikatora klienta i identyfikatora użytkownika.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04cca2f7c99023ef277f0f265a755be3e4692fa5e786ce37939b6aebd32a3ba3
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996907"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Przywracanie usuniętego użytkownika dla klienta

Jak przywrócić usuniętego **użytkownika według** identyfikatora klienta i identyfikatora użytkownika.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika. Jeśli nie masz identyfikatora użytkownika, zobacz [Wyświetlanie usuniętych użytkowników dla klienta](view-a-deleted-user.md).

## <a name="when-can-you-restore-a-deleted-user-account"></a>Kiedy można przywrócić usunięte konto użytkownika?

Stan użytkownika jest ustawiany na "nieaktywny" podczas usuwania konta użytkownika. Pozostanie w ten sposób przez 30 dni, po upływie których konto użytkownika i skojarzone z nim dane zostaną przeczyszwiązane i nie będzie można ich uzyskać. Usunięte konto użytkownika można przywrócić tylko w tym 30-dniowym oknie. Gdy konto użytkownika zostanie usunięte i oznaczone jako "nieaktywne", nie będzie już zwracane jako członek kolekcji użytkowników (na przykład przy użyciu funkcji Pobierz listę wszystkich kont użytkowników [dla klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Aby przywrócić użytkownika, utwórz nowe wystąpienie klasy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) i ustaw wartość właściwości [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**UserState.Active.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)

Usuniętego użytkownika można przywrócić, ustawiając jego stan na aktywny. Nie trzeba ponownieopulacji pozostałych pól w zasobie użytkownika. Te wartości zostaną automatycznie przywrócone z usuniętego, nieaktywnego zasobu użytkownika. Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, a metody [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) w celu zidentyfikowania użytkownika.

Na koniec wywołaj [**metodę Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) i przekaż wystąpienie **CustomerUser,** aby wysłać żądanie przywrócenia użytkownika.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples Class : CustomerUserRestore.cs **(Klasa przykładów** kodu : CustomerUserRestore.cs)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/users/{user-id} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby określić identyfikator klienta i identyfikator użytkownika.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników do danego klienta. |
| **identyfikator użytkownika**            | **guid** | Y        | Wartość to identyfikator GUID sformatowany **jako identyfikator użytkownika** należący do jednego konta użytkownika.                                         |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa       | Typ   | Wymagane | Opis                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Stan      | ciąg | Y        | Stan użytkownika. Aby przywrócić usuniętego użytkownika, ten ciąg musi zawierać ciąg "aktywny". |
| Atrybuty | object | N        | Zawiera "ObjectType": "CustomerUser".                                 |

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zwróci przywrócone informacje o użytkowniku w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz Partner Center REST Error Codes (Kody [błędów REST).](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```
