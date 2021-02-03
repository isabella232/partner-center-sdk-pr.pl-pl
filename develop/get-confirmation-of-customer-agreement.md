---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768166"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft

**Dotyczy:**

- Centrum partnerskie

Zasób **umowy** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*. Ten zasób nie ma zastosowania do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule wyjaśniono, jak można pobrać potwierdzenia akceptacji umowy klienta firmy Microsoft przez klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="net"></a>.NET

Aby pobrać potwierdzenia, które zostały wcześniej dostarczone przez klienta:

- Użyj metody **IAggregatePartner. Customers** i Wywołaj metodę **ById** z określonym identyfikatorem klienta.

- Pobierz Właściwość **Agreements** i przefiltruj wyniki do umowy klienta firmy Microsoft przez wywołanie metody **ByAgreementType** .

- Wywoływanie metody **Get** lub **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Żądanie REST

Aby pobrać potwierdzenie przyjęcia przez klienta wcześniej dostarczonego:

1. Utwórz żądanie REST w celu pobrania kolekcji [umów](./agreement-resources.md) dla klienta.

2. Użyj parametru **querytype** , aby ograniczyć wyniki do umowy klienta firmy Microsoft.

### <a name="request-syntax"></a>Składnia żądania

Użyj następującej składni żądania:

| Metoda | Identyfikator URI żądania                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements? agreementtype = {Agreement-Type} http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Z żądaniem można użyć następujących parametrów URI:

| Nazwa             | Typ | Wymagane | Opis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| Identyfikator dzierżawy klienta | GUID | Tak | Wartość jest identyfikatorem GUID w formacie **CustomerTenantId** , który umożliwia określenie klienta. |
| typ umowy | ciąg | Nie | Ten parametr zwraca wszystkie metadane umowy. Użyj tego parametru, aby ograniczyć odpowiedź zapytania do określonego typu umowy. Obsługiwane są następujące wartości: <br/><br/> **MicrosoftCloudAgreement** , który zawiera tylko metadane umów typu *MicrosoftCloudAgreement*.<br/><br/> **MicrosoftCustomerAgreement** , który zawiera tylko metadane umów typu *MicrosoftCustomerAgreement*.<br/><br/> **\*** zwraca wszystkie metadane umowy. (Nie używaj **\*** , chyba że kod ma niezbędną logikę do obsługi nieoczekiwanych typów umowy).<br/><br/> **Uwaga:** Jeśli parametr URI nie jest określony, zapytanie jest domyślnie **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami. Firma Microsoft może w dowolnym momencie wprowadzać metadane umów z nowymi typami umów.  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.

Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
