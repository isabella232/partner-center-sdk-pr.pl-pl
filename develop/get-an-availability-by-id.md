---
title: Uzyskiwanie dostępności według identyfikatora
description: Pobiera dostępność dla określonego produktu i sku przy użyciu identyfikatora dostępności.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: fccd566e83dab8994280fdee072c0d6f27b690d5292ed3973427088f46b30d6b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993558"
---
# <a name="get-the-availability-by-id"></a>Uzyskiwanie dostępności według identyfikatora

Pobiera dostępność dla określonego produktu i sku przy użyciu identyfikatora dostępności.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator produktu.

- Identyfikator SKU.

- Identyfikator dostępności.

## <a name="c"></a>C\#

Aby uzyskać szczegółowe informacje o określonej [dostępności,](product-resources.md#availability)rozpocznij od kroków z artykułu Get a SKU by ID to get the interface for a specific SKU's operations (Uzyskiwanie [skuku](get-a-sku-by-id.md) według identyfikatora) w celu uzyskania interfejsu dla operacji [określonej sku.](product-resources.md#sku) Z wynikowego interfejsu wybierz właściwość **Availabilities,** aby uzyskać interfejs z dostępnymi operacjami dla właściwości Dostępność. Następnie przekaż identyfikator dostępności do metody **ById(),** aby pobrać operacje dotyczące określonej dostępności, a następnie wywołaj metodę **Get()** lub **GetAsync(),** aby pobrać szczegóły dostępności.

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

Aby uzyskać szczegółowe informacje o określonej [dostępności,](product-resources.md#availability)rozpocznij od kroków z artykułu Get a SKU by ID to get the interface for a specific SKU's operations (Uzyskiwanie [skuku](get-a-sku-by-id.md) według identyfikatora) w celu uzyskania interfejsu dla operacji [określonej sku.](product-resources.md#sku) Z wynikowego interfejsu wybierz funkcję **getAvailabilities,** aby uzyskać interfejs z dostępnymi operacjami dostępności. Następnie przekaż identyfikator dostępności do funkcji **byId(),** aby pobrać operacje dotyczące określonej dostępności, a następnie wywołaj funkcję **get(),** aby pobrać szczegóły dostępności.

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
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1         |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać określoną dostępność przy użyciu identyfikatora dostępności.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | ciąg   | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje produkt.            |
| identyfikator sku                 | ciąg   | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje sku.                |
| identyfikator dostępności        | ciąg   | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje dostępność.       |
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

### <a name="response-example"></a>Przykład odpowiedzi

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
