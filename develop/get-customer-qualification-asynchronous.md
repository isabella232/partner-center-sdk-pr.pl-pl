---
title: Uzyskiwanie kwalifikacji klienta
description: Dowiedz się, jak za pomocą walidacji asynchronicznej uzyskać kwalifikację klienta za pośrednictwem Partner Center API. Partnerzy mogą używać tej funkcji do weryfikowania klientów edukacyjnych.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 4795b6e1ad008f9d854dc7efbee0c2099aefa609
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446313"
---
# <a name="get-a-customers-qualification-asynchronously"></a>Asynchroniczne uzyskiwanie kwalifikacji klienta

Jak asynchronicznie uzyskać kwalifikacje klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby uzyskać kwalifikacje klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta. Następnie użyj właściwości [**Qualification,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Na koniec zadzwoń `GetQualifications()` na numer lub , aby pobrać `GetQualificationsAsync()` kwalifikacje klienta.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

**Przykład:** [przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples, **klasa**: GetCustomerQualifications.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania wszystkich kwalifikacji.

| Nazwa               | Typ   | Wymagane | Opis                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **identyfikator dzierżawy klienta** | ciąg | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca kolekcję kwalifikacji w treści odpowiedzi.  Poniżej przedstawiono przykłady rozmowy **GET** dotyczącej klienta z kwalifikacją **do edukacji.**

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-examples"></a>Przykłady odpowiedzi

#### <a name="approved"></a>Approved (Zatwierdzono)

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

#### <a name="in-review"></a>Przegląd

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

#### <a name="denied"></a>Odmowa

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

#### <a name="state-owned-entity-samples"></a>Przykłady jednostek należących do stanu

**Przykład jednostki należącej do stanu za pośrednictwem posta**

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

**Jednostka należąca do stanu za pośrednictwem przykładu Pobierz kwalifikacje**

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

**Jednostka należąca do stanu za pośrednictwem get qualifications with Education**

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “Education”,
        “vettingStatus”: “Approved”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

**Jednostka należąca do stanu za pośrednictwem get qualifications with GCC**

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “GovernmentCommunityCloud”,
        “vettingStatus”: “Approved”,
        “vettingCreateDate”: “2021-05-06T19:59:56.6832021+00:00”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

## <a name="related-articles"></a>Pokrewne artykuły:

- [Aktualizowanie kwalifikacji klienta](./update-customer-qualification-asynchronous.md)
