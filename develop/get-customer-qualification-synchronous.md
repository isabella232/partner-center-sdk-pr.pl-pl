---
title: Pobieranie kwalifikacji klienta
description: Dowiedz się, jak za pomocą synchronicznej walidacji uzyskać kwalifikację klienta za pośrednictwem Partner Center API. Partnerzy mogą używać tego do weryfikowania klientów edukacyjnych.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446347"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a>Uzyskiwanie kwalifikacji klienta za pośrednictwem walidacji synchronicznej

Dowiedz się, jak synchronicznie uzyskać kwalifikację klienta za pośrednictwem Partner Center API. Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz Get a customer's qualification via asynchronous validation (Uzyskiwanie [kwalifikacji klienta za pośrednictwem walidacji asynchronicznej).](get-customer-qualification-asynchronous.md)

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby uzyskać kwalifikację klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta. Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Na koniec [**wywołaj usługę Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) aby pobrać kwalifikację klienta.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania wszystkich kwalifikacji.

| Nazwa               | Typ   | Wymagane | Opis                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **identyfikator dzierżawy klienta** | ciąg | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca wartość kwalifikacji w treści odpowiedzi.  Poniżej znajduje się przykład rozmowy **GET** dotyczącej klienta z kwalifikacją **edukacyjną.**

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a>Pokrewne artykuły:

- [Aktualizowanie kwalifikacji klienta](./update-customer-qualification-synchronous.md)