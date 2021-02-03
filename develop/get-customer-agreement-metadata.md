---
title: Pobieranie metadanych umowy dla umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać metadane umów dla umowy klienta firmy Microsoft.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768162"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Pobieranie metadanych umowy dla umowy klienta firmy Microsoft

**Dotyczy:**

- Centrum partnerskie

Metadane umowy dla umowy klienta firmy Microsoft są obecnie obsługiwane przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*. Nie dotyczy:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Przed rozpoczęciem można pobrać metadane umów licencyjnych firmy Microsoft:

- [Potwierdzanie akceptacji umowy klienta firmy Microsoft przez klienta](./confirm-customer-consent-customer-agreement.md)
- [Pobierz link pobierania dla szablonu umowy klienta firmy Microsoft](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Wymagania wstępne

- W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.

## <a name="net-version-114-or-newer"></a>.NET (wersja 1,14 lub nowsza)

Aby pobrać metadane umowy dla umowy klienta firmy Microsoft:

1. Najpierw pobierz kolekcję **IAggregatePartner. AgreementDetails** .

2. Wywołaj metodę **ByAgreementType** , aby odfiltrować kolekcję do umowy klienta firmy Microsoft.

3. Na koniec Wywołaj metodę **Get** lub **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Żądanie REST

Aby pobrać metadane umowy dla umowy klienta firmy Microsoft:

1. Utwórz żądanie REST w celu pobrania kolekcji [AgreementMetaData](./agreement-metadata-resources.md) .

2. Użyj parametru **querytype** , aby ograniczyć wynik do umowy klienta firmy Microsoft.

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/V1/Agreements? agreementtype = {Agreement-Type} http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

| Nazwa                   | Typ     | Wymagane | Opis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| typ umowy | ciąg | Nie | Użyj tego parametru, aby ograniczyć odpowiedź zapytania do określonego typu umowy. Obsługiwane są następujące wartości: <br/><br/>**MicrosoftCloudAgreement** obejmujący metadane umów tylko typu *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement** obejmujący metadane umów tylko typu *MicrosoftCustomerAgreement*.<br/><br/>**\*** zwraca wszystkie metadane umowy. (Nie używaj **\*** , chyba że Twój kod ma niezbędną logikę uruchomieniową do obsługi nieznanych typów umów, ponieważ firma Microsoft może w dowolnym czasie wprowadzić metadane umów z nowymi typami umów).<br/><br/> **Uwaga:** Jeśli parametr URI nie jest określony, zapytanie jest domyślnie **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami.  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję [zasobów **AgreementMetaData**](./agreement-metadata-resources.md) w treści odpowiedzi.

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
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
