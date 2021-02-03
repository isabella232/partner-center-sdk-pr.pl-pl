---
title: Pobieranie listy produktów (według klientów)
description: Możesz użyć identyfikatora klienta, aby uzyskać kolekcję produktów przez klienta.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 98a099c458535123f675c6452db950b087b9f387
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768174"
---
# <a name="get-a-list-of-products-by-customer"></a>Pobieranie listy produktów (według klientów)

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Poniższe metody umożliwiają pobranie kolekcji produktów dla istniejącego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Products? targetViewd = {targetView} http/1.1 |

#### <a name="request-uri-parameters"></a>Parametry identyfikatora URI żądania

| Nazwa               | Typ | Wymagane | Opis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | GUID | Tak | Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta. |
| **targetView** | ciąg | Tak | Identyfikuje widok docelowy wykazu. Obsługiwane są następujące wartości: <br/><br/>**Azure**, w tym wszystkie elementy platformy Azure<br/><br/>**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure<br/><br/>**AzureReservationsVM**, w tym wszystkie elementy rezerwacji maszyny wirtualnej (VM)<br/><br/>**AzureReservationsSQL**, która obejmuje wszystkie elementy rezerwacji SQL<br/><br/>**AzureReservationsCosmosDb**, która obejmuje wszystkie elementy zastrzeżeń bazy danych Cosmos<br/><br/>**MicrosoftAzure**, w tym elementy subskrypcji Microsoft Azure (**MS-AZR-0145P**) i plany platformy Azure<br/><br/>**OnlineServices** obejmujący wszystkie elementy usługi online, w tym komercyjne produkty Marketplace<br/><br/>**Oprogramowanie**, które obejmuje wszystkie elementy oprogramowania<br/><br/>**SoftwareSUSELinux**, który obejmuje wszystkie elementy oprogramowania SUSE Linux<br/><br/>**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania<br/><br/>**SoftwareSubscriptions** obejmujący wszystkie elementy subskrypcji oprogramowania  |

### <a name="request-header"></a>Nagłówek żądania

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

Żądanie listy produktów opartych na użyciu platformy Azure dostępnych dla danego klienta. Produkty dla obu Microsoft Azure (MS-AZR-0145P) i plany platformy Azure zostaną zwrócone dla klientów w chmurze publicznej:

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>Odpowiedź REST

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP | Kod błędu   | Opis                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | Nie można uzyskać dostępu do żądanego targetView. |

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
