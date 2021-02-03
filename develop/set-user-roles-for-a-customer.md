---
title: Ustawianie ról użytkownika dla klienta
description: W ramach konta klienta istnieje zestaw ról w katalogu. Do tych ról można przypisywać konta użytkowników.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768269"
---
# <a name="set-user-roles-for-a-customer"></a>Ustawianie ról użytkownika dla klienta

**Dotyczy**

- Centrum partnerskie

W ramach konta klienta istnieje zestaw ról w katalogu. Do tych ról można przypisywać konta użytkowników.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby przypisać rolę katalogu do użytkownika klienta, Utwórz nowy [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) z odpowiednimi szczegółami użytkownika. Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta, aby zidentyfikować klienta. W tym miejscu Użyj metody [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu, aby określić rolę. Następnie uzyskaj dostęp do kolekcji **UserMembers** i użyj metody [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) , aby dodać członka nowego użytkownika do kolekcji członków użytkownika przypisanych do tej roli.

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: AddUserMemberToDirectoryRole.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów identyfikatora URI, aby zidentyfikować prawidłowego klienta i rolę. Aby zidentyfikować użytkownika, do którego ma zostać przypisana rola, podaj informacje identyfikacyjne w treści żądania.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |
| **Identyfikator roli**            | **guid** | Y        | Wartość jest **identyfikatorem** GUID z sformatowaną rolą identyfikującą rolę, która ma zostać przypisana do użytkownika.                                                              |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                  | Typ       | Wymagane | Opis                            |
|-----------------------|------------|----------|----------------------------------------|
| **#C1**                | **parametry** | Y        | Identyfikator użytkownika, który ma zostać dodany do roli. |
| **Nazwa wyświetlana**       | **parametry** | Y        | Przyjazna nazwa wyświetlana użytkownika. |
| **UserPrincipalName** | **parametry** | Y        | Nazwa podmiotu zabezpieczeń użytkownika.        |
| **Atrybuty**        | **Stream** | Y        | Zawiera "ObjectType": "UserMember"     |

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Ta metoda zwraca konto użytkownika z identyfikatorem roli dołączonym, gdy użytkownik pomyślnie przypisał rolę.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
