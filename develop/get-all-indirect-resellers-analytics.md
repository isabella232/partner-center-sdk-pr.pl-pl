---
title: Pobieranie wszystkich informacji analitycznych dotyczących odsprzedawców pośrednich
description: Jak uzyskać wszystkie pośrednie informacje o analizie odsprzedawcy.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 9f9c030278ba8fef9090f7be89064ac6054129ef
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768170"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących odsprzedawców pośrednich

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać informacje o analizie pośrednich odsprzedawcaów dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/indirectresellers http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

| Parametr                             | Typ     | Opis                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | ciąg   | Identyfikator dzierżawy partnera, dla którego chcesz pobrać pośrednie dane odsprzedawcy. |
| identyfikator                                    | ciąg   | Pośredni identyfikator odsprzedawcy                                                                 |
| name                                  | ciąg   | Nazwa partnera, dla którego mają zostać pobrane pośrednie dane odsprzedawcy.      |
| rynek                                | ciąg   | Rynek partnera, dla którego chcesz pobrać pośrednie dane odsprzedawcy.    |
| firstSubscriptionCreationDate         | ciąg w formacie daty i godziny czasu UTC  | Data utworzenia pierwszej subskrypcji, na podstawie której chcesz pobrać pośrednie dane odsprzedawcy.  |
| latestSubscriptionCreationDate        | ciąg w formacie daty i godziny czasu UTC  | Data utworzenia najnowszej subskrypcji.                 |
| firstSubscriptionEndDate              | ciąg w formacie daty i godziny czasu UTC  | Po raz pierwszy subskrypcja została zakończona.                        |
| latestSubscriptionEndDate             | ciąg w formacie daty i godziny czasu UTC  | Najnowsza Data zakończenia subskrypcji.                  |
| firstSubscriptionSuspendedDate        | ciąg daty i godziny w formacie UTC         | Po raz pierwszy subskrypcja została zawieszona.                    |
| latestSubscriptionSuspendedDate       | ciąg w formacie daty i godziny czasu UTC  | Najnowsza Data wstrzymania subskrypcji.              |
| firstSubscriptionDeprovisionedDate    | ciąg w formacie daty i godziny czasu UTC  | Po raz pierwszy subskrypcja została anulowana.                |
| latestSubscriptionDeprovisionedDate   | ciąg w formacie daty i godziny czasu UTC  | Najnowsza data anulowania aprowizacji subskrypcji.          |
| subscriptionCount                     | double   | Liczba subskrypcji dla wszystkich dodanych odsprzedawcy                                     |
| licenseCount                          | double   | Liczba licencji dla wszystkich dodanych odsprzedawcy.                                         |
| indirectResellerCount                 | double   | Liczba pośrednich odsprzedawcy                                                             |
|  top (pierwsze)                                  | ciąg   | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli zapytanie zawiera więcej wierszy, treść odpowiedzi obejmuje następny link, którego można użyć do żądania następnej strony danych.  |
| Pomiń                                  | int      | Liczba wierszy do pominięcia w zapytaniu. Użyj tego parametru, aby uzyskać stronę z dużymi zestawami danych. Na przykład program **`top=10000 and skip=0`** Pobiera pierwsze 10000 wierszy danych, **`top=10000 and skip=10000`** pobiera następne 10000 wierszy danych i tak dalej.              |
| filter                                | ciąg   | Parametr *Filter* żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z **`eq`** **`ne`** operatorami or, a instrukcje można łączyć za pomocą **`and`** lub **`or`** . Można określić następujące pola:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Nazwa*<br/>                *rynek*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Przykład:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Przykład:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | ciąg    | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może to być jeden z następujących ciągów: &quot; dzień &quot; , &quot; tydzień &quot; lub &quot; miesiąc &quot; . Jeśli nie zostanie określony, wartością domyślną jest &quot; dzień &quot; .<br/><br/>                                 `aggregationLevel` nie jest obsługiwane bez `aggregationLevel` . `aggregationLevel` dotyczy wszystkich **datefields** obecnych w `aggregationLevel`                         |
| OrderBy                              | ciąg    | Instrukcja, która porządkuje wartości danych wynikowych dla każdej instalacji. Składnia jest następująca: `...&orderby=field[order],field [order],...` Parametr pola może być jednym z następujących ciągów:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Nazwij&quot;<br/>                &quot;rynek&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   Parametr *Order* jest opcjonalny i może mieć wartość `asc` or `desc` ;, aby określić kolejność rosnącą lub malejącą dla każdego pola. Wartość domyślna to `asc`.<br/><br/>    **Przykład:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| GroupBy                              | ciąg    | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Nazwa*<br/>                *rynek*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 Zwrócone wiersze danych zawierają pola określone w `groupby` klauzuli oraz następujące pola:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            `groupby`Parametru można użyć z `aggregationLevel` parametrem.<br/><br/>            **Przykład:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [pośrednich zasobów odsprzedawcy](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>Zobacz też

- [Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
