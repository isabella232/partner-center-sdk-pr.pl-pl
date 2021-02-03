---
title: Pobieranie zamówienia według identyfikatora
description: Pobiera zasób zamówienia, który odpowiada IDENTYFIKATORowi klienta i zamówienia.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 0a39d7142e5bf97f9fb345416964d4ed6bb935ad
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768454"
---
# <a name="get-an-order-by-id"></a>Pobieranie zamówienia według identyfikatora

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Pobiera zasób [zamówienia](order-resources.md) , który odpowiada identyfikatorowi klienta i zamówienia.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator zamówienia.

## <a name="c"></a>C\#

Aby uzyskać zamówienie klienta według identyfikatora:

1. Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .

2. Wywołaj Właściwość [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , a następnie metodę [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) jeszcze raz.
3. Wywołanie [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSample **Klasa**: GetOrder.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby uzyskać zamówienie klienta według identyfikatora:

1. Użyj funkcji **IAggregatePartner. GetCustomers** i wywołaj funkcję **byId ()** .

2. Wywołaj funkcję **GetOrders** , a następnie funkcję **byID ()** jeszcze raz.
3. Wywołaj funkcję **Get ()** .

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby uzyskać identyfikator zamówienia klienta według identyfikatora, należy wykonać polecenie [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) i określić parametry **CustomerID** i **IDZamówienia** .

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{ID-for-Order} http/1.1  |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania identyfikatora order by.

| Nazwa                   | Typ     | Wymagane | Opis                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| Identyfikator dzierżawy klienta     | ciąg   | Tak      | Ciąg w formacie GUID odpowiadający klientowi. |
| Identyfikator — dla zamówienia           | ciąg   | Tak      | Ciąg odpowiadający IDENTYFIKATORowi zamówienia.                |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca zasób [zamówienia](order-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
