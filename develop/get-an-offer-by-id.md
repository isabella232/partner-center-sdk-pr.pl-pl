---
title: Pobieranie oferty według identyfikatora
description: Pobiera zasób oferty, który jest zgodny z IDENTYFIKATORem oferty.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768481"
---
# <a name="get-an-offer-by-id"></a>Pobieranie oferty według identyfikatora

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Pobiera zasób **oferty** , który jest zgodny z identyfikatorem oferty.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator oferty.

## <a name="c"></a>C\#

Aby znaleźć określoną ofertę według identyfikatora, Użyj kolekcji **IAggregatePartner. offers** , ustal kraj z wywołaniem **ByCountry ()**, a następnie Wywołaj metodę [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) . Następnie Wywołaj metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) lub [**Get Async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) .

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSample **Klasa**: GetOffer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby znaleźć określoną ofertę według identyfikatora, użyj funkcji **IAggregatePartner. Getoffers** , ustal kraj z wywołaniem funkcji **byCountry ()** , a następnie wywołaj funkcję **byID ()** . Następnie wywołaj funkcję **Get ()** .

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby znaleźć określoną ofertę według identyfikatora, należy wykonać polecenie [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) i określić parametry **CountryCode** i **OfferId** .

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/offers/{Offer-ID}? Country = {Country-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

| Nazwa           | Typ       | Wymagane | Opis                           |
|----------------|------------|----------|---------------------------------------|
| **Oferta — identyfikator**   | **guid**   | Y        | Identyfikator GUID, który odpowiada ofercie. |
| **Identyfikator kraju** | **parametry** | Y        | Identyfikator kraju/regionu.                |

### <a name="request-headers"></a>Nagłówki żądań

- Wymagany jest **identyfikator ustawień regionalnych** , który jest sformatowany jako ciąg.
Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca zasób **oferty** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
