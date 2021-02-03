---
title: Pobieranie danych dotyczących użycia dla subskrypcji według miernika
description: Kolekcji zasobów MeterUsageRecord można użyć do uzyskania rekordów użycia zliczania klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767973"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Pobieranie danych dotyczących użycia dla subskrypcji według miernika

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Kolekcji zasobów **MeterUsageRecord** można użyć do uzyskania rekordów użycia zliczania klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym. Ta kolekcja zasobów reprezentuje zagregowaną sumę dla każdego licznika dla bieżącego cyklu rozliczeniowego w całym planie platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji

*Ta nowa trasa jest równoznaczna z `subscriptions/{subscription-id}/usagerecords/resources` , która będzie nadal działać tylko w przypadku subskrypcji Microsoft Azure (MS-AZR-0145P).* Ta nowa trasa będzie obsługiwać zarówno subskrypcje Microsoft Azure (MS-AZR-0145P), jak i plany platformy Azure. Aby uzyskać informacje dotyczące planu platformy Azure, musisz przełączyć się do tej nowej trasy. Poza właściwościami wymienionymi w poniższych sekcjach odpowiedź jest taka sama jak w przypadku starej trasy.

## <a name="c"></a>C\#

Aby uzyskać rekordy użycia liczników klienta dla określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym:

1. Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .

2. Wywołaj Właściwość subscriptions i **UsageRecords**, a następnie właściwość **mierników** . Zakończ, wywołując metody get () lub GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Aby zapoznać się z przykładem, zobacz następujący przykład:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klasa: **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/meterusagerecords http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania informacji o znamionowym użyciu klienta.

| Nazwa                   | Typ     | Wymagane | Opis                               |
|------------------------|----------|----------|-------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **Identyfikator subskrypcji**    | **guid** | Y        | Identyfikator GUID odpowiadający identyfikatorowi [zasobu subskrypcji](subscription-resources.md#subscription)Centrum partnerskiego, który reprezentuje subskrypcję Microsoft Azure (MS-AZR-0145P) lub plan platformy Azure. *W przypadku zasobów subskrypcji planu platformy Azure Podaj **identyfikator planu** jako **Identyfikator subskrypcji** w tej trasie.* |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca zasób **PagedResourceCollection \<MeterUsageRecord>** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Przykład odpowiedzi dla subskrypcji Microsoft Azure (MS-AZR-0145P)

W tym przykładzie klient zakupił **145Pą usługę Azure PayG**.

*W przypadku klientów z subskrypcją usługi Microsoft Azure (MS-AZR-0145P) nie zostanie zmieniona odpowiedź interfejsu API.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Przykład odpowiedzi REST dla usługi Azure plan

W tym przykładzie klient kupił plan platformy Azure.

*W przypadku klientów z planami platformy Azure w odpowiedzi interfejsu API istnieją następujące zmiany:*

- **currencyLocale** został zastąpiony **CurrencyCode**
- **usdTotalCost** jest nowym polem

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
