---
title: Ustawianie ról użytkownika dla klienta
description: W ramach konta klienta istnieje zestaw ról katalogu. Do tych ról można przypisać konta użytkowników.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a035d711ffa91200fa7b479ed5ec53929aa4feaf
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446704"
---
# <a name="set-user-roles-for-a-customer"></a>Ustawianie ról użytkownika dla klienta

W ramach konta klienta istnieje zestaw ról katalogu. Do tych ról można przypisać konta użytkowników.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby przypisać rolę katalogu do użytkownika klienta, utwórz nowego użytkownika [**UserMember z**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) odpowiednimi szczegółami użytkownika. Następnie wywołaj metodę [**IAggregatePartner.Customers.ById z**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) określonym identyfikatorem klienta, aby zidentyfikować klienta. W tym miejscu użyj [**metody DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu, aby określić rolę. Następnie uzyskaj dostęp do **kolekcji UserMembers** i użyj metody [**Create,**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) aby dodać nowego członka użytkownika do kolekcji członków użytkowników przypisanych do tej roli.

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

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: AddUserMemberToDirectoryRole.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles/{identyfikator-roli}/usermembers HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów URI, aby zidentyfikować prawidłowego klienta i rolę. Aby zidentyfikować użytkownika, do którego ma zostać przypisana rola, należy podać informacje identyfikujące w treści żądania.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy. |
| **identyfikator roli**            | **guid** | Y        | Wartość jest identyfikatorem roli sformatowanym przez **identyfikator** GUID, który identyfikuje rolę, która ma zostać przypisana do użytkownika.                                                              |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                  | Typ       | Wymagane | Opis                            |
|-----------------------|------------|----------|----------------------------------------|
| **Identyfikator**                | **ciąg** | Y        | Identyfikator użytkownika, który ma dodać do roli. |
| **Nazwa wyświetlana**       | **ciąg** | Y        | Przyjazna nazwa wyświetlana użytkownika. |
| **Userprincipalname** | **ciąg** | Y        | Nazwa podmiotu zabezpieczeń użytkownika.        |
| **Atrybuty**        | **Obiektu** | Y        | Zawiera "ObjectType":"UserMember"     |

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

Ta metoda zwraca konto użytkownika z dołączonym identyfikatorem roli, gdy użytkownik zostanie pomyślnie przypisany do roli.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

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
