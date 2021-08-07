---
title: Pobieranie ról użytkowników dla klienta
description: Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika. Odmiany obejmują pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników klienta i pobieranie listy użytkowników, którzy mają danej roli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b139ee69ae5148896b1a438b061907e022175f318956667cebb91ead15b863f6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989342"
---
# <a name="get-user-roles-for-a-customer"></a>Pobieranie ról użytkowników dla klienta

Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika. Odmiany obejmują pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników klienta i pobieranie listy użytkowników, którzy mają danej roli.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby pobrać wszystkie role katalogu dla określonego klienta, najpierw pobierz określony identyfikator klienta. Następnie użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().** Następnie wywołaj **właściwość DirectoryRoles,** a następnie metodę **Get()** lub **GetAsync().**

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomerDirectoryRoles.cs

Aby pobrać listę użytkowników klientów, którzy mają określoną rolę, najpierw pobierz określony identyfikator klienta i identyfikator roli katalogu. Następnie użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().** Następnie wywołaj właściwość **DirectoryRoles,** następnie metodę **ById(),** następnie właściwość **UserMembers,** a następnie metodę **Get()** lub **GetAsync().**

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** Klasa PartnerSDK.FeatureSamples: GetCustomerDirectoryRoleUserMembers.cs 

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1 |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles HTTP/1.1                 |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles/{identyfikator-roli}/usermembers    |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zidentyfikować prawidłowego klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.                                                      |
| **identyfikator użytkownika**            | **guid** | N        | Wartość to identyfikator GUID sformatowany **jako identyfikator użytkownika** należący do jednego konta użytkownika.                                                                                                                            |
| **identyfikator roli**            | **guid** | N        | Wartość jest identyfikatorem roli sformatowanym **przez identyfikator** GUID, który należy do typu roli. Te identyfikatory można uzyskać, odpytując wszystkie role katalogu dla klienta na wszystkich kontach użytkowników. (Drugi scenariusz powyżej). |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca listę ról skojarzonych z danym kontem użytkownika.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
