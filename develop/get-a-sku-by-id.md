---
title: Pobieranie jednostki SKU według identyfikatora
description: Pobiera SKU dla określonego produktu przy użyciu określonego identyfikatora SKU.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3be496b694d9e0e34619807e85ed8fe63879f3561a404ebc7361dcedc4479612
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994187"
---
# <a name="get-a-sku-by-id"></a>Pobieranie jednostki SKU według identyfikatora

Pobiera SKU dla określonego produktu przy użyciu określonego identyfikatora SKU.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator produktu.

- Identyfikator SKU.

## <a name="c"></a>C\#

Aby uzyskać szczegółowe informacje o określonej sku, zacznij od kroków z artykułu Get [a product by ID (Uzyskiwanie](get-a-product-by-id.md) produktu według identyfikatora) w celu uzyskania interfejsu dla operacji określonego produktu. Z wynikowego interfejsu wybierz właściwość **Jednostki SKU,** aby uzyskać interfejs z dostępnymi operacjami dla jednostki SKU. Przekaż identyfikator SKU do metody **ById()** i wywołaj metodę **Get()** lub **GetAsync(),** aby pobrać szczegóły dotyczące tej sku.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1   |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać wartość SKU dla określonego produktu przy użyciu określonego identyfikatora SKU.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | ciąg   | Tak      | Ciąg identyfikujący produkt.                           |
| identyfikator sku                 | ciąg   | Tak      | Ciąg identyfikujący sku.                               |
| kod kraju           | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SKU.](product-resources.md#sku)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Nie znaleziono produktu.                                                                                    |
| 404                  | 400018       | Nie znaleziono sku.                                                                                        |

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```
