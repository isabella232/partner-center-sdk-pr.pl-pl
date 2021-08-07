---
title: Uzyskiwanie analizy subskrypcji pogrupowanych według dat lub terminów
description: Jak uzyskać informacje dotyczące analizy subskrypcji pogrupowane według dat lub terminów.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66336d3e5573598eb4810853ad2704bc8d2c76680292a4f5b4a3da9bb50936b8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989682"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Uzyskiwanie analizy subskrypcji pogrupowanych według dat lub terminów

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak uzyskać informacje analityczne dotyczące subskrypcji dla klientów pogrupowane według dat lub terminów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|--------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries} |

### <a name="uri-parameters"></a>Parametry URI

Użyj następujących wymaganych parametrów ścieżki, aby zidentyfikować organizację i pogrupować wyniki.

| Nazwa | Typ | Wymagane | Opis |
|------|------|----------|-------------|
| groupby_queries | pary ciągów i dateTime | Tak | Terminy i daty do filtrowania wyniku. |

### <a name="groupby-syntax"></a>Składnia grupowania

Parametr grupowania musi być składany jako seria wartości pól rozdzielonych przecinkami.

Niezakodowany przykład wygląda następująco:

```http
?groupby=termField1,dateField1,termField2
```

W poniższej tabeli przedstawiono listę obsługiwanych pól dla grupowania według.

| Pole | Typ | Opis |
|-------|------|-------------|
| customerTenantId | ciąg | Ciąg w formacie identyfikatora GUID, który identyfikuje dzierżawę klienta. |
| Customername | ciąg | Nazwa klienta. |
| customerMarket | ciąg | Kraj/region, w którym klient działa. |
| identyfikator | ciąg | Ciąg w formacie identyfikatora GUID, który identyfikuje subskrypcję. |
| status | ciąg | Stan subskrypcji. Obsługiwane wartości to: "ACTIVE", "SUSPENDED" lub "DEPROVISIONED". |
| Productname | ciąg | Nazwa produktu. |
| Subscriptiontype | ciąg | Typ subskrypcji. Uwaga: w tym polu jest zróżnicowa wielkość liter. Obsługiwane wartości to: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Wartość logiczna | Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie. |
| partnerId  | ciąg | Identyfikator MPN. W przypadku odsprzedawcy bezpośredniego ten parametr będzie identyfikatorem MPN partnera. W przypadku odsprzedawcy pośredniego ten parametr będzie identyfikatorem MPN odsprzedawcy pośredniego. |
| Friendlyname | ciąg | Nazwa subskrypcji. |
| nazwa_partnera | ciąg | Nazwa partnera, dla którego zakupiono subskrypcję |
| Providername | ciąg | Gdy transakcja subskrypcji jest dla odsprzedawcy pośredniego, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.
| Creationdate | ciąg w formacie daty i czasu UTC | Data utworzenia subskrypcji. |
| effectiveStartDate | ciąg w formacie daty i czasu UTC | Data rozpoczęcia subskrypcji. |
| commitmentEndDate | ciąg w formacie daty i czasu UTC | Data zakończenia subskrypcji. |
| currentStateEndDate | ciąg w formacie daty i czasu UTC | Data zmiany bieżącego stanu subskrypcji. |
| trialToPaidConversionDate | ciąg w formacie daty i czasu UTC | Data konwersji subskrypcji z wersji próbnej na płatną. Wartość domyślna to null. |
| trialStartDate | ciąg w formacie daty i czasu UTC | Data rozpoczęcia okresu próbnego subskrypcji. Wartość domyślna to null. |
| lastUsageDate | ciąg w formacie daty i czasu UTC | Data ostatniego użytej subskrypcji. Wartość domyślna to null. |
| deprovisionedDate | ciąg w formacie daty i czasu UTC | Data coprowizowana subskrypcji. Wartość domyślna to null. |
| lastRenewalDate | ciąg w formacie daty i czasu UTC | Data ostatniego odnowienia subskrypcji. Wartość domyślna to null. |

### <a name="filter-fields"></a>Filtrowanie pól

W poniższej tabeli wymieniono opcjonalne pola filtru i ich opisy:

| Pole | Typ |  Opis |
|-------|------|--------------|
| top (pierwsze) | int | Liczba wierszy danych do zwrócenia w żądaniu. Jeśli wartość nie zostanie określona, wartość maksymalna i wartość domyślna to 10000. Jeśli w zapytaniu znajduje się więcej wierszy, treść odpowiedzi zawiera następny link, za pomocą których można zażądać następnej strony danych. |
| Pomiń | int | Liczba wierszy do pominięcia w zapytaniu. Ten parametr umożliwia stronicować duże zestawy danych. Na przykład wartości top=10000 i skip=0 pobierają pierwsze 10000 wierszy danych, top=10000, a skip=10000 pobiera następne 10000 wierszy danych. |
| filter | ciąg | Co najmniej jedna instrukcja, która filtruje wiersze w odpowiedzi. Każda instrukcja filtru zawiera nazwę pola z treści odpowiedzi i wartość skojarzoną z operatorem **`eq`** , lub dla niektórych **`ne`** **`contains`** pól. Instrukcje można łączyć przy użyciu **`and`** instrukcji lub **`or`** . Wartości ciągu muszą być otoczone pojedynczymi cudzysłowami w parametrze filtru. Zobacz następującą sekcję, aby uzyskać listę pól, które można filtrować, oraz operatory obsługiwane przez te pola. |
| aggregationLevel | ciąg | Określa zakres czasu, dla którego mają zostać pobrane zagregowane dane. Może być jednym z następujących ciągów: **dzień,** **tydzień** lub **miesiąc**. Jeśli wartość nie zostanie określona, wartością domyślną jest **dateRange**. **Uwaga:** ten parametr ma zastosowanie tylko wtedy, gdy pole daty jest przekazywane jako część parametru groupBy. |
| Groupby | ciąg | Instrukcja, która stosuje agregację danych tylko do określonych pól. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) pogrupowanych według określonych terminów i dat.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
