---
title: Pobieranie usługi Subscription Analytics pogrupowane według dat lub warunków
description: Jak uzyskać informacje o usłudze Subscription Analytics pogrupowane według dat lub warunków.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767909"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Pobieranie usługi Subscription Analytics pogrupowane według dat lub warunków

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać informacje o usłudze Subscription Analytics dla klientów pogrupowane według dat lub warunków.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|--------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/subscriptions? GroupBy = {groupby_queries} |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj poniższych wymaganych parametrów ścieżki, aby zidentyfikować organizację i zgrupować wyniki.

| Nazwa | Typ | Wymagane | Opis |
|------|------|----------|-------------|
| groupby_queries | pary ciągów i dateTime | Tak | Warunki i daty filtrowania wyniku. |

### <a name="groupby-syntax"></a>Składnia GroupBy

Parametry Group by muszą składać się z serii oddzielonych przecinkami, wartości pól.

Niezakodowany przykład wygląda następująco:

```http
?groupby=termField1,dateField1,termField2
```

W poniższej tabeli przedstawiono listę obsługiwanych pól dla Grupuj według.

| Pole | Typ | Opis |
|-------|------|-------------|
| customerTenantId | ciąg | Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje dzierżawcę klienta. |
| customerName | ciąg | Nazwa klienta. |
| customerMarket | ciąg | Kraj/region, w którym klient wykonuje działalność. |
| identyfikator | ciąg | Ciąg w formacie GUID, który identyfikuje subskrypcję. |
| status | ciąg | Stan subskrypcji. Obsługiwane wartości to: "ACTIVE", "SUSPENDed" lub "unsupportedd". |
| productName | ciąg | Nazwa produktu. |
| SubscriptionType | ciąg | Typ subskrypcji. Uwaga: w tym polu jest uwzględniana wielkość liter. Obsługiwane są następujące wartości: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Wartość logiczna | Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie. |
| partnerId  | ciąg | IDENTYFIKATOR MPN. Dla bezpośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN partnera. W odniesieniu do pośredniego odsprzedawcy ten parametr będzie IDENTYFIKATORem MPN pośredniego odsprzedawcy. |
| friendlyName | ciąg | Nazwa subskrypcji. |
| partnerName | ciąg | Nazwa partnera, dla którego została zakupiona subskrypcja |
| providerName | ciąg | Gdy transakcja subskrypcyjna dotyczy pośredniego odsprzedawcy, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.
| creationDate | ciąg w formacie daty i godziny czasu UTC | Data utworzenia subskrypcji. |
| effectiveStartDate | ciąg w formacie daty i godziny czasu UTC | Data rozpoczęcia subskrypcji. |
| commitmentEndDate | ciąg w formacie daty i godziny czasu UTC | Data zakończenia subskrypcji. |
| currentStateEndDate | ciąg w formacie daty i godziny czasu UTC | Data zmiany bieżącego stanu subskrypcji. |
| trialToPaidConversionDate | ciąg w formacie daty i godziny czasu UTC | Data konwersji subskrypcji z wersji próbnej na płatne. Wartość domyślna to null. |
| trialStartDate | ciąg w formacie daty i godziny czasu UTC | Data rozpoczęcia okresu próbnego dla subskrypcji. Wartość domyślna to null. |
| lastUsageDate | ciąg w formacie daty i godziny czasu UTC | Data ostatniego użycia subskrypcji. Wartość domyślna to null. |
| deprovisionedDate | ciąg w formacie daty i godziny czasu UTC | Data anulowania aprowizacji subskrypcji. Wartość domyślna to null. |
| lastRenewalDate | ciąg w formacie daty i godziny czasu UTC | Data ostatniego odnowienia subskrypcji. Wartość domyślna to null. |

### <a name="filter-fields"></a>Pola filtru

W poniższej tabeli wymieniono opcjonalne pola filtrów i ich opisy:

| Pole | Typ |  Opis |
|-------|------|--------------|
| top (pierwsze) | int | Liczba wierszy danych do zwrócenia w żądaniu. Jeśli wartość nie jest określona, wartość maksymalna i wartość domyślna to 10000. Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych. |
| Pomiń | int | Liczba wierszy do pominięcia w zapytaniu. Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych. Na przykład: Top = 10000 i Skip = 0 pobiera pierwsze 10000 wierszy danych, Top = 10000 i Skip = 10000 pobiera następne 10000 wierszy danych. |
| filter | ciąg | Jedna lub więcej instrukcji, które filtrują wiersze w odpowiedzi. Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość, która jest skojarzona z **`eq`** , **`ne`** lub dla niektórych pól, **`contains`** operatora. Instrukcje można łączyć przy użyciu **`and`** lub **`or`** . Wartości ciągu muszą być ujęte w pojedyncze cudzysłowy w parametrze Filter. W poniższej sekcji znajduje się lista pól, które można filtrować i operatory, które są obsługiwane przez te pola. |
| aggregationLevel | ciąg | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może to być jeden z następujących ciągów: **dzień**, **tydzień** lub **miesiąc**. Jeśli wartość nie jest określona, wartością domyślną jest **dateRange**. **Uwaga**: ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przesyłane jako część parametru GroupBy. |
| groupBy | ciąg | Instrukcja, która stosuje agregację danych tylko do określonych pól. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) pogrupowanych według określonych warunków i dat.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>Zobacz też

[Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
