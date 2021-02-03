---
title: Aktualizowanie żądania obsługi
description: Jak zaktualizować istniejące żądanie obsługi klienta zgłoszone przez dostawcę rozwiązań w chmurze do firmy Microsoft w imieniu klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768369"
---
# <a name="update-a-service-request"></a>Aktualizowanie żądania obsługi

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak zaktualizować istniejące żądanie obsługi klienta zgłoszone przez dostawcę rozwiązań w chmurze do firmy Microsoft w imieniu klienta.

Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md). Następnie wybierz pozycję **Zarządzanie usługami** na lewym pasku bocznym. W nagłówku **żądania pomocy technicznej** wybierz odpowiednie żądanie obsługi. Aby zakończyć, wprowadź odpowiednie zmiany w żądaniu usługi, a następnie wybierz pozycję **Prześlij.**

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator żądania obsługi.

## <a name="c"></a>C\#

Aby zaktualizować żądanie obsługi klienta, wywołaj metodę [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) z identyfikatorem żądania obsługi, aby zidentyfikować i zwrócić interfejs żądania obsługi. Następnie Wywołaj metodę [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) lub [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) , aby zaktualizować żądanie obsługi. Aby podać zaktualizowane wartości, Utwórz nowy, pusty obiekt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) i ustaw tylko wartości właściwości, które chcesz zmienić. Następnie Przekaż ten obiekt w wywołaniu metody patch lub PatchAsync.

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdatePartnerServiceRequest.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/servicerequests/{ServiceRequest-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Aby zaktualizować żądanie obsługi, użyj następującego parametru identyfikatora URI.

| Nazwa                  | Typ     | Wymagane | Opis                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **Identyfikator żądania ServiceRequest** | **guid** | Y        | Identyfikator GUID, który identyfikuje żądanie obsługi. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania powinna zawierać zasób [ServiceRequest](service-request-resources.md) . Jedyne wymagane wartości to te, które mają zostać zaktualizowane.

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca zasób **żądania obsługi** ze zaktualizowanymi właściwościami w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
