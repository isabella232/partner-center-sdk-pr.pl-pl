---
title: Uzyskiwanie analizy subskrypcji według zapytania wyszukiwania
description: Sposób filtrowania informacji analizy subskrypcji według zapytania wyszukiwania.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dc6ef8d2136c5ffac3278a372980e9a601ef49bb485ef54187865fc9431b3404
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995683"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Pobieranie informacji analitycznych dotyczących subskrypcji filtrowanych wg zapytania wyszukiwania

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak uzyskać informacje analityczne dotyczące subskrypcji dla klientów przefiltrowane według zapytania wyszukiwania.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|--------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string} |

### <a name="uri-parameters"></a>Parametry URI

Użyj następującego parametru wymaganej ścieżki, aby zidentyfikować organizację i odfiltrować wyszukiwanie.

| Nazwa | Typ | Wymagane | Opis |
|------|------|----------|-------------|
| filter_string | ciąg | Tak | Filtr do zastosowania do analizy subskrypcji. Zobacz sekcje Składnia filtru i Pola filtru, aby uzyskać informacje o składni, polach i operatorach do użycia w tym parametrze. |

### <a name="filter-syntax"></a>Składnia filtru

Parametr filtru musi składać się z serii kombinacji pól, wartości i operatorów. Wiele kombinacji można łączyć przy użyciu **`and`** operatorów **`or`** lub .

Niezakodowany przykład wygląda następująco:

- Ciąg: `?filter=Field operator 'Value'`
- Boolean: `?filter=Field operator Value`
- Zawiera `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Filtrowanie pól

Parametr filtru żądania zawiera co najmniej jedną instrukcje, które filtruje wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z operatorami **`eq`** **`ne`** lub . Niektóre pola obsługują również **`contains`** operatory **`gt`** , , , **`lt`** i **`ge`** **`le`** . Instrukcje można łączyć przy użyciu **`and`** operatorów **`or`** lub .

Poniżej przedstawiono przykłady ciągów filtrów:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

W poniższej tabeli przedstawiono listę obsługiwanych pól i operatorów obsługi dla parametru filtru. Wartości ciągu muszą być otoczone pojedynczymi cudzysłowami.

| Parametr | Obsługiwane operatory | Opis |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Data zakończenia subskrypcji. |
| Creationdate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Data utworzenia subskrypcji. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data zmiany bieżącego stanu subskrypcji. |
| customerMarket | `eq`, `ne` | Kraj/region, w którym klient działa. |
| Customername | `contains` | Nazwa klienta. |
| customerTenantId | `eq`, `ne` | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje dzierżawę klienta. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data coprowizowana subskrypcji. Wartość domyślna to null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data rozpoczęcia subskrypcji. |
| Friendlyname | `contains` | Nazwa subskrypcji. |
| identyfikator | `eq`, `ne` | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data ostatniego odnowienia subskrypcji. Wartość domyślna to null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data ostatniego użytej subskrypcji. Wartość domyślna to null. |
| partnerId | `eq`, `ne` | Identyfikator MPN. W przypadku odsprzedawcy bezpośredniego ta wartość będzie identyfikatorem MPN partnera. W przypadku odsprzedawcy pośredniego ta wartość będzie identyfikatorem MPN odsprzedawcy pośredniego. |
| partnerName | ciąg | Nazwa partnera, dla którego zakupiono subskrypcję |
| Productname | `contains`, `eq`, `ne` | Nazwa produktu. |
| Providername | ciąg | Gdy transakcja subskrypcji jest dla odsprzedawcy pośredniego, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.|
| status | `eq`, `ne` | Stan subskrypcji. Obsługiwane wartości to: "ACTIVE", "SUSPENDED" lub "DEPROVISIONED". |
| Subscriptiontype | `eq`, `ne` | Typ subskrypcji. **Uwaga:** w tym polu jest zróżnicowa wielkość liter. Obsługiwane wartości to: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data rozpoczęcia okresu próbnego subskrypcji. Wartość domyślna to null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Data konwersji subskrypcji z wersji próbnej na płatną. Wartość domyślna to null. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) spełniających kryteria filtrowania.

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>Zobacz też

- [Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
