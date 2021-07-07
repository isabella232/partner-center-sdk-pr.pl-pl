---
title: Zawieszenie subskrypcji
description: Wstrzymuje zasób subskrypcji, który pasuje do klienta i identyfikatora subskrypcji z powodu oszustwa lub braku płatności. Na Partner Center nawigacyjnym tę operację można wykonać, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dae7c3422a403c48a2b10424c4ae5dbdbc498ea
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547346"
---
# <a name="suspend-a-subscription"></a>Zawieszenie subskrypcji

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Wstrzymuje [zasób](subscription-resources.md) subskrypcji, który pasuje do klienta i identyfikatora subskrypcji z powodu oszustwa lub braku płatności.

Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md). Następnie wybierz subskrypcję, którą chcesz zmienić. Aby zakończyć, wybierz przycisk **Wstrzymano,** a następnie wybierz pozycję **Prześlij.**

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby wstrzymać subskrypcję klienta, najpierw [pobierz subskrypcję,](get-a-subscription-by-id.md)a następnie zmień właściwość [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji. Aby uzyskać informacje **na temat kodów** stanu, zapoznaj się z tematem [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). Po wejściu zmiany użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().** Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Następnie zakończ, wywołując **metodę Patch().**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Suspended
   });
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** Klasa PartnerSDK.FeatureSample: UpdateSubscription.cs 

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

W tej tabeli wymieniono parametr zapytania wymagany do wstrzymania subskrypcji.

| Nazwa                    | Typ     | Wymagane | Opis                               |
|-------------------------|----------|----------|-------------------------------------------|
| **identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **identyfikator subskrypcji** | **guid** | Y        | Identyfikator GUID odpowiadający subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W treści **żądania** wymagany jest pełny zasób Subskrypcji. Upewnij **się, że właściwość Status** została zaktualizowana.

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca zaktualizowane [właściwości](subscription-resources.md) zasobów subskrypcji w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
