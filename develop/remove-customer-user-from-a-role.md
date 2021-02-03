---
title: Usuwanie użytkownika klienta z roli
description: Jak usunąć użytkownika z roli katalogu w ramach konta klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253e86f3733bbf2b9c593c5ca3f3e2fccce7c2c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768306"
---
# <a name="remove-a-customer-user-from-a-role"></a>Usuwanie użytkownika klienta z roli

**Dotyczy**

- Centrum partnerskie

Jak usunąć użytkownika z roli katalogu w ramach konta klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby usunąć użytkownika z roli katalogu, wybierz klienta, który ma zostać zmodyfikowany za pomocą wywołania metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) , w tym miejscu określ rolę przy użyciu metody [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu. Następnie uzyskaj dostęp do metody [**UserMembers. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) , aby zidentyfikować użytkownika do usunięcia, i metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) , aby usunąć użytkownika z roli.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **USUNIĘTY** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers/{User-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów identyfikatora URI, aby zidentyfikować prawidłowy klient, rolę i użytkownika.

| Nazwa                   | Typ     | Wymagane | Opis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , który identyfikuje klienta. |
| **Identyfikator roli**            | **guid** | Y        | Wartość jest **identyfikatorem** GUID z sformatowaną rolą identyfikującą rolę.                |
| **Identyfikator użytkownika**            | **guid** | Y        | Wartość jest **identyfikatorem użytkownika** w formacie identyfikatora GUID, który identyfikuje pojedyncze konto użytkownika.   |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli użytkownik zostanie pomyślnie usunięty z roli, treść odpowiedzi jest pusta.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
