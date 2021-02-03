---
title: Pobieranie danych dotyczących użycia dla subskrypcji według zasobu
description: Zasobu ResourceUsageRecord można użyć do uzyskania rekordów użycia zasobów klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767969"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>Pobieranie danych dotyczących użycia dla subskrypcji według zasobu

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano sposób pobierania zasobu **ResourceUsageRecord** . Ten zasób reprezentuje zagregowaną sumę dla danego miesiąca dla poszczególnych zasobów zainicjowanych w planie platformy Azure. Za pomocą tego zasobu można pobrać rekordy użycia zasobów klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym. Ten interfejs API zwraca dane, które nie były wcześniej dostępne za pomocą interfejsów API wydatków platformy Azure.

*Ta trasa nie obsługuje subskrypcji Microsoft Azure (MS-AZR-0145P).*

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji

## <a name="c"></a>C\#

Aby uzyskać rekordy użycia zasobów klienta dla określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym:

1. Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .

2. Wywołaj Właściwość subscriptions, a następnie **UsageRecords**, a następnie właściwości **resources** . Zakończ, wywołując metody get () lub GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klasa: **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/resourceusagerecords http/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca zasób **PagedResourceCollection \<ResourceUsageRecord>** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
