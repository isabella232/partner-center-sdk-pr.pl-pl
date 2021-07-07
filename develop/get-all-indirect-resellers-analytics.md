---
title: Pobieranie wszystkich informacji analitycznych dotyczących odsprzedawców pośrednich
description: Jak uzyskać informacje analityczne dla wszystkich odsprzedawców pośrednich.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 4252f5fcbbcb038f382408074c8fd6ede3fd1f58
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760746"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących odsprzedawców pośrednich

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak uzyskać informacje analityczne dla wszystkich odsprzedawców pośrednich dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

| Parametr                             | Typ     | Opis                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | ciąg   | Identyfikator dzierżawy partnera, dla którego chcesz pobrać dane odsprzedawców pośrednich. |
| identyfikator                                    | ciąg   | Identyfikator odsprzedawcy pośredniego                                                                 |
| name                                  | ciąg   | Nazwa partnera, dla którego chcesz pobrać dane odsprzedawców pośrednich.      |
| rynek                                | ciąg   | Rynek partnera, dla którego chcesz pobrać dane odsprzedawców pośrednich.    |
| firstSubscriptionCreationDate         | ciąg w formacie daty i czasu UTC  | Data utworzenia pierwszej subskrypcji, na podstawie której chcesz pobrać dane odsprzedawców pośrednich.  |
| latestSubscriptionCreationDate        | ciąg w formacie daty i czasu UTC  | Data utworzenia najnowszej subskrypcji.                 |
| firstSubscriptionEndDate              | ciąg w formacie daty i czasu UTC  | Po raz pierwszy subskrypcja została zakończona.                        |
| latestSubscriptionEndDate             | ciąg w formacie daty i czasu UTC  | Najpóźniejsza data zakończenia dowolnej subskrypcji.                  |
| firstSubscriptionSuspendedDate        | string in UTC date time (ciąg w czasie UTC)         | Po raz pierwszy wstrzymano każdą subskrypcję.                    |
| latestSubscriptionSuspendedDate       | ciąg w formacie daty i czasu UTC  | Najpóźniejsza data, kiedy jakakolwiek subskrypcja została wstrzymana.              |
| firstSubscriptionDeprovisionedDate    | ciąg w formacie daty i czasu UTC  | Po raz pierwszy anulowano aprowizę dowolnej subskrypcji.                |
| latestSubscriptionDeprovisionedDate   | ciąg w formacie daty i czasu UTC  | Najpóźniejsza data coprowizowana dowolnej subskrypcji.          |
| subscriptionCount                     | double   | Liczba subskrypcji dla wszystkich odsprzedawców z dodaną wartością                                     |
| licenseCount                          | double   | Liczba licencji dla wszystkich odsprzedawców z dodaną wartością.                                         |
| indirectResellerCount                 | double   | Liczba odsprzedawców pośrednich                                                             |
|  top (pierwsze)                                  | ciąg   | Liczba wierszy danych do zwrócenia w żądaniu. Wartość maksymalna i wartość domyślna, jeśli nie zostanie określona, to 10000. Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych.  |
| Pomiń                                  | int      | Liczba wierszy do pominięcia w zapytaniu. Ten parametr umożliwia stronicować duże zestawy danych. Na przykład **`top=10000 and skip=0`** program pobiera pierwsze 10 000 wierszy danych, pobiera następne **`top=10000 and skip=10000`** 10000 wierszy danych i tak dalej.              |
| filter                                | ciąg   | Parametr *filter* żądania zawiera co najmniej jedną instrukcje filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami lub , a instrukcje mogą być łączone przy **`eq`** **`ne`** użyciu lub **`and`** **`or`** . Można określić następujące pola:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Nazwa*<br/>                *rynek*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Przykład:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Przykład:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | ciąg    | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może być jednym z następujących ciągów: &quot; &quot; dzień, &quot; &quot; tydzień lub &quot; miesiąc &quot; . Jeśli nie zostanie on nieokreślony, wartością domyślną jest &quot; dzień &quot; .<br/><br/>                                 `aggregationLevel` Nie jest obsługiwany bez `aggregationLevel` . `aggregationLevel` ma zastosowanie do **wszystkich zakresów dat** obecnych w `aggregationLevel`                         |
| Orderby                              | ciąg    | Instrukcja, która nakazuje wartości danych wynikowych dla każdej instalacji. Składnia jest następująca: `...&orderby=field[order],field [order],...` Parametr pola może być jednym z następujących ciągów:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Nazwa&quot;<br/>                &quot;rynek&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   Parametr *order* jest opcjonalny i może mieć wartość lub , aby określić kolejność rosnącą lub `asc` `desc` malejącą dla każdego pola. Wartość domyślna to `asc`.<br/><br/>    **Przykład:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| Groupby                              | ciąg    | Instrukcja, która stosuje agregację danych tylko do określonych pól. Można określić następujące pola:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Nazwa*<br/>                *rynek*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 Zwracane wiersze danych zawierają pola określone w `groupby` klauzuli i następujące pola:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            Parametru `groupby` można używać z `aggregationLevel` parametrem .<br/><br/>            **Przykład:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [odsprzedawców pośrednich.](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
