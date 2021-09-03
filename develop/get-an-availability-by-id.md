---
title: Uzyskiwanie dostępności według identyfikatora
description: Pobiera dostępność dla określonego produktu i sku przy użyciu identyfikatora dostępności.
ms.date: 02/16/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 5bbbfdfeb81a915e5399bf2a89f99a70b509476d
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456158"
---
# <a name="get-the-availability-by-id"></a>Uzyskiwanie dostępności według identyfikatora

Pobiera dostępność dla określonego produktu i sku przy użyciu identyfikatora dostępności.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator produktu.

- Identyfikator SKU.

- Identyfikator dostępności.

## <a name="c"></a>C\#

Aby uzyskać szczegółowe informacje o określonej [dostępności,](product-resources.md#availability)zacznij od kroków z artykułu Get [a SKU by ID (Uzyskiwanie sku za](get-a-sku-by-id.md) pomocą identyfikatora) w celu uzyskania interfejsu dla operacji [określonej sku.](product-resources.md#sku) Z wynikowego interfejsu wybierz właściwość **Availabilities,** aby uzyskać interfejs z dostępnymi operacjami dla właściwości Availabilities. Następnie przekaż identyfikator dostępności do metody **ById(),** aby pobrać operacje dla tej określonej dostępności, a następnie wywołaj metodę **Get()** lub **GetAsync(),** aby pobrać szczegóły dostępności.

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać szczegółowe informacje o określonej [dostępności,](product-resources.md#availability)zacznij od kroków z artykułu Get [a SKU by ID (Uzyskiwanie sku za](get-a-sku-by-id.md) pomocą identyfikatora) w celu uzyskania interfejsu dla operacji [określonej sku.](product-resources.md#sku) Z wynikowego interfejsu wybierz funkcję **getAvailabilities,** aby uzyskać interfejs z dostępnymi operacjami dostępności. Następnie przekaż identyfikator dostępności do funkcji **byId(),** aby pobrać operacje dla tej określonej dostępności, a następnie wywołaj funkcję **get(),** aby pobrać szczegóły dostępności.

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać szczegółowe informacje o [określonej](product-resources.md#availability)dostępności, wykonaj polecenie [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) i określ parametry **AvailabilityId**, **CountryCode,** **ProductId** i **SkuId,** aby pobrać szczegóły dostępności.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **POBIERZ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{identyfikator-produktu}/skus/{sku-id}/availabilities/{identyfikator-dostępności}?country={kod-kraju} HTTP/1.1         |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać określoną dostępność przy użyciu identyfikatora dostępności.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| identyfikator produktu             | ciąg   | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje produkt.            |
| identyfikator sku                 | ciąg   | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje sku.                |
| identyfikator dostępności        | ciąg   | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje dostępność.       |
| kod kraju           | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób Availability.](product-resources.md#availability)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Nie znaleziono produktu.                                                                                    |
| 404                  | 400018       | Nie znaleziono sku.                                                                                        |
| 404                  | 400019       | Nie znaleziono dostępności.                                                                                   |

### <a name="response-example-for-azure-vm-reservations-azure-plan"></a>Przykład odpowiedzi dla rezerwacji maszyn wirtualnych platformy Azure (plan platformy Azure)

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```

### <a name="response-example-for-new-commerce-license-based-services"></a>Przykład odpowiedzi dla nowych usług opartych na licencjach handlowych

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "id": "CFQ7TTC0K971",
    "productId": "CFQ7TTC0LH18",
    "skuId": "0001",
    "catalogItemId": "CFQ7TTC0LH18:0001:CFQ7TTC0K971",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": true, 
    "renewalInstructions": [
        {
            "applicableTermIds": [
                "5aeco6mffyxo"
            ],
            "renewalOptions": [
                {
                    "renewToId": "CFQ7TTC0LH18:0001",
                    "isAutoRenewable": true
                }
            ]
        },
     …
    ],
    "terms": [
        {
            "id": "5aeco6mffyxo",
            "duration": "P1Y",
            "description": "One-Year commitment for monthly/yearly billing",
            "billingCycle": "Annual",
            "cancellationPolicies": [
                {
                    "refundOptions": [
                        {
                            "sequenceId": 0,
                            "type": "Full",
                            "expiresAfter": "P1D"
                        }
                    ]
                }
            ]
        },
       …
    ],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/CFQ7TTC0LH18/skus/0001/availabilities/CFQ7TTC0K971?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
