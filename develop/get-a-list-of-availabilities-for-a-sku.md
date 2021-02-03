---
title: Pobieranie listy dostępności dla jednostki SKU (według kraju)
description: Jak uzyskać zbiór podaży dla określonego produktu i jednostki SKU według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767957"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Pobieranie listy dostępności dla jednostki SKU (według kraju)

**Dotyczy:**

- Centrum partnerskie

W tym artykule opisano, jak uzyskać zbiór podaży w określonym kraju dla określonego produktu i jednostki SKU.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator produktu.

- Identyfikator jednostki SKU.

- Kraj.

## <a name="c"></a>C\#

Aby uzyskać listę [podaży](product-resources.md#availability) dla [jednostki SKU](product-resources.md#sku):

1. Postępuj zgodnie z instrukcjami w temacie [pobieranie jednostki SKU według identyfikatora](get-a-sku-by-id.md) , aby uzyskać interfejs dla operacji określonej jednostki SKU.

2. W interfejsie SKU wybierz właściwość **dostępność** , aby uzyskać interfejs z operacjami dla opcji dostępność.

3. Obowiązkowe Użyj metody **ByTargetSegment ()** , aby odfiltrować dostępność przez segment docelowy.

4. Wywoływanie **Get ()** lub **GetAsync ()** w celu pobrania kolekcji podaży dla tej jednostki SKU.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities? Country = {Country-code} &targetSegment = {Target-segment} http/1.1     |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę dostępność dla jednostki SKU.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| Identyfikator produktu             | ciąg   | Tak      | Ciąg identyfikujący produkt.                           |
| jednostka SKU — identyfikator                 | ciąg   | Tak      | Ciąg, który identyfikuje jednostkę SKU.                               |
| Kraj — kod           | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |
| segment docelowy         | ciąg   | Nie       | Ciąg, który identyfikuje segment docelowy używany do filtrowania. |
| reservationScope | ciąg   | Nie | Podczas wykonywania zapytania o listę dostępności dla jednostki SKU rezerwacji platformy Azure należy określić, `reservationScope=AzurePlan` Aby uzyskać listę dostępności, która ma zastosowanie do AzurePlan. Wyklucz ten parametr, aby uzyskać listę dostępności, która ma zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-examples"></a>Przykłady żądań

#### <a name="availabilities-for-sku-by-country"></a>Dostępność dla jednostki SKU według kraju

Postępuj zgodnie z tym przykładem, aby uzyskać listę podaży dla danej jednostki SKU według kraju:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>Dostępność na potrzeby rezerwacji maszyn wirtualnych (plan platformy Azure)

Postępuj zgodnie z tym przykładem, aby uzyskać listę podaży według kraju dla jednostek SKU rezerwacji maszyn wirtualnych platformy Azure. Ten przykład dotyczy jednostek SKU, które są stosowane do planów platformy Azure:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Dostępność dla rezerwacji maszyn wirtualnych dla subskrypcji Microsoft Azure (MS-AZR-0145P)

Postępuj zgodnie z tym przykładem, aby uzyskać listę dostępności według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [**dostępności**](product-resources.md#availability) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Nie można uzyskać dostępu do żądanego **targetSegment** .                                                     |

### <a name="response-example"></a>Przykład odpowiedzi

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
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
