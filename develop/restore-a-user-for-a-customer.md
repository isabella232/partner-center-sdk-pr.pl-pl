---
title: Przywracanie usuniętego użytkownika dla klienta
description: Jak przywrócić usuniętego użytkownika według identyfikatora klienta i identyfikatora użytkownika.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768406"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Przywracanie usuniętego użytkownika dla klienta

**Dotyczy**

- Centrum partnerskie

Jak przywrócić usuniętego **użytkownika** według identyfikatora klienta i identyfikatora użytkownika.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika. Jeśli nie masz identyfikatora użytkownika, zobacz [Wyświetlanie usuniętych użytkowników dla klienta](view-a-deleted-user.md).

## <a name="when-can-you-restore-a-deleted-user-account"></a>Kiedy można przywrócić usunięte konto użytkownika?

Po usunięciu konta użytkownika stan użytkownika ma wartość "nieaktywne". Nie jest to możliwe przez 30 dni, po upływie których konto użytkownika i powiązane z nim dane zostaną usunięte i nie można ich odzyskać. Usunięte konto użytkownika można przywrócić tylko w tym trzydzieści-dniowym oknie. Po usunięciu i oznaczeniu elementu "nieaktywne" konto użytkownika nie jest już zwracane jako członek kolekcji użytkowników (na przykład przy użyciu polecenia [Pobierz listę wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Aby przywrócić użytkownika, Utwórz nowe wystąpienie klasy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) i ustaw wartość właściwości [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).

Użytkownik zostanie przywrócony przez ustawienie stanu użytkownika jako aktywny. Nie trzeba ponownie wypełniać pozostałych pól w zasobie użytkownika. Te wartości zostaną automatycznie przywrócone z usuniętego zasobu nieaktywnego użytkownika. Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę user [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować użytkownika.

Na koniec Wywołaj metodę [**patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) i przekaż wystąpienie **CustomerUser** w celu wysłania żądania przywrócenia użytkownika.

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

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CustomerUserRestore.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby określić identyfikator klienta i identyfikator użytkownika.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników do danego klienta. |
| **Identyfikator użytkownika**            | **guid** | Y        | Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.                                         |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa       | Typ   | Wymagane | Opis                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Stan      | ciąg | Y        | Stan użytkownika. Aby przywrócić usuniętego użytkownika, ten ciąg musi zawierać wartość "Active". |
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

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
