---
title: Pobieranie listy klientów
description: Jak uzyskać zbiór zasobów reprezentujących wszystkich klientów partnerskich.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2dd8469458809ab38b6d6081adc91d6d1184d2d0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768294"
---
# <a name="get-a-list-of-customers"></a>Pobieranie listy klientów

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano, jak uzyskać kolekcję zasobów reprezentujących wszystkich klientów partnerskich.

> [!TIP]
> Tę operację można także wykonać na pulpicie nawigacyjnym Centrum partnerskiego. Na stronie głównej w obszarze **Zarządzanie klientami** wybierz pozycję **Wyświetl klientów**. Na pasku bocznym wybierz pozycję **klienci**.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

## <a name="c"></a>C\#

Aby uzyskać listę wszystkich klientów:

1. Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby utworzyć obiekt **IPartner** .

2. Pobierz listę klientów przy użyciu metod [**Query ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) . (Aby uzyskać instrukcje dotyczące tworzenia zapytania, zobacz Klasa [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) ).

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klasa: **CustomerPaging.cs**

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać listę wszystkich klientów:

1. Użyj funkcji [**IAggregatePartner. GetCustomers**], aby uzyskać odwołanie do operacji klienta.

2. Pobierz listę klientów przy użyciu funkcji **Query ()** .

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Wykonaj polecenie [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) bez parametrów, aby uzyskać pełną listę klientów.

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers? size = {size} http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby uzyskać listę klientów.

| Nazwa     | Typ    | Wymagane | Opis                                        |
|----------|---------|----------|----------------------------------------------------|
| **zmienia** | **int** | Y        | Liczba wyników do wyświetlenia w tym samym czasie. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [klienta](customer-resources.md#customer) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
