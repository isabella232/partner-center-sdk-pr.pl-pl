---
title: Usuwanie użytkownika klienta z roli
description: Jak usunąć użytkownika z roli katalogu w ramach konta klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 985b80a35182aefe283a8e9bbff75a1ff7bd9790157147fb943d8b18eb5c5079
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996992"
---
# <a name="remove-a-customer-user-from-a-role"></a>Usuwanie użytkownika klienta z roli

Jak usunąć użytkownika z roli katalogu w ramach konta klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby usunąć użytkownika z roli katalogu, wybierz klienta z użytkownikiem do zmodyfikowania za pomocą wywołania metody [**IAggregatePartner.Customers.ById.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) W tym miejscu określ rolę przy użyciu metody [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu. Następnie uzyskaj dostęp do [**metody UserMembers.ById,**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) aby zidentyfikować użytkownika do usunięcia, i metody [**Delete,**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) aby usunąć użytkownika z roli.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project**: zestaw SDK Centrum partnerskiego Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Usunąć** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles/{identyfikator-roli}/usermembers/{identyfikator użytkownika} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów identyfikatorów URI, aby zidentyfikować odpowiedniego klienta, rolę i użytkownika.

| Nazwa                   | Typ     | Wymagane | Opis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID w **formacie customer-tenant-id,** który identyfikuje klienta. |
| **identyfikator roli**            | **guid** | Y        | Wartość jest identyfikatorem roli sformatowanym **przez identyfikator GUID,** który identyfikuje rolę.                |
| **identyfikator użytkownika**            | **guid** | Y        | Wartość to identyfikator GUID sformatowany **jako identyfikator użytkownika,** który identyfikuje jedno konto użytkownika.   |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli użytkownik zostanie pomyślnie usunięty z roli, treść odpowiedzi będzie pusta.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

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
