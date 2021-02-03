---
title: Zmiana ilości subskrypcji
description: Dowiedz się, jak zmienić liczbę licencji dla subskrypcji klienta przy użyciu interfejsów API usługi Partner Center. Można to również zrobić na pulpicie nawigacyjnym Centrum partnerskiego.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768589"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a>Zmień liczbę licencji w ramach subskrypcji klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Aktualizuje [subskrypcję](subscription-resources.md) , aby zwiększyć lub zmniejszyć liczbę licencji.

Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md). Następnie wybierz subskrypcję, której nazwę chcesz zmienić. Aby zakończyć, Zmień wartość w polu **ilość** , a następnie wybierz pozycję **Prześlij.**

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby zmienić liczbę subskrypcji klienta, najpierw [Uzyskaj subskrypcję](get-a-subscription-by-id.md), a następnie [**Zmień właściwość wartość**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) subskrypcji. Po wprowadzeniu zmiany Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** . Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) . Następnie Zakończ, wywołując metodę **patch ()** .

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSample **Klasa**: UpdateSubscription.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Ta tabela zawiera listę wymaganych parametrów zapytania, aby zmienić liczbę subskrypcji.

| Nazwa                    | Typ     | Wymagane | Opis                               |
|-------------------------|----------|----------|-------------------------------------------|
| **Identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **Identyfikator — dla subskrypcji** | **guid** | Y        | Identyfikator GUID odpowiadający subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W treści żądania jest wymagany pełny zasób **subskrypcji** . Upewnij się, że właściwość **ilość** została zaktualizowana.

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
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
    "Status": "active",
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

Jeśli to się powiedzie, ta metoda zwraca kod stanu **HTTP 200** i zaktualizowane właściwości [zasobów subskrypcji](subscription-resources.md)  w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zwraca kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać kod stanu, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

Gdy operacja patch trwa dłużej niż oczekiwany czas, centrum partnerskie wyśle kod stanu **http o stanie 202** i nagłówek lokalizacji wskazujący, gdzie pobrać subskrypcję. W celu monitorowania zmian stanu i ilości można wykonać zapytanie o subskrypcję okresowo.

### <a name="response-examples"></a>Przykłady odpowiedzi

#### <a name="response-example-1"></a>Przykład odpowiedzi 1

Pomyślne żądanie ze **stanem HTTP 200** kod stanu:

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
    "Status": "active",
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

#### <a name="response-example-2"></a>Przykład odpowiedzi 2

Pomyślne żądanie ze **stanem HTTP 202** kod stanu:

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
