---
title: Pobieranie stanu aprowizacji subskrypcji
description: Jak uzyskać status aprowizacji subskrypcji klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38544aa380ba0a6a8804ae45f7d8ae7cb431d3ba
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768437"
---
# <a name="get-subscription-provisioning-status"></a>Pobieranie stanu aprowizacji subskrypcji

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać status aprowizacji subskrypcji klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

- Do wykonania tej operacji są wymagane uprawnienia administratora delegowanego.

## <a name="c"></a>C\#

Aby uzyskać stan aprowizacji subskrypcji, Zacznij od użycia metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę Subscription [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji. Następnie użyj właściwości [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) , aby uzyskać interfejs do operacji stanu aprowizacji bieżącej subskrypcji, a następnie Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) , aby pobrać obiekt [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) .

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/provisioningstatus http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.

| Nazwa            | Typ   | Wymagane | Opis                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| Identyfikator klienta     | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje klienta.     |
| Identyfikator subskrypcji | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje subskrypcję. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a>Uwagi

- Podczas przypisywania zmiany licencji pole Stan w [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) ma wartość "oczekiwanie".

- Pole Stan jest aktualizowane co 15 minut.
