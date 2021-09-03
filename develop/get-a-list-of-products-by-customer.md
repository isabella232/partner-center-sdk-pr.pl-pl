---
title: Pobieranie listy produktów (według klientów)
description: Identyfikator klienta umożliwia pobieranie kolekcji produktów według klienta.
ms.assetid: ''
ms.date: 02/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1f3f38271b97ceba143c819ec03758ad1b9c0d3b
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2021
ms.locfileid: "123455765"
---
# <a name="get-a-list-of-products-by-customer"></a>Pobieranie listy produktów (według klientów)

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center dla Microsoft Cloud for US Government

Aby uzyskać kolekcję produktów dla istniejącego klienta, można użyć następujących metod.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1 |

#### <a name="request-uri-parameters"></a>Parametry URI żądania

| Nazwa               | Typ | Wymagane | Opis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | GUID | Tak | Wartość jest identyfikatorem **customer-tenant-id** w formacie identyfikatora GUID, który jest identyfikatorem umożliwiającym określenie klienta. |
| **targetView** | ciąg | Tak | Określa widok docelowy katalogu. Obsługiwane wartości to: <br/><br/>**Azure**, który zawiera wszystkie elementy platformy Azure<br/><br/>**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure<br/><br/>**AzureReservationsVM,** która zawiera wszystkie elementy rezerwacji maszyny wirtualnej<br/><br/>**AzureReservationsSQL**, który zawiera wszystkie SQL elementów rezerwacji<br/><br/>**AzureReservationsCosmosDb,** która zawiera wszystkie Cosmos rezerwacji bazy danych<br/><br/>**MicrosoftAzure**, który zawiera elementy dla Microsoft Azure subskrypcji **(MS-AZR-0145P)** i planów platformy Azure<br/><br/>**OnlineServices**, która obejmuje wszystkie elementy usług online. Ten element targetView obejmuje komercyjną platformę handlową, trandycyjną usługę opartą na licencjach i nowe usługi oparte na licencjach handlowych<br/><br/>**Oprogramowanie**, które zawiera wszystkie elementy oprogramowania<br/><br/>**SoftwareSUSELinux**, który zawiera wszystkie elementy oprogramowania SUSE Linux<br/><br/>**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania<br/><br/>**SoftwareSubscriptions**, która obejmuje wszystkie elementy subskrypcji oprogramowania  |

### <a name="request-header"></a>Nagłówek żądania

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

Zażądaj listy produktów opartych na użyciu platformy Azure dostępnych dla danego klienta. Produkty dla obu Microsoft Azure (MS-AZR-0145P) i planów platformy Azure będą zwracane dla klientów w chmurze publicznej:

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```
#### <a name="new-commerce-license-based-services"></a>Nowe usługi oparte na licencjach handlowych

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview

Postępuj zgodnie z tym przykładem, aby uzyskać listę produktów według krajów dla nowych usług opartych na licencjach handlowych w ramach nowego doświadczenia handlowego w wersji Technical Preview. Nowe usługi oparte na licencjach handlowych będą identyfikowane za pomocą wartości id i displayNames klasy **OnlineServicesNCE.** Zobacz przykład odpowiedzi poniżej.

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=OnlineServices HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpowiedź REST

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP | Kod błędu   | Opis                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | Dostęp do żądanego obiektu targetView nie jest dozwolony. |

### <a name="response-example-for-microsoft-azure-and-azure-plan"></a>Przykład odpowiedzi dla Microsoft Azure i planu platformy Azure

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
### <a name="response-example-for-new-commerce-license-based-services"></a>Przykład odpowiedzi dla nowych usług opartych na licencjach handlowych

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview

```http
{
  "totalCount": 19,
  "items": [{
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
    },
    ...
  ],
  "links": {
    "self": {
      "uri": "/products?country=US&targetView=OnlineServices",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
