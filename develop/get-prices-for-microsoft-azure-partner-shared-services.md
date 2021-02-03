---
title: Pobieranie cen usług Microsoft Azure Partner Shared Services
description: Jak uzyskać kartę stawki platformy Azure z cenami usług udostępnionych Microsoft Azure partnerskich.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cd396c35b6b89de4d0f092ba4da738a2ed0ac633
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768478"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a>Pobieranie cen usług Microsoft Azure Partner Shared Services

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać [kartę stawki platformy Azure](azure-rate-card-resources.md) z cenami usług udostępnionych Microsoft Azure partnerskich.

Ceny różnią się w zależności od rynku i waluty, a ten interfejs API przyjmuje lokalizację. Domyślnie interfejs API używa ustawień profilu partnera w centrum partnerskim i w języku przeglądarki. te ustawienia można dostosować. Rozpoznawanie lokalizacji jest szczególnie istotne w przypadku zarządzania sprzedażą na wielu rynkach z jednego, scentralizowanego biura.

## <a name="example-code"></a>Przykładowy kod

## <a name="c"></a>C\#

Aby uzyskać kartę stawki platformy Azure, wywołaj metodę [**IAzureRateCard. Getshared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) w celu zwrócenia zasobu [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) zawierającego ceny platformy Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać kartę stawki platformy Azure, wywołaj funkcję **IAzureRateCard. Getshared** , aby zwracała szczegóły karty szybkości zawierającej ceny platformy Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać kartę platformy Azure, wykonaj polecenie [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) i określ parametr **SharedServices** w celu zwrócenia szczegółów karty częstotliwość, która zawiera ceny platformy Azure.

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                               |
|---------|---------------------------------------------------------------------------|
| **Pobierz** | *{baseURL}*/V1/ratecards/Azure-Shared? Currency = {currency} &region = {Region} |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

| Nazwa     | Typ   | Wymagane | Opis                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | ciąg | Nie       | Opcjonalny trzyliterowy kod ISO dla waluty, w której zostaną podane stawki zasobów (na przykład `EUR` ). Wartość domyślna to waluta skojarzona z rynkiem w profilu partnera. |
| region   | ciąg | Nie       | Opcjonalny dwuliterowy kod kraju/regionu w formacie ISO, który wskazuje rynek zakupu oferty (na przykład `FR` ). Wartość domyślna to kod kraju/regionu ustawiony w profilu partnera.        |

Jeśli opcjonalny nagłówek X-locale zostanie uwzględniony w żądaniu, jego wartość określa język używany dla szczegółów odpowiedzi.

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli żądanie zakończy się pomyślnie, zwraca zasób [karty usługi Azure rate](azure-rate-card-resources.md) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
