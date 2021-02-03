---
title: Pobieranie listy kategorii oferty według rynku
description: Jak uzyskać kolekcję zawierającą wszystkie kategorie oferty w danym kraju/regionie i ustawieniach regionalnych.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 22c46ed03a8579c53ee18c14cbca9a1e19ddb82a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768237"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Pobieranie listy kategorii oferty według rynku

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano, jak uzyskać kolekcję zawierającą wszystkie kategorie oferty w danym kraju/regionie i ustawieniach regionalnych.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

## <a name="c"></a>C\#

Aby uzyskać listę kategorii oferty w danym kraju/regionie i ustawieniach regionalnych:

1. Użyj kolekcji [**IAggregatePartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) , aby wywołać metodę [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) w danym kontekście.

2. Sprawdź Właściwość [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) obiektu będącego wynikiem.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSample**
- Klasa: **PartnerSDK. FeatureSample**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/offercategories? Country = {Country-ID} http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania kategorii oferty.

| Nazwa           | Typ       | Wymagane | Opis            |
|----------------|------------|----------|------------------------|
| **Identyfikator kraju** | **parametry** | Y        | Identyfikator kraju/regionu. |

### <a name="request-headers"></a>Nagłówki żądań

Wymagany jest **identyfikator ustawień regionalnych** , który jest sformatowany jako ciąg.

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **OfferCategory** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
