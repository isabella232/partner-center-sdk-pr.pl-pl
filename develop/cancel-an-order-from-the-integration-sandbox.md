---
title: Anulowanie zamówienia z piaskownicy integracji
description: Dowiedz się, jak za pomocą Partner Center API anulować różne typy zamówień subskrypcji z kont piaskownicy integracji.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104975"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Anulowanie zamówienia z piaskownicy integracji przy użyciu Partner Center API

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

W tym artykule opisano, jak za pomocą Partner Center API anulować różne typy zamówień subskrypcji z kont piaskownicy integracji. Takie zamówienia mogą obejmować wystąpienia zarezerwowane, oprogramowanie i zamówienia subskrypcji oprogramowania jako usługi (SaaS) na platformie handlowej.

> [!NOTE] 
> Należy pamiętać, że anulowanie zamówień subskrypcji SaaS wystąpienia zarezerwowanego lub komercyjnej platformy handlowej jest możliwe tylko z kont piaskownicy integracji. Nie można anulować żadnych zamówień piaskownicy starszych niż 60 dni Partner Center.

Aby anulować produkcyjne zamówienia oprogramowania za pośrednictwem interfejsu API, [użyj polecenia cancel-software-purchases.](cancel-software-purchases.md)
Możesz również anulować produkcyjne zamówienia oprogramowania za pośrednictwem pulpitu [nawigacyjnego, anulując zakup.](/partner-center/csp-software-subscriptions)

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Konto partnera piaskownicy integracji z klientem z aktywnym wystąpieniem zarezerwowanym/ oprogramowaniem /zamówieniami subskrypcji SaaS innych firm.

## <a name="c"></a>C\#

Aby anulować zamówienie z piaskownicy integracji, przekaż poświadczenia konta do metody , aby uzyskać [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) interfejs do uzyskania operacji [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) partnera.

Aby wybrać konkretne [zamówienie,](order-resources.md#order)użyj operacji partnera i wywołaj metodę z identyfikatorem klienta, aby określić klienta, a następnie z identyfikatorem zamówienia, aby określić zamówienie, oraz metodę lub , [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) aby je **`Orders.ById()`** **`Get`** **`GetAsync`** pobrać.

Ustaw właściwość [**`Order.Status`**](order-resources.md#order) na i użyj metody , aby `cancelled` **`Patch()`** zaktualizować zamówienie.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby usunąć klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy. |
| **order-id** | **ciąg** | Y        | Wartość jest ciągiem oznaczający identyfikatory zamówień, które muszą zostać anulowane. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca anulowane zamówienie.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
