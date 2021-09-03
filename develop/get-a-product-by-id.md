---
title: Pobieranie produktu według identyfikatora
description: Pobiera określony zasób produktu przy użyciu identyfikatora produktu.
ms.date: 02/16/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 95821b0f3678d38c75e2f684f7ad629b82f9b43b
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456107"
---
# <a name="get-a-product-by-id"></a>Pobieranie produktu według identyfikatora

Pobiera określony zasób produktu przy użyciu identyfikatora produktu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator produktu.

## <a name="c"></a>C\#

Aby znaleźć konkretny produkt według identyfikatora, użyj kolekcji **IAggregatePartner.Products,** wybierz kraj przy użyciu metody **ByCountry(),** a następnie wywołaj metodę **ById().** Na koniec wywołaj **metodę Get()** **lub GetAsync(),** aby zwrócić produkt.

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

Aby znaleźć konkretny produkt według identyfikatora, użyj funkcji **IAggregatePartner.getProducts,** wybierz kraj przy użyciu funkcji **byCountry(),** a następnie wywołaj funkcję **byId().** Na koniec wywołaj **funkcję get(),** aby zwrócić produkt.

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

Aby znaleźć konkretny produkt według identyfikatora, wykonaj polecenie [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) i określ **parametr ProductId.** Parametr **CountryCode** jest opcjami. Jeśli nie zostanie określony, zostanie użyty kraj skojarzony z odsprzedawcą.

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **POBIERZ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{identyfikator-produktu}?country={country} HTTP/1.1  |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów ścieżki, aby uzyskać określony produkt.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| identyfikator produktu             | ciąg   | Tak      | Ciąg identyfikujący produkt.                           |
| country                | ciąg   | Tak      | Identyfikator kraju/regionu.                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób](product-resources.md#product) Product.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | Nie znaleziono produktu.                                                     |

### <a name="response-example-for-azure-vm-reservation-azure-plan"></a>Przykład odpowiedzi dla rezerwacji maszyny wirtualnej platformy Azure (plan platformy Azure)

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
### <a name="response-example-for-new-commerce-license-based-product"></a>Przykład odpowiedzi dla nowego produktu opartego na licencjach handlowych

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview

```http
{
    "id": "CFQ7TTC0LH18",
    "title": "Microsoft 365 Business Basic",
    "description": "Best for businesses that need professional email, cloud file storage, and online meetings & chat. Desktop versions of Office apps like Excel, Word, and PowerPoint not included. For businesses with up to 300 employees.",
    "productType": {
        "id": "OnlineServicesNCE",
        "displayName": "OnlineServicesNCE"
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/CFQ7TTC0LH18/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
        "uri": "/products/CFQ7TTC0LH18?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
