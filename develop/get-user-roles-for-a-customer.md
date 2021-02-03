---
title: Pobieranie ról użytkowników dla klienta
description: Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika. Warianty obejmują Pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników dla klienta i pobieranie listy użytkowników, którzy mają daną rolę.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767813"
---
# <a name="get-user-roles-for-a-customer"></a>Pobieranie ról użytkowników dla klienta

**Dotyczy**

- Centrum partnerskie

Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika. Warianty obejmują Pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników dla klienta i pobieranie listy użytkowników, którzy mają daną rolę.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby pobrać wszystkie role katalogu dla określonego klienta, najpierw Pobierz określony identyfikator klienta. Następnie użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** . Następnie Wywołaj Właściwość **DirectoryRoles** , a następnie metodę **Get ()** lub **GetAsync ()**.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetCustomerDirectoryRoles.cs

Aby pobrać listę użytkowników klientów, którzy mają daną rolę, najpierw Pobierz określony identyfikator klienta i identyfikator roli katalogu. Następnie użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** . Następnie Wywołaj Właściwość **DirectoryRoles** , a następnie metodę **ById ()** , a następnie właściwość **UserMembers** , a następnie metodę **Get ()** lub **GetAsync ()** .

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSamples **Klasa**: GetCustomerDirectoryRoleUserMembers.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID}/directoryroles http/1.1 |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles http/1.1                 |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers    |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zidentyfikować odpowiedniego klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.                                                      |
| **Identyfikator użytkownika**            | **guid** | N        | Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.                                                                                                                            |
| **Identyfikator roli**            | **guid** | N        | Wartość jest **identyfikatorem** GUID o formacie ID, który należy do typu roli. Identyfikatory te można uzyskać, badając wszystkie role katalogu dla klienta w ramach wszystkich kont użytkowników. (Drugi scenariusz, powyżej). |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca listę ról skojarzonych z danym kontem użytkownika.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
