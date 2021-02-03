---
title: Pobieranie listy dostępności dla jednostki SKU (według klientów)
description: Możesz uzyskać kolekcję podaży dla określonego produktu i jednostki SKU przez klienta przy użyciu identyfikatorów klienta, produktu i jednostki SKU.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5f4067916fea911963182954eed77f4e230e79d6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767958"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a>Pobieranie listy dostępności dla jednostki SKU (według klientów)

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Korzystając z poniższych metod, można uzyskać kolekcję dostępności dla określonego produktu i jednostki SKU dostępnego dla danego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator produktu (**Identyfikator produktu**).

- Identyfikator jednostki SKU (**SKU-ID**).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/SKUs/{SKU-ID} http/1.1 |

### <a name="request-uri-parameters"></a>Parametry identyfikatora URI żądania

| Nazwa               | Typ | Wymagane | Opis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| Identyfikator dzierżawy klienta | GUID | Tak | Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta. |
| Identyfikator produktu | ciąg | Tak | Ciąg identyfikujący produkt. |
| jednostka SKU — identyfikator | ciąg | Tak | Ciąg, który identyfikuje jednostkę SKU. |

### <a name="request-header"></a>Nagłówek żądania

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>Odpowiedź REST

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP | Kod błędu | Opis |
|------------------|------------|-------------|
| 404 | 400013 | Nie znaleziono produktu nadrzędnego. |

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
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
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
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
```
