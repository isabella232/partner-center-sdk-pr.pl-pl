---
title: Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji
description: Jak uzyskać wszystkie informacje analityczne dotyczące subskrypcji.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 5c93f36491851be11c700388201443f2e951122e4129786abc3e064091605b8d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992606"
---
# <a name="get-all-subscription-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących subskrypcji

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

W tym artykule opisano sposób uzyskania wszystkich informacji analitycznych dotyczących subskrypcji dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|--------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

W poniższej tabeli wymieniono parametry opcjonalne i ich opisy:

| Parametr | Typ |  Opis |
|-----------|------|--------------|
| top (pierwsze) | int | Liczba wierszy danych do zwrócenia w żądaniu. Jeśli wartość nie zostanie określona, wartość maksymalna i wartość domyślna to `10000` . Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych. |
| Pomiń | int | Liczba wierszy do pominięcia w zapytaniu. Ten parametr umożliwia stronicować duże zestawy danych. Na przykład `top=10000` program i pobiera pierwsze `skip=0` 10000 wierszy danych i pobiera `top=10000` kolejne `skip=10000` 10000 wierszy danych. |
| filter | ciąg | Co najmniej jedna instrukcja, która filtruje wiersze w odpowiedzi. Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość skojarzoną z operatorem **`eq`** , lub dla niektórych **`ne`** **`contains`** pól. Instrukcje można łączyć przy użyciu **`and`** instrukcji lub **`or`** . Wartości ciągu muszą być otoczone pojedynczymi cudzysłowami w **parametrze filtru.** W poniższej sekcji znajduje się lista pól, które można filtrować, oraz operatorów obsługiwanych przez te pola. |
| aggregationLevel | ciąg | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może być jednym z następujących ciągów: **dzień,** **tydzień** lub **miesiąc**. Jeśli wartość nie zostanie określona, wartość domyślna to **dateRange**. Ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przekazywane jako część **parametru groupBy.** |
| Groupby | ciąg | Instrukcja, która stosuje agregację danych tylko do określonych pól. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [**zasobów**](partner-center-analytics-resources.md#subscription-resource) subskrypcji.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
