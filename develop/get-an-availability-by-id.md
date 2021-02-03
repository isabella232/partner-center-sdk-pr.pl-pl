---
title: Pobierz dostępność według identyfikatora
description: Pobiera dostępność dla określonego produktu i jednostki SKU przy użyciu identyfikatora dostępności.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767714"
---
# <a name="get-the-availability-by-id"></a>Pobierz dostępność według identyfikatora

**Dotyczy**

- Centrum partnerskie

Pobiera dostępność dla określonego produktu i jednostki SKU przy użyciu identyfikatora dostępności.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator produktu.

- IDENTYFIKATOR JEDNOSTKI SKU.

- Identyfikator dostępności.

## <a name="c"></a>C\#

Aby uzyskać szczegółowe informacje o konkretnej [dostępności](product-resources.md#availability), Zacznij od wykonania kroków z sekcji [pobieranie jednostki SKU według identyfikatora](get-a-sku-by-id.md) , aby uzyskać interfejs dla operacji określonej [jednostki SKU](product-resources.md#sku) . Z poziomu interfejsu uzyskanego wybierz właściwość **dostępność** , aby uzyskać interfejs z dostępnymi operacjami dostępności. Następnie Przekaż identyfikator dostępności do metody **ById ()** w celu uzyskania operacji dla tej konkretnej dostępności, a następnie Wywołaj metodę **Get ()** lub **GetAsync ()** , aby pobrać szczegóły dostępności.

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

Aby uzyskać szczegółowe informacje o konkretnej [dostępności](product-resources.md#availability), Zacznij od wykonania kroków z sekcji [pobieranie jednostki SKU według identyfikatora](get-a-sku-by-id.md) , aby uzyskać interfejs dla operacji określonej [jednostki SKU](product-resources.md#sku) . W interfejsie wynikającym wybierz funkcję **getAvailabilities** , aby uzyskać interfejs z dostępnymi operacjami dostępności. Następnie Przekaż identyfikator dostępności do funkcji **byId ()** w celu uzyskania operacji dla tej konkretnej dostępności, a następnie wywołaj funkcję **Get ()** , aby pobrać szczegóły dostępności.

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

Aby uzyskać szczegółowe informacje o konkretnej [dostępności](product-resources.md#availability), wykonaj [**polecenie Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) i określ **Parametry AvailabilityId**, **CountryCode**, **ProductID** i **identyfikatora skuId** , aby pobrać szczegóły dostępności.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID}? Country = {Country-Code} http/1.1         |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać określoną dostępność przy użyciu identyfikatora dostępności.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| Identyfikator produktu             | ciąg   | Tak      | Ciąg w formacie GUID, który identyfikuje produkt.            |
| jednostka SKU — identyfikator                 | ciąg   | Tak      | Ciąg w formacie GUID, który identyfikuje jednostkę SKU.                |
| Identyfikator dostępności        | ciąg   | Tak      | Ciąg w formacie GUID, który identyfikuje dostępność.       |
| Kraj — kod           | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [dostępności](product-resources.md#availability) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Produkt nie został znaleziony.                                                                                    |
| 404                  | 400018       | Nie znaleziono jednostki SKU.                                                                                        |
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
