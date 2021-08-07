---
title: Uzyskiwanie podsumowania użycia subskrypcji klienta
description: Możesz użyć zasobu SubscriptionUsageSummary, aby uzyskać podsumowanie użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df7757807256fee8326969011f4d038c981c07362ee354ef929e592a7931a728
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992776"
---
# <a name="get-usage-summary-for-customers-subscription"></a>Uzyskiwanie podsumowania użycia subskrypcji klienta

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Możesz użyć zasobu **SubscriptionUsageSummary,** aby uzyskać podsumowanie użycia subskrypcji dla klienta. Ten zasób reprezentuje podsumowanie użycia subskrypcji dla określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji

## <a name="c"></a>C\#

Aby uzyskać podsumowanie użycia subskrypcji dla subskrypcji klienta:

1. Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**

2. Następnie wywołaj właściwość Subscriptions i **właściwość UsageSummary.** Zakończ, wywołując metody Get() lub GetAsync().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

Przykład można znaleźć w następujących tematach:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Klasa: **GetSubscriptionUsageSummary.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

W tej tabeli wymieniono wymagane parametry zapytania w celu uzyskania informacji o użyciu ocenianych przez klienta.

| Nazwa                   | Typ     | Wymagane | Opis                               |
|------------------------|----------|----------|-------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **subscription-id**    | **guid** | Y        | Identyfikator GUID odpowiadający identyfikatorowi subskrypcji. W przypadku planu platformy Azure jest to identyfikator odpowiedniego zasobu Partner Center [subskrypcji](subscription-resources.md#subscription), który reprezentuje plan platformy Azure. *W przypadku zasobów subskrypcji planu platformy Azure podaj **identyfikator planu** jako identyfikator **subskrypcji w** tej trasie.* |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca **zasób SubscriptionUsageSummary** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Przykład odpowiedzi dla Microsoft Azure subskrypcji (MS-AZR-0145P)

W tym przykładzie klient kupił ofertę **145P usługi Azure PayG.**

*W przypadku klientów Microsoft Azure subskrypcji (MS-AZR-0145P) odpowiedź interfejsu API nie zmieni się.*

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

## <a name="rest-response-example-for-azure-plan"></a>Przykład odpowiedzi REST dla planu platformy Azure

W tym przykładzie klient kupił plan platformy Azure.

*W przypadku klientów z planami platformy Azure istnieją następujące zmiany odpowiedzi interfejsu API:*

- **CurrencyLocale jest** zastępowany wartością **currencyCode**
- **USDTotalCost** to nowe pole

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
