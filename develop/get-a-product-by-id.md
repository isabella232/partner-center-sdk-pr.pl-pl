---
title: Pobieranie produktu według identyfikatora
description: Pobiera określony zasób produktu przy użyciu identyfikatora produktu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767897"
---
# <a name="get-a-product-by-id"></a>Pobieranie produktu według identyfikatora

**Dotyczy**

- Centrum partnerskie

Pobiera określony zasób produktu przy użyciu identyfikatora produktu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator produktu.

## <a name="c"></a>C\#

Aby znaleźć konkretny produkt według identyfikatora, Użyj kolekcji **IAggregatePartner. Products** , wybierz kraj przy użyciu metody **ByCountry ()** , a następnie Wywołaj metodę **ById ()** . Na koniec Wywołaj metodę **Get ()** lub **GetAsync ()** w celu zwrócenia produktu.

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

Aby znaleźć konkretny produkt według identyfikatora, użyj funkcji **IAggregatePartner. getProducts** , wybierz kraj przy użyciu funkcji **byCountry ()** , a następnie wywołaj funkcję **byId ()** . Na koniec wywołaj funkcję **Get ()** w celu zwrócenia produktu.

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

Aby znaleźć konkretny produkt według identyfikatora, należy wykonać polecenie [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) i określić parametr **ProductID** . Parametr **CountryCode** jest opcjami, jeśli nie zostanie określony, zostanie użyty kraj skojarzony z odsprzedawcą.

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Products/{Product-ID}? Country = {Country} http/1.1  |

### <a name="uri-parameter"></a>Parametr URI

Aby uzyskać określony produkt, użyj następujących parametrów ścieżki.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| Identyfikator produktu             | ciąg   | Tak      | Ciąg identyfikujący produkt.                           |
| country                | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [produktu](product-resources.md#product) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | Produkt nie został znaleziony.                                                     |

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
