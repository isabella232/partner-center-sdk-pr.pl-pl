---
title: Pobierz Podsumowanie użycia dla subskrypcji klienta
description: Zasobu SubscriptionUsageSummary można użyć do uzyskania podsumowania użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767966"
---
# <a name="get-usage-summary-for-customers-subscription"></a>Pobierz Podsumowanie użycia dla subskrypcji klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Za pomocą zasobu **SubscriptionUsageSummary** można uzyskać podsumowanie użycia subskrypcji dla klienta. Ten zasób reprezentuje Podsumowanie użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji

## <a name="c"></a>C\#

Aby uzyskać podsumowanie użycia subskrypcji dla subskrypcji klienta:

1. Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .

2. Następnie Wywołaj Właściwość subscriptions, a także właściwość **UsageSummary** . Zakończ, wywołując metody get () lub GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klasa: **GetSubscriptionUsageSummary.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/usagesummary http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania informacji o znamionowym użyciu klienta.

| Nazwa                   | Typ     | Wymagane | Opis                               |
|------------------------|----------|----------|-------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **Identyfikator subskrypcji**    | **guid** | Y        | Identyfikator GUID odpowiadający identyfikatorowi subskrypcji. W przypadku planu platformy Azure jest to identyfikator odpowiedniego [zasobu subskrypcji](subscription-resources.md#subscription)Centrum partnerskiego, który reprezentuje plan platformy Azure. *W przypadku zasobów subskrypcji planu platformy Azure Podaj **identyfikator planu** jako **Identyfikator subskrypcji** w tej trasie.* |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca zasób **SubscriptionUsageSummary** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Przykład odpowiedzi dla subskrypcji Microsoft Azure (MS-AZR-0145P)

W tym przykładzie klient zakupił ofertę **145Pą platformy Azure** .

*W przypadku klientów z subskrypcjami Microsoft Azure (MS-AZR-0145P) nie będzie zmieniana odpowiedź interfejsu API.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Przykład odpowiedzi REST dla usługi Azure plan

W tym przykładzie klient kupił plan platformy Azure.

*W przypadku klientów z planami platformy Azure istnieją następujące zmiany dotyczące odpowiedzi interfejsu API:*

- **currencyLocale** został zastąpiony **CurrencyCode**
- **usdTotalCost** jest nowym polem

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
