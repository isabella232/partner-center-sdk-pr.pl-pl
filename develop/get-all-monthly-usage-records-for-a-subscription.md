---
title: Pobieranie wszystkich rekordów dotyczących miesięcznego użycia dla subskrypcji
description: Możesz użyć kolekcji zasobów AzureResourceMonthlyUsageRecord, aby uzyskać listę usług w ramach subskrypcji klienta i skojarzonych z nimi informacji o użyciu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ee4bd413eec7d5a2dddbe3803df8839589ab7504
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760287"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a>Pobieranie wszystkich rekordów dotyczących miesięcznego użycia dla subskrypcji

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Możesz użyć kolekcji zasobów [**AzureResourceMonthlyUsageRecord,**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) aby uzyskać listę usług w ramach subskrypcji klienta i skojarzonych z nimi informacji o użyciu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

*Ten interfejs API obsługuje Microsoft Azure subskrypcji (MS-AZR-0145P). Jeśli używasz planu platformy Azure, zobacz Zamiast tego zobacz [Get usage data for subscription by meter (Uzyskiwanie](get-a-customer-subscription-meter-usage-records.md) danych użycia dla subskrypcji według miernika).*

## <a name="c"></a>C\#

Aby uzyskać informacje o użyciu zasobów subskrypcji:

1. Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**

2. Wywołaj **właściwości Subscriptions** i **UsageRecords,** a następnie **właściwość Resources.**
3. Wywołaj **metody Get()** **lub GetAsync().**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

Przykład można znaleźć w następujących tematach:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Project: **PartnerSDK.FeatureSample**
- Klasa: **SubscriptionResourceUsageRecords.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

W tej tabeli wymieniono wymagane parametry zapytania w celu uzyskania informacji o użyciu.

| Nazwa                    | Typ     | Wymagane | Opis                               |
|-------------------------|----------|----------|-------------------------------------------|
| **identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **subscription-id** | **guid** | Y        | Identyfikator GUID odpowiadający subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca kolekcję zasobów **AzureResourceMonthlyUsageRecord** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
