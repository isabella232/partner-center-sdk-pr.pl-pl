---
title: Usuwanie konta użytkownika dla klienta
description: Jak usunąć istniejące konto użytkownika dla klienta.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768129"
---
# <a name="delete-a-user-account-for-a-customer"></a>Usuwanie konta użytkownika dla klienta

**Dotyczy:**

- Centrum partnerskie

W tym artykule wyjaśniono, jak usunąć istniejące konto użytkownika dla klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika. Jeśli nie masz identyfikatora użytkownika, zobacz temat [Pobieranie listy wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md).

## <a name="deleting-a-user-account"></a>Usuwanie konta użytkownika

Po usunięciu konta użytkownika stan użytkownika jest ustawiony jako **nieaktywny** przez 30 dni. Po upływie 30 dni konto użytkownika i powiązane z nim dane są przeczyszczane i niemożliwym do odzyskania.

Można [przywrócić usunięte konto użytkownika dla klienta](restore-a-user-for-a-customer.md) , jeśli konto nieaktywne znajduje się w oknie trzydziestu dni. Jednak podczas przywracania konta, które zostało usunięte i oznaczone jako nieaktywne, konto nie jest już zwracane jako element członkowski kolekcji użytkowników (na przykład po wyświetleniu [listy wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Aby usunąć istniejące konto użytkownika klienta:

1. Użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.

2. Wywołaj metodę [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować użytkownika.

3. Wywołaj metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) , aby usunąć użytkownika i ustawić stan użytkownika jako nieaktywny.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: DeleteCustomerUser.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID} http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów zapytania, aby zidentyfikować klienta i użytkownika.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| Identyfikator dzierżawy klienta     | GUID     | Y        | Wartość jest formatem **identyfikatora dzierżawy klienta** w formacie GUID, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta. |
| user-id                | GUID     | Y        | Wartość jest **identyfikatorem użytkownika** sformatowanym przez identyfikator GUID, który należy do jednego konta użytkownika.                                          |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, ta metoda zwraca 204 kod stanu **zawartości** .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
