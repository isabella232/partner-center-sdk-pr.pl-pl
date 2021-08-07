---
title: Pobieranie listy produktów (według kraju)
description: Możesz użyć zasobu Product, aby uzyskać kolekcję produktów według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6ec3a642006a100ef85c0af9eeddd9daf00cc1cd981eabd5dddb77e60e15111f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989444"
---
# <a name="get-a-list-of-products-by-country"></a>Pobieranie listy produktów (według kraju)

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Aby uzyskać kolekcję produktów dostępnych w danym kraju, można użyć następujących metod.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Kraj.

## <a name="c"></a>C\#

Aby uzyskać listę produktów:

1. Użyj **kolekcji IAggregatePartner.Products,** aby wybrać kraj przy użyciu **metody ByCountry().**

2. Wybierz widok wykazu przy użyciu **metody ByTargetView().**

3. (Opcjonalnie) Wybierz zakres rezerwacji przy **użyciu metody ByReservationScope().**

4. (Opcjonalnie) Wybierz segment docelowy przy użyciu **metody ByTargetSegment().**

5. Wywołaj **metodę Get()** lub **GetAsync(),** aby zwrócić kolekcję.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać listę produktów:

1. Użyj funkcji **IAggregatePartner.getProducts,** aby wybrać kraj przy użyciu **funkcji byCountry().**

2. Wybierz widok wykazu przy użyciu **funkcji byTargetView().**
3. (Opcjonalnie) Wybierz segment docelowy przy użyciu **funkcji byTargetSegment().**

4. Wywołaj **funkcję get(),** aby zwrócić kolekcję.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać listę produktów:

1. Wykonaj polecenie [**Get-PartnerProduct.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)

2. Wybierz wykaz, określając parametr **Catalog.**
3. (Opcjonalnie) Wybierz segment docelowy, określając **parametr Segment.**

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę produktów.

| Nazwa                   | Typ     | Wymagane | Opis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | ciąg   | Tak      | Identyfikator kraju/regionu.                                                  |
| targetView             | ciąg   | Tak      | Identyfikuje widok docelowy wykazu. Obsługiwane wartości to: <br/><br/>**Azure**, który zawiera wszystkie elementy platformy Azure<br/><br/>**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure<br/><br/>**AzureReservationsVM,** która obejmuje wszystkie elementy rezerwacji maszyny wirtualnej<br/><br/>**AzureReservationsSQL**, który zawiera wszystkie SQL elementów rezerwacji<br/><br/>**AzureReservationsCosmosDb,** która zawiera wszystkie Cosmos rezerwacji bazy danych<br/><br/>**MicrosoftAzure**, który zawiera elementy dla Microsoft Azure subskrypcji **(MS-AZR-0145P)** i planów platformy Azure<br/><br/>**OnlineServices**, która obejmuje wszystkie elementy usług online (w tym produkty platformy handlowej)<br/><br/>**Oprogramowanie**, które zawiera wszystkie elementy oprogramowania<br/><br/>**SoftwareSUSELinux**, który zawiera wszystkie elementy oprogramowania SUSE Linux<br/><br/>**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania<br/><br/>**SoftwareSubscriptions**, która obejmuje wszystkie elementy subskrypcji oprogramowania    |
| targetSegment          | ciąg   | Nie       | Identyfikuje segment docelowy. Widok dla różnych odbiorców docelowych. Obsługiwane wartości to: <br/><br/>**Handlowych**<br/>**Edukacji**<br/>**Rząd**<br/>**Non-profit**  |
| reservationScope (zakres rezerwacji) | ciąg   | Nie | Podczas wykonywania zapytania o listę produktów dla rezerwacji platformy Azure określ, aby uzyskać listę produktów, które `reservationScope=AzurePlan` mają zastosowanie do planów platformy Azure. Wyklucz ten parametr, aby uzyskać listę produktów dla rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure **(MS-AZR-0145P).**  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-examples"></a>Przykłady żądań

#### <a name="products-by-country"></a>Produkty według kraju

Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla subskrypcji Microsoft Azure (MS-AZR-0145P) i planów platformy Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Rezerwacje maszyn wirtualnych platformy Azure (plan platformy Azure)

Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według krajów dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do planów platformy Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Rezerwacje maszyn wirtualnych platformy Azure Microsoft Azure subskrypcji platformy Azure (MS-AZR-0145P)

Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji usługi Microsoft Azure (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia treść odpowiedzi zawiera kolekcję [**zasobów**](product-resources.md#product) produktu.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Dostęp do żądanego obiektu targetSegment jest niedozwolone.                                                     |
| 403                  | 400036       | Dostęp do żądanego obiektu targetView jest niedozwolone.                                                        |

### <a name="response-example"></a>Przykład odpowiedzi

```http
{
    "totalCount": 19,
    "items": [
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
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
