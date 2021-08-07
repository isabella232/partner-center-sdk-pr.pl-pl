---
title: Sprawdzanie spisu
description: Dowiedz się, jak Partner Center interfejsów API do sprawdzania spisu określonego zestawu elementów katalogu. Można to zrobić, aby zidentyfikować produkty lub jednostki SKU klienta.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de931c7dd89f94b6be8fdaf0ad79c8faee268267c35a2c0f8e38d36b97842f3f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992113"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Sprawdzanie spisu elementów wykazu przy użyciu Partner Center API

Jak sprawdzić spis dla określonego zestawu elementów katalogu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Co najmniej jeden identyfikator produktu. Opcjonalnie można również określić identyfikatory SKU.

- Wszelkie dodatkowe konteksty potrzebne do zweryfikowania spisu sku, do których odwołują się podane identyfikatory produktów/SKU. Te wymagania mogą się różnić w zależności od [](product-resources.md#sku) typu produktu/sku i można je określić na podstawie właściwości **InventoryVariables tej sku.**

## <a name="c"></a>C\#

Aby sprawdzić spis, skonstruuj obiekt [InventoryCheckRequest](product-resources.md#inventorycheckrequest) przy użyciu obiektu [InventoryItem](product-resources.md#inventoryitem) dla każdego elementu do sprawdzenia. Następnie użyj metody dostępu **IAggregatePartner.Extensions,** określ jej zakres w dół do opcji **Product,** a następnie wybierz kraj przy użyciu **metody ByCountry().** Na koniec wywołaj **metodę CheckInventory() przy** użyciu **obiektu InventoryCheckRequest.**

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1                        |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby sprawdzić spis.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| kod kraju           | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Szczegóły żądania spisu składające się z zasobu [InventoryCheckRequest](product-resources.md#inventorycheckrequest) zawierającego co najmniej jeden [zasób InventoryItem.](product-resources.md#inventoryitem)

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję obiektów [InventoryItem](product-resources.md#inventoryitem) wypełnionych szczegółami ograniczeń, jeśli mają zastosowanie.

>[!NOTE]
>Jeśli element wejściowy InventoryItem reprezentuje element, który nie można odnaleźć w wykazie, nie zostanie uwzględniony w kolekcji wyjściowej.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
