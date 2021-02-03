---
title: Pobieranie odsprzedawców pośrednich klienta
description: Jak uzyskać listę pośrednich odsprzedawcaów, które mają relację z określonym klientem.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d69abf9530548f110820ca04fefb698e0e37556c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768334"
---
# <a name="get-indirect-resellers-of-a-customer"></a>Pobieranie odsprzedawców pośrednich klienta

**Dotyczy**

- Centrum partnerskie

Jak uzyskać listę pośrednich odsprzedawcaów, które mają relację z określonym klientem.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby pobrać listę pośrednich odsprzedawcaów, z którymi określony klient ma relację, należy najpierw uzyskać interfejs do operacji zbierania danych klienta dla określonego klienta z właściwości [**partnerOperations. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) , podając identyfikator klienta w celu zidentyfikowania klienta. Następnie Wywołaj [**relacje. Pobierz**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) lub [**Pobierz metodę \_ asynchroniczną**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) , aby uzyskać listę pośrednich odsprzedawcaów.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: GetIndirectResellersOfCustomer.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Relationships http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa        | Typ   | Wymagane | Opis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerRelationship](relationships-resources.md) , aby zidentyfikować odsprzedawcy.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
