---
title: Zmiana cyklu rozliczeniowego
description: Dowiedz się, jak zaktualizować subskrypcję klienta do miesięcznej lub rocznej rozliczania przy użyciu interfejsów API Centrum partnerskiego. Można to również zrobić z poziomu pulpitu nawigacyjnego Centrum partnerskiego.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768601"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Zmień cykl rozliczeniowy subskrypcji klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Aktualizuje [Zamówienie](order-resources.md) od miesięcznego do rocznego rozliczania lub rocznego rozliczania.

Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, przechodząc do strony szczegółów subskrypcji klienta. W tej chwili zobaczysz opcję definiującą bieżący cykl rozliczeniowy dla subskrypcji z możliwością jej zmiany i przesłania.

**Poza zakresem** tego artykułu:

- Zmiana cyklu rozliczeniowego dla prób
- Zmiana cykli rozliczeń w przypadku ofert nierocznych (miesięcznych, 6-letnich) & subskrypcji platformy Azure
- Zmiana cykli rozliczeń dla nieaktywnych subskrypcji
- Zmiana cykli rozliczeń dla subskrypcji opartych na licencji programu Microsoft Usługi online

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator zamówienia.

## <a name="c"></a>C\#

Aby zmienić częstotliwość cyklu rozliczeniowego, zaktualizuj właściwość [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Ta tabela zawiera listę wymaganych parametrów zapytania, aby zmienić liczbę subskrypcji.

| Nazwa                   | Typ | Wymagane | Opis                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | GUID |    Y     | Identyfikator GUID w formacie identyfikatora **dzierżawy klienta** , który identyfikuje klienta |
| **Identyfikator zamówienia**           | GUID |    Y     | Identyfikator zamówienia                                                 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W poniższych tabelach opisano właściwości w treści żądania.

### <a name="order"></a>Zamówienie

| Właściwość           | Typ             | Wymagane | Opis                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | ciąg           |    N     | Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia |
|ReferenceCustomerId | ciąg           |    Y     | Identyfikator klienta                                                    |
| BillingCycle       | ciąg           |    Y     | Wskazuje częstotliwość, z jaką jest rozliczany partner dla tego zamówienia. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](product-resources.md#billingcycletype). |
| LineItems          | Tablica obiektów |    Y     | Tablica zasobów [OrderLineItem](#orderlineitem)                      |
| CreationDate       | datetime         |    N     | Data, w której zamówienie zostało utworzone, w formacie daty i godziny                        |
| Atrybuty         | Obiekt           |    N     | Zawiera "ObjectType": "OrderLineItem"                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Właściwość             | Typ   | Wymagane | Opis                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | liczba |    Y     | Numer elementu wiersza, zaczynając od 0                                              |
| OfferId              | ciąg |    Y     | Identyfikator oferty                                                                |
| SubscriptionId       | ciąg |    Y     | Identyfikator subskrypcji                                                         |
| FriendlyName         | ciąg |    N     | Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, aby pomóc w odróżnieniu |
| Ilość             | liczba |    Y     | Liczba licencji lub wystąpień                                                |
| PartnerIdOnRecord    | ciąg |    N     | IDENTYFIKATOR MPN partnera rekordu                                                |
| Atrybuty           | Obiekt |    N     | Zawiera "ObjectType": "OrderLineItem"                                             |

### <a name="request-example"></a>Przykład żądania

Aktualizowanie do rozliczeń rocznych

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca zaktualizowany porządek subskrypcji w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```