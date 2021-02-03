---
title: Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji.
description: Możesz użyć kolekcji zasobów AzureResourceMonthlyUsageRecord, aby uzyskać listę usług w ramach subskrypcji klienta i ich skojarzone informacje o użyciu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768365"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a>Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji.

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Możesz użyć kolekcji zasobów [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) , aby uzyskać listę usług w ramach subskrypcji klienta i ich skojarzone informacje o użyciu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

*Ten interfejs API obsługuje tylko subskrypcje Microsoft Azure (MS-AZR-0145P). Jeśli używasz planu platformy Azure, zobacz [pobieranie danych użycia dla subskrypcji według miernika](get-a-customer-subscription-meter-usage-records.md) .*

## <a name="c"></a>C\#

Aby uzyskać informacje o użyciu zasobów subskrypcji:

1. Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .

2. Wywołaj Właściwość **subscriptions** , a następnie **UsageRecords**, a następnie właściwości **resources** .
3. Wywołaj metody **Get ()** lub **GetAsync ()** .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSample**
- Klasa: **SubscriptionResourceUsageRecords.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription}/usagerecords/Resources http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać informacje o ocenach użycia.

| Nazwa                    | Typ     | Wymagane | Opis                               |
|-------------------------|----------|----------|-------------------------------------------|
| **Identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **Identyfikator subskrypcji** | **guid** | Y        | Identyfikator GUID odpowiadający subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **AzureResourceMonthlyUsageRecord** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
