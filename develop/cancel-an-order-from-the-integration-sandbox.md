---
title: Anulowanie zamówienia z piaskownicy integracji
description: Dowiedz się, jak za pomocą interfejsów API usługi Partner Center anulować różne typy zamówień subskrypcji z kont piaskownicy integracji.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768597"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Anulowanie zamówienia z piaskownicy integracji przy użyciu interfejsów API usługi Partner Center

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano sposób używania interfejsów API usługi Partner Center do anulowania różnych typów zamówień subskrypcji z kont piaskownicy integracji. Takie zamówienia mogą obejmować wystąpienia zarezerwowane, oprogramowanie i komercyjne zamówienie na oprogramowanie Marketplace jako usługa (SaaS).

>[!NOTE]
>Należy pamiętać, że anulowane subskrypcje wystąpień zarezerwowanych lub komercyjnych zakupów rynkowych SaaS są możliwe tylko z kont piaskownicy integracji.  

Aby anulować zlecenia produkcyjne oprogramowania za pomocą interfejsu API, należy użyć polecenia [Anuluj zakup oprogramowania](cancel-software-purchases.md).
Możesz również anulować zlecenia produkcyjne oprogramowania za pośrednictwem pulpitu nawigacyjnego, używając [przycisku Anuluj zakup](/partner-center/csp-software-subscriptions).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Konto partnera piaskownicy integracji z klientem z aktywną alternatywnym wystąpieniem/oprogramowaniem/SaaSą subskrypcją innych firm.

## <a name="c"></a>C\#

Aby anulować zamówienie z piaskownicy integracji, Przekaż poświadczenia konta do [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metody w celu uzyskania [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interfejsu umożliwiającego uzyskanie operacji partnerskich.

Aby wybrać określoną [kolejność](order-resources.md#order), użyj operacji partnera i [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metody Call z identyfikatorem klienta, aby określić klienta, a następnie pozycję **`Orders.ById()`** z identyfikatorem zamówienia, aby określić kolejność, a wreszcie **`Get`** lub metodę, **`GetAsync`** Aby ją pobrać.

Ustaw [**`Order.Status`**](order-resources.md#order) Właściwość na `cancelled` i użyj metody, **`Patch()`** Aby zaktualizować kolejność.

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
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby usunąć klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |
| **Identyfikator zamówienia** | **parametry** | Y        | Wartość jest ciągiem wskazującym identyfikatory kolejności, które muszą być anulowane. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, metoda zwraca anulowaną kolejność.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
