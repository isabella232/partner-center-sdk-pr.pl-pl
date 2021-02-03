---
title: Pobieranie listy odsprzedawców pośrednich
description: Jak pobrać listę pośrednich odsprzedawcaów zalogowanego partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768398"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Pobieranie listy odsprzedawców pośrednich

**Dotyczy**

- Centrum partnerskie

Jak pobrać listę pośrednich odsprzedawcaów zalogowanego partnera.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

## <a name="c"></a>C\#

Aby pobrać listę pośrednich odsprzedawcaów, z którymi partner zalogowany ma relację, należy najpierw uzyskać interfejs do operacji kolekcji relacji z właściwości [**partnerOperations. Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) . Następnie Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) lub [**get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , przekazując element członkowski wyliczenia [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) , aby zidentyfikować typ relacji. Aby pobrać pośrednich odsprzedawcaów, musisz użyć IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: GetIndirectResellers.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Relationships? \_ Typ relacji = IsIndirectCloudSolutionProviderOf http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zidentyfikować typ relacji.

| Nazwa               | Typ    | Wymagane  | Opis                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | ciąg  | Tak       | Wartość jest reprezentacją ciągu jednej z nazw składowych znalezionych w [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).<br/><br/> Jeśli partner jest zalogowany jako dostawca i chcesz uzyskać listę pośrednich odsprzedawcaów, z którymi ustanowiono relację, użyj IsIndirectCloudSolutionProviderOf.<br/><br/> Jeśli partner jest zalogowany jako odsprzedawca i chcesz uzyskać listę dostawców pośrednich, którym ustanowiono relację, użyj IsIndirectResellerOf.    |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
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
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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