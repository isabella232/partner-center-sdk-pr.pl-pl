---
title: Usuwanie konta użytkownika dla klienta
description: Jak usunąć istniejące konto użytkownika dla klienta.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 64e9175a2a4545022175b326a2d765ecd6a1106242b8926fe19e32c7e2ab6ec2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994884"
---
# <a name="delete-a-user-account-for-a-customer"></a>Usuwanie konta użytkownika dla klienta

W tym artykule wyjaśniono, jak usunąć istniejące konto użytkownika dla klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika. Jeśli nie masz identyfikatora użytkownika, zobacz Get a list of all user accounts for a customer (Uzyskiwanie listy wszystkich kont [użytkowników dla klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="deleting-a-user-account"></a>Usuwanie konta użytkownika

Po usunięciu konta użytkownika stan użytkownika jest ustawiany na nieaktywny **przez** 30 dni. Po upływie 30 dni konto użytkownika i skojarzone z nim dane są przeczyszczane i nienadajne do nieodwracalności.

Możesz [przywrócić usunięte konto użytkownika dla klienta,](restore-a-user-for-a-customer.md) jeśli nieaktywne konto znajduje się w 30-dniowym oknie. Jednak po przywróceniu konta, które zostało usunięte i oznaczone jako nieaktywne, konto nie jest już zwracane jako element członkowski kolekcji użytkowników (na przykład w przypadku uzyskania listy wszystkich kont użytkowników dla [klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Aby usunąć istniejące konto użytkownika klienta:

1. Użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.

2. Wywołaj [**metodę Users.ById,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) aby zidentyfikować użytkownika.

3. Wywołaj [**metodę Delete,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) aby usunąć użytkownika i ustawić stan użytkownika na nieaktywny.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: DeleteCustomerUser.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów zapytania, aby zidentyfikować klienta i użytkownika.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| identyfikator dzierżawy klienta     | GUID     | Y        | Wartość jest identyfikatorem **customer-tenant-id** w formacie identyfikatora GUID, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta. |
| user-id                | GUID     | Y        | Wartość jest identyfikatorem użytkownika w formacie **GUID,** który należy do jednego konta użytkownika.                                          |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca kod **stanu 204 Brak** zawartości.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
