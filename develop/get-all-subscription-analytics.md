---
title: Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji
description: Jak uzyskać wszystkie informacje o usłudze Subscription Analytics.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767710"
---
# <a name="get-all-subscription-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano, jak uzyskać wszystkie informacje o usłudze Subscription Analytics dla swoich klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|--------|-------------|
| **Pobierz** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/subscriptions http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

W poniższej tabeli wymieniono parametry opcjonalne i ich opisy:

| Parametr | Typ |  Opis |
|-----------|------|--------------|
| top (pierwsze) | int | Liczba wierszy danych do zwrócenia w żądaniu. Jeśli wartość nie jest określona, wartość maksymalna i wartość domyślna to `10000` . Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych. |
| Pomiń | int | Liczba wierszy do pominięcia w zapytaniu. Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych. Na przykład program `top=10000` `skip=0` pobiera pierwsze 10000 wierszy danych `top=10000` i `skip=10000` pobiera następne 10000 wierszy danych. |
| filter | ciąg | Jedna lub więcej instrukcji, które filtrują wiersze w odpowiedzi. Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość, która jest skojarzona z **`eq`** , **`ne`** lub dla niektórych pól, **`contains`** operatora. Instrukcje można łączyć przy użyciu **`and`** lub **`or`** . Wartości ciągu muszą być ujęte w pojedyncze cudzysłowy w parametrze **Filter** . W poniższej sekcji znajduje się lista pól, które można filtrować i operatory, które są obsługiwane przez te pola. |
| aggregationLevel | ciąg | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może to być jeden z następujących ciągów: **dzień**, **tydzień** lub **miesiąc**. Jeśli wartość nie jest określona, wartością domyślną jest **dateRange**. Ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przesyłane jako część parametru **GroupBy** . |
| groupBy | ciąg | Instrukcja, która stosuje agregację danych tylko do określonych pól. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [**subskrypcji**](partner-center-analytics-resources.md#subscription-resource) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>Zobacz też

- [Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
