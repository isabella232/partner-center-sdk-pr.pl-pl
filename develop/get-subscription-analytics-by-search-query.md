---
title: Pobierz usługę Subscription Analytics według zapytania wyszukiwania
description: Jak uzyskać informacje o analizie subskrypcji odfiltrowane według zapytania wyszukiwania.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767910"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Pobieranie informacji analitycznych dotyczących subskrypcji filtrowanych wg zapytania wyszukiwania

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać informacje o analizie subskrypcji dla klientów odfiltrowanych według zapytania wyszukiwania.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania |
|--------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/subscriptions? Filter = {filter_string} |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj poniższego wymaganego parametru Path, aby zidentyfikować organizację i przefiltrować wyszukiwanie.

| Nazwa | Typ | Wymagane | Opis |
|------|------|----------|-------------|
| filter_string | ciąg | Tak | Filtr, który ma zostać zastosowany do analizy subskrypcji. Zobacz sekcję składnia filtrów i pola filtru, aby poznać składnię, pola i operatory, które mają być używane w tym parametrze. |

### <a name="filter-syntax"></a>Składnia filtru

Parametr Filter musi składać się z szeregu kombinacji pól, wartości i operatora. Wiele kombinacji można łączyć za pomocą **`and`** **`or`** operatora OR.

Niezakodowany przykład wygląda następująco:

- Parametry `?filter=Field operator 'Value'`
- Typu `?filter=Field operator Value`
- Wyświetlana `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Pola filtru

Parametr Filter żądania zawiera jedną lub więcej instrukcji, które filtrują wiersze w odpowiedzi. Każda instrukcja zawiera pole i wartość, które są skojarzone z **`eq`** **`ne`** operatorami or. Niektóre pola obsługują również **`contains`** operatory, **`gt`** , **`lt`** , **`ge`** i **`le`** . Instrukcje można łączyć przy użyciu **`and`** **`or`** operatorów or.

Poniżej przedstawiono przykłady ciągów filtrów:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

W poniższej tabeli przedstawiono listę obsługiwanych pól i operatorów pomocy technicznej dla parametru Filter. Wartości ciągu muszą być ujęte w pojedyncze cudzysłowy.

| Parametr | Obsługiwane operatory | Opis |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Wartość wskazująca, czy subskrypcja jest odnawiana automatycznie. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Data zakończenia subskrypcji. |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Data utworzenia subskrypcji. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data zmiany bieżącego stanu subskrypcji. |
| customerMarket | `eq`, `ne` | Kraj/region, w którym klient wykonuje działalność. |
| customerName | `contains` | Nazwa klienta. |
| customerTenantId | `eq`, `ne` | Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje dzierżawcę klienta. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data anulowania aprowizacji subskrypcji. Wartość domyślna to null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data rozpoczęcia subskrypcji. |
| friendlyName | `contains` | Nazwa subskrypcji. |
| identyfikator | `eq`, `ne` | Ciąg w formacie GUID, który identyfikuje subskrypcję. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data ostatniego odnowienia subskrypcji. Wartość domyślna to null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data ostatniego użycia subskrypcji. Wartość domyślna to null. |
| partnerId | `eq`, `ne` | IDENTYFIKATOR MPN. W przypadku bezpośredniego odsprzedawcy ta wartość będzie MPN IDENTYFIKATORem partnera. W odniesieniu do pośredniego odsprzedawcy ta wartość będzie IDENTYFIKATORem MPN pośredniego odsprzedawcy. |
| partnerName | ciąg | Nazwa partnera, dla którego została zakupiona subskrypcja |
| productName | `contains`, `eq`, `ne` | Nazwa produktu. |
| providerName | ciąg | Gdy transakcja subskrypcyjna dotyczy pośredniego odsprzedawcy, nazwa dostawcy jest dostawcą pośrednim, który kupił subskrypcję.|
| status | `eq`, `ne` | Stan subskrypcji. Obsługiwane wartości to: "ACTIVE", "SUSPENDed" lub "unsupportedd". |
| SubscriptionType | `eq`, `ne` | Typ subskrypcji. **Uwaga**: w tym polu jest rozróżniana wielkość liter. Obsługiwane są następujące wartości: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Data rozpoczęcia okresu próbnego dla subskrypcji. Wartość domyślna to null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Data konwersji subskrypcji z wersji próbnej na płatne. Wartość domyślna to null. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](partner-center-analytics-resources.md#subscription-resource) , które spełniają kryteria filtrowania.

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
