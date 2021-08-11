---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta Umowa z Klientem Microsoft.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f5e71f2660c6db638193deec02e9ba4f25a35be6aabdc1c4219f63b1f3295908
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993507"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Pobieranie potwierdzenia akceptacji przez klienta umowy klienta firmy Microsoft

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **Umowy** jest obecnie obsługiwany przez Partner Center tylko w chmurze publicznej firmy Microsoft.

W tym artykule wyjaśniono, jak można pobrać potwierdzenia akceptacji przez klienta Umowa z Klientem Microsoft.

## <a name="prerequisites"></a>Wymagania wstępne

- Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.14 lub nowsza.

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md) Ten scenariusz obsługuje tylko uwierzytelnianie app+user.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="net"></a>.NET

Aby pobrać wcześniej podane potwierdzenia akceptacji przez klienta:

- Użyj **kolekcji IAggregatePartner.Customers** i wywołaj metodę **ById** z określonym identyfikatorem klienta.

- Pobierz właściwość **Agreements** i przefiltruj wyniki, aby Umowa z Klientem Microsoft przez wywołanie **metody ByAgreementType.**

- Wywołaj **metodę Get** lub **GetAsync.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Kompletny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>Żądanie REST

Aby pobrać potwierdzenie akceptacji klienta, które zostało podane wcześniej:

1. Utwórz żądanie REST, aby pobrać [kolekcję Umowy](./agreement-resources.md) dla klienta.

2. Użyj **parametru zapytania agreementType,** aby określać zakres wyników tylko do Umowa z Klientem Microsoft.

### <a name="request-syntax"></a>Składnia żądania

Użyj następującej składni żądania:

| Metoda | Identyfikator URI żądania                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

W żądaniu można użyć następujących parametrów URI:

| Nazwa             | Typ | Wymagane | Opis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| identyfikator dzierżawy klienta | GUID | Tak | Wartość jest identyfikatorem GUID w **formacie CustomerTenantId,** który umożliwia określenie klienta. |
| typ umowy | ciąg | Nie | Ten parametr zwraca wszystkie metadane umowy. Użyj tego parametru, aby określać zakres odpowiedzi na zapytanie dla określonego typu umowy. Obsługiwane wartości to: <br/><br/> **MicrosoftCloudAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCloudAgreement*.<br/><br/> **MicrosoftCustomerAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCustomerAgreement*.<br/><br/> **\**_ zwraca wszystkie metadane umowy. (Nie używaj _* \* *_, chyba że kod ma logikę niezbędną do obsługi nieoczekiwanych typów umów). <br/> <br/> _* Uwaga:** Jeśli parametr URI nie zostanie określony, zapytanie domyślnie będzie mieć wartość **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami. Firma Microsoft może wprowadzać metadane umowy z nowymi typami umów w dowolnym momencie.  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.

Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

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
