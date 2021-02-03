---
title: Pobieranie listy jednostek SKU dla produktu (według kraju)
description: Możesz uzyskać i przefiltrować kolekcję jednostek SKU według kraju dla produktu przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767937"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>Pobieranie listy jednostek SKU dla produktu (według kraju)

**Dotyczy:**

- Centrum partnerskie

Możesz uzyskać kolekcję jednostek SKU dostępnych w danym kraju dla określonego produktu przy użyciu interfejsów API Centrum partnerskiego.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator produktu.

## <a name="c"></a>C\#

Aby uzyskać listę jednostek SKU produktu:

1. Pobierz interfejs dla operacji określonego produktu, wykonując kroki opisane w temacie [Uzyskiwanie produktu według identyfikatora](get-a-product-by-id.md).

2. Z poziomu interfejsu wybierz właściwość **SKU** , aby uzyskać interfejs z dostępnymi operacjami dla jednostek SKU.

3. Wywołaj metodę **Get ()** lub **GetAsync ()** , aby pobrać kolekcję dostępnych jednostek SKU dla produktu.

4. Obowiązkowe Wybierz zakres rezerwacji przy użyciu metody **ByReservationScope ()** .

5. Obowiązkowe Użyj metody **ByTargetSegment ()** , aby odfiltrować jednostki SKU według segmentu docelowego przed wywołaniem metody **Get ()** lub **GetAsync ()**.

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać listę jednostek SKU produktu:

1. Pobierz interfejs dla operacji określonego produktu, wykonując kroki opisane w temacie [Uzyskiwanie produktu według identyfikatora](get-a-product-by-id.md).

2. Z poziomu interfejsu wybierz funkcję **Getskus** , aby uzyskać interfejs z dostępnymi operacjami dla jednostek SKU.

3. Wywołaj funkcję **Get ()** , aby pobrać kolekcję dostępnych jednostek SKU dla produktu.

4. Obowiązkowe Użyj funkcji **byTargetSegment ()** , aby odfiltrować jednostki SKU według segmentu docelowego przed wywołaniem funkcji **Get ()** .

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać listę jednostek SKU produktu:

1. Wykonaj polecenie [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) .

2. Obowiązkowe Określ parametr **segmentu** , aby przefiltrować jednostki SKU według segmentu docelowego.

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}/SKUs? Country = {Country-code} &targetSegment = {Target-segment} http/1.1  |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę jednostek SKU dla produktu.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| Identyfikator produktu             | ciąg   | Tak      | Ciąg identyfikujący produkt.                           |
| Kraj — kod           | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |
| segment docelowy         | ciąg   | Nie       | Ciąg, który identyfikuje segment docelowy używany do filtrowania. |
| reservationScope | ciąg   | Nie | Podczas wykonywania zapytania o listę jednostek SKU dla produktu Azure Reservation należy określić, `reservationScope=AzurePlan` Aby uzyskać listę jednostek SKU, które mają zastosowanie do AzurePlan. Wyklucz ten parametr, aby uzyskać listę jednostek SKU dla produktów rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-examples"></a>Przykłady żądań

Pobierz listę jednostek SKU dla danego produktu:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Pobierz listę jednostek SKU dla produktu rezerwacji platformy Azure. Uwzględnij tylko jednostki SKU, które mają zastosowanie do planów platformy Azure, a nie Microsoft Azure (MS-AZR-0145P):

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Pobierz listę jednostek SKU dla produktu rezerwacji platformy Azure. Uwzględnij tylko jednostki SKU, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P), a nie planów platformy Azure:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [jednostki SKU](product-resources.md#sku) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Nie można uzyskać dostępu do żądanego targetSegment.                                                     |
| 404                  | 400013       | Nie znaleziono produktu nadrzędnego.                                                                         |

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
