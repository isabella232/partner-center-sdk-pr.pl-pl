---
title: Pobieranie cen usług Microsoft Azure Partner Shared Services
description: How to get an Azure Rate Card with prices for Microsoft Azure Partner Shared Services (Jak uzyskać kartę stawki platformy Azure z cenami usług udostępnionych Microsoft Azure Partner).
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 33ee82bb966dee459cdeef6691c5e86eb7369fc7f76117f9360ac51d6cb3da22
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995819"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a>Pobieranie cen usług Microsoft Azure Partner Shared Services

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

How to get an Azure Rate Card with prices for Microsoft Azure Partner Shared Services (Jak uzyskać [kartę stawki platformy Azure](azure-rate-card-resources.md) z cenami usług udostępnionych Microsoft Azure Partner).

Ceny różnią się w zależności od rynku i waluty, a ten interfejs API uwzględnia lokalizację. Domyślnie interfejs API używa ustawień profilu partnera w języku Partner Center i języku przeglądarki, a te ustawienia można dostosowywać. Świadomość lokalizacji jest szczególnie przydatna, jeśli zarządzasz sprzedażą na wielu rynkach z jednego, scentralizowanego biura.

## <a name="example-code"></a>Przykładowy kod

## <a name="c"></a>C\#

Aby uzyskać kartę stawki platformy Azure, wywołaj metodę [**IAzureRateCard.GetShared,**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) aby zwrócić [**zasób AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) zawierający ceny platformy Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać kartę stawki platformy Azure, wywołaj funkcję **IAzureRateCard.getShared,** aby zwrócić szczegóły karty stawki zawierające ceny platformy Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać kartę platformy Azure, wykonaj polecenie [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) i określ parametr **SharedServices,** aby zwrócić szczegóły karty stawki zawierające ceny platformy Azure.

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                               |
|---------|---------------------------------------------------------------------------|
| **Pobierz** | *{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region} |

### <a name="uri-parameters"></a>Parametry URI

| Nazwa     | Typ   | Wymagane | Opis                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | ciąg | Nie       | Opcjonalny trzyliterowy kod ISO dla waluty, w której zostaną podane stawki zasobów (na przykład `EUR` ). Wartość domyślna to waluta skojarzona z rynek w profilu partnera. |
| region   | ciąg | Nie       | Opcjonalny dwuliterowy kod kraju/regionu ISO, który wskazuje rynek, na którym zakupiono ofertę (na przykład `FR` ). Wartość domyślna to kod kraju/regionu ustawiony w profilu partnera.        |

Jeśli opcjonalny nagłówek X-Locale jest uwzględniony w żądaniu, jego wartość określa język używany do określania szczegółów w odpowiedzi.

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli żądanie powiedzie się, zwraca [zasób karty stawki platformy Azure.](azure-rate-card-resources.md)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
