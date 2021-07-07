---
title: Zmiana cyklu rozliczeniowego
description: Dowiedz się, jak zaktualizować subskrypcję klienta do rozliczeń miesięcznych lub rocznych przy użyciu Partner Center API. Możesz to również zrobić z Partner Center nawigacyjnego.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974118"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Zmienianie cyklu rozliczeniowego subskrypcji klienta

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Aktualizuje zamówienie [z](order-resources.md) rozliczenia miesięcznego na roczne lub rocznego na miesięczne.

Na Partner Center nawigacyjnym można wykonać tę operację, przechodząc do strony szczegółów subskrypcji klienta. W tym miejscu zobaczysz opcję definiowania bieżącego cyklu rozliczeniowego dla subskrypcji z możliwością jej zmiany i przesyłania.

**Poza zakresem** tego artykułu:

- Zmiana cyklu rozliczeniowego dla wersji próbnych
- Zmiana cykli rozliczeniowych dla wszystkich ofert poza rocznym okresem (miesięcznych, sześciorocznych) & subskrypcji platformy Azure
- Zmienianie cykli rozliczeniowych dla nieaktywnych subskrypcji
- Zmienianie cykli rozliczeniowych dla subskrypcji Usługi online Microsoft opartych na licencjach

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator zamówienia.

## <a name="c"></a>C\#

Aby zmienić częstotliwość cyklu rozliczeniowego, zaktualizuj [**właściwość Order.BillingCycle.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)

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
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

W tej tabeli wymieniono parametr zapytania wymagany do zmiany ilości subskrypcji.

| Nazwa                   | Typ | Wymagane | Opis                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | GUID |    Y     | Identyfikator GUID **sformatowany jako customer-tenant-id,** który identyfikuje klienta |
| **order-id**           | GUID |    Y     | Identyfikator zamówienia                                                 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W poniższych tabelach opisano właściwości w treści żądania.

### <a name="order"></a>Zamówienie

| Właściwość           | Typ             | Wymagane | Opis                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | ciąg           |    N     | Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia |
|ReferenceCustomerId | ciąg           |    Y     | Identyfikator klienta                                                    |
| BillingCycle       | ciąg           |    Y     | Wskazuje częstotliwość, za pomocą której partner jest rozliczany za to zamówienie. Obsługiwane wartości to nazwy członków w [typie BillingCycleType](product-resources.md#billingcycletype). |
| LineItems          | tablica obiektów |    Y     | Tablica zasobów [OrderLineItem](#orderlineitem)                      |
| Creationdate       | datetime         |    N     | Data utworzenia zamówienia w formacie data/godzina                        |
| Atrybuty         | Obiekt           |    N     | Zawiera "ObjectType": "OrderLineItem"                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Właściwość             | Typ   | Wymagane | Opis                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | liczba |    Y     | Numer elementu wiersza rozpoczynający się od 0                                              |
| OfferId              | ciąg |    Y     | Identyfikator oferty                                                                |
| SubscriptionId       | ciąg |    Y     | Identyfikator subskrypcji                                                         |
| FriendlyName         | ciąg |    N     | Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu uujednoznania |
| Liczba             | liczba |    Y     | Liczba licencji lub wystąpień                                                |
| PartnerIdOnRecord    | ciąg |    N     | Identyfikator MPN partnera rekordu                                                |
| Atrybuty           | Obiekt |    N     | Zawiera "ObjectType": "OrderLineItem"                                             |

### <a name="request-example"></a>Przykład żądania

Aktualizowanie do rozliczenia rocznego

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

W przypadku powodzenia ta metoda zwraca zaktualizowaną kolejność subskrypcji w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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