---
title: Pobieranie metadanych umowy dla umowy klienta firmy Microsoft
description: W tym artykule wyjaśniono, jak uzyskać metadane umowy dla Umowa z Klientem Microsoft.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025724"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Pobieranie metadanych umowy dla umowy klienta firmy Microsoft

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Metadane umowy dla Umowa z Klientem Microsoft są obecnie obsługiwane Partner Center tylko w chmurze publicznej firmy Microsoft.

Musisz pobrać metadane umowy dla Umowa z Klientem Microsoft, aby można było:

- [Potwierdź zgodę klienta na Umowa z Klientem Microsoft](./confirm-customer-consent-customer-agreement.md)
- [Pobieranie linku pobierania dla Umowa z Klientem Microsoft szablonu](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Wymagania wstępne

- Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.14 lub nowsza.

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md) Ten scenariusz obsługuje tylko uwierzytelnianie app+user.

## <a name="net-version-114-or-newer"></a>.NET (wersja 1.14 lub nowsza)

Aby pobrać metadane umowy dla Umowa z Klientem Microsoft:

1. Najpierw pobierz **kolekcję IAggregatePartner.AgreementDetails.**

2. Wywołaj **metodę ByAgreementType,** aby filtrować kolekcję w Umowa z Klientem Microsoft.

3. Na koniec wywołaj **metodę Get** lub **GetAsync.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>Żądanie REST

Aby pobrać metadane umowy dla Umowa z Klientem Microsoft:

1. Utwórz żądanie REST, aby pobrać [kolekcję AgreementMetaData.](./agreement-metadata-resources.md)

2. Użyj **parametru zapytania agreementType,** aby zawęzać wynik tylko do Umowa z Klientem Microsoft.

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

| Nazwa                   | Typ     | Wymagane | Opis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| typ umowy | ciąg | Nie | Użyj tego parametru, aby określać zakres odpowiedzi na zapytanie dla określonego typu umowy. Obsługiwane wartości to: <br/><br/>**MicrosoftCloudAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement,** który zawiera tylko metadane umowy typu *MicrosoftCustomerAgreement*.<br/><br/>**\**_ zwraca wszystkie metadane umowy. (Nie używaj _* \* _, chyba że kod ma logikę środowiska uruchomieniowego niezbędną do obsługi nieznanych typów umów, ponieważ firma Microsoft może w dowolnym momencie wprowadzić metadane umowy z *nowymi typami umów). <br/> <br/> _* Uwaga:** Jeśli parametr URI nie zostanie określony, zapytanie domyślnie będzie mieć wartość **MicrosoftCloudAgreement** w celu zapewnienia zgodności z poprzednimi wersjami.  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca kolekcję [ **zasobów AgreementMetaData**](./agreement-metadata-resources.md) w treści odpowiedzi.

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
