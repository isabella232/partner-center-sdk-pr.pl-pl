---
title: Pobieranie listy produktów (według kraju)
description: Możesz użyć zasobu produktu, aby uzyskać zbiór produktów według kraju klienta.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768173"
---
# <a name="get-a-list-of-products-by-country"></a>Pobieranie listy produktów (według kraju)

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Poniższe metody umożliwiają pobranie kolekcji produktów dostępnych w danym kraju.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Kraj.

## <a name="c"></a>C\#

Aby uzyskać listę produktów:

1. Użyj kolekcji **IAggregatePartner. Products** , aby wybrać kraj przy użyciu metody **ByCountry ()** .

2. Wybierz widok wykazu przy użyciu metody **ByTargetView ()** .

3. Obowiązkowe Wybierz zakres rezerwacji przy użyciu metody **ByReservationScope ()** .

4. Obowiązkowe Wybierz segment docelowy przy użyciu metody **ByTargetSegment ()** .

5. Wywołaj metodę **Get ()** lub **GetAsync ()** w celu zwrócenia kolekcji.

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

1. Użyj funkcji **IAggregatePartner. getProducts** , aby wybrać kraj przy użyciu funkcji **byCountry ()** .

2. Wybierz widok wykazu przy użyciu funkcji **byTargetView ()** .
3. Obowiązkowe Wybierz segment docelowy przy użyciu funkcji **byTargetSegment ()** .

4. Wywołaj funkcję **Get ()** w celu zwrócenia kolekcji.

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

1. Wykonaj polecenie [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .

2. Wybierz katalog, określając parametr **wykazu** .
3. Obowiązkowe Wybierz segment docelowy, określając parametr **segmentu** .

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Products? Country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następującej ścieżki i parametrów zapytania, aby uzyskać listę produktów.

| Nazwa                   | Typ     | Wymagane | Opis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | ciąg   | Tak      | Identyfikator kraju/regionu.                                                  |
| targetView             | ciąg   | Tak      | Identyfikuje widok docelowy wykazu. Obsługiwane są następujące wartości: <br/><br/>**Azure**, w tym wszystkie elementy platformy Azure<br/><br/>**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure<br/><br/>**AzureReservationsVM**, w tym wszystkie elementy rezerwacji maszyny wirtualnej (VM)<br/><br/>**AzureReservationsSQL**, która obejmuje wszystkie elementy rezerwacji SQL<br/><br/>**AzureReservationsCosmosDb**, która obejmuje wszystkie elementy zastrzeżeń bazy danych Cosmos<br/><br/>**MicrosoftAzure**, w tym elementy subskrypcji Microsoft Azure (**MS-AZR-0145P**) i plany platformy Azure<br/><br/>**OnlineServices**, która obejmuje wszystkie elementy usługi online (w tym komercyjne produkty Marketplace)<br/><br/>**Oprogramowanie**, które obejmuje wszystkie elementy oprogramowania<br/><br/>**SoftwareSUSELinux**, który obejmuje wszystkie elementy oprogramowania SUSE Linux<br/><br/>**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania<br/><br/>**SoftwareSubscriptions** obejmujący wszystkie elementy subskrypcji oprogramowania    |
| targetSegment          | ciąg   | Nie       | Identyfikuje segment docelowy. Widok dla różnych docelowych odbiorców. Obsługiwane są następujące wartości: <br/><br/>**lekki**<br/>**oświat**<br/>**Zarządowi**<br/>**non profit**  |
| reservationScope | ciąg   | Nie | Podczas wykonywania zapytania dotyczącego listy produktów dla Azure Reservations należy określić, `reservationScope=AzurePlan` Aby uzyskać listę produktów, które mają zastosowanie do planów platformy Azure. Wyklucz ten parametr, aby uzyskać listę produktów dla rezerwacji platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (**MS-AZR-0145P**).  |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do planów platformy Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Rezerwacje maszyn wirtualnych platformy Azure dla subskrypcji Microsoft Azure (MS-AZR-0145P)

Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według kraju dla rezerwacji maszyn wirtualnych platformy Azure, które mają zastosowanie do subskrypcji Microsoft Azure (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [**produktu**](product-resources.md#product) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Nie można uzyskać dostępu do żądanego targetSegment.                                                     |
| 403                  | 400036       | Nie można uzyskać dostępu do żądanego targetView.                                                        |

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
