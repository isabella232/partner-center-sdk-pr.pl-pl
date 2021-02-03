---
title: Anulowanie zakupów oprogramowania
description: Opcja samoobsługowego anulowania subskrypcji oprogramowania i zakupów bezterminowego w ramach interfejsów API Centrum partnerskiego.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 25fd10a171fa6ca01f3442d49145443f2382cc18
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768093"
---
# <a name="cancel-software-purchases"></a>Anulowanie zakupów oprogramowania

**Dotyczy:**

- Centrum partnerskie

Możesz użyć interfejsów API Centrum partnerskiego, aby anulować subskrypcje oprogramowania i okresowe zakupy oprogramowania (o ile te zakupy zostały dokonane w oknie anulowania od daty zakupu). Nie musisz tworzyć biletu pomocy technicznej w celu dokonania takich operacji, a zamiast nich można używać następujących metod samoobsługi.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

## <a name="c"></a>C\#

Aby anulować kolejność oprogramowania,

1. Przekaż poświadczenia konta do metody [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) , aby uzyskać Interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) w celu pobrania operacji partnerskich.

2. Wybierz określoną [kolejność](order-resources.md#order) , którą chcesz anulować. Wywołaj metodę [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, a następnie **Orders. ById ()** z identyfikatorem zamówienia.

3. Wywołaj metodę **Get** lub **GetAsync** , aby pobrać zamówienie.

4. Ustaw właściwość [**Order. status**](order-resources.md#order) na wartość `cancelled` .

5. Obowiązkowe Jeśli chcesz określić niektóre elementy wiersza do anulowania, ustaw polecenie [**Order. LineItems**](order-resources.md#order) na listę elementów wiersza, które chcesz anulować.

6. Aby zaktualizować kolejność, użyj metody **patch ()** .

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów zapytania, aby usunąć klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość to identyfikator GUID w formacie identyfikatora dzierżawy klienta, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |
| **Identyfikator zamówienia** | **parametry** | Y        | Wartość jest ciągiem, który oznacza identyfikator zamówienia, który ma zostać anulowany. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca zamówienie z anulowanymi elementami wiersza.

Stan zamówienia zostanie oznaczony jako **anulowany** , jeśli wszystkie elementy wiersza w zamówieniu zostaną anulowane lub **ukończone** , jeśli nie wszystkie elementy wiersza w zamówieniu zostaną anulowane.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

W poniższym przykładzie odpowiedzi można zobaczyć, że ilość elementu wiersza o identyfikatorze oferty **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** stała się równa zero (0). Ta zmiana oznacza, że element wiersza, który został oznaczony do anulowania został pomyślnie anulowany. Przykładowa kolejność zawiera inne elementy wiersza, które nie zostały anulowane, co oznacza, że stan zamówienia ogólnego zostanie oznaczony jako **ukończone**, a nie **anulowane**.

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
