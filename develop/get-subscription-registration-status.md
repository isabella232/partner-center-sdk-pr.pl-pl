---
title: Pobieranie stanu rejestracji subskrypcji
description: Uzyskaj stan subskrypcji, która została zarejestrowana do użycia z Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e0a65abba94f1f05a98282fa67ff1d185ba4e082488d2d7887b4e9346c38967
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989665"
---
# <a name="get-subscription-registration-status"></a>Pobieranie stanu rejestracji subskrypcji

Jak uzyskać stan rejestracji subskrypcji dla subskrypcji klienta, dla których włączono obsługę zakupu Azure Reserved VM Instances.

Aby kupić wystąpienie zarezerwowane maszyny wirtualnej platformy Azure przy użyciu interfejsu API Partner Center, musisz mieć co najmniej jedną istniejącą subskrypcję platformy Azure dostawcy usług w chmurze. Metoda [Rejestrowania subskrypcji](register-a-subscription.md) umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure w programie CSP, umożliwiając jej zakup Azure Reserved VM Instances. Ta metoda umożliwia pobranie stanu tej rejestracji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby uzyskać stan rejestracji subskrypcji, zacznij od użycia metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta. Następnie pobierz interfejs do operacji subskrypcji, wywołując metodę [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) z identyfikatorem subskrypcji w celu zidentyfikowania subskrypcji. Następnie użyj właściwości RegistrationStatus, aby uzyskać interfejs do operacji stanu rejestracji bieżącej subskrypcji, i wywołaj metodę **Get** lub **GetAsync,** aby pobrać obiekt **SubscriptionRegistrationStatus.**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.

| Nazwa                    | Typ       | Wymagane | Opis                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| identyfikator klienta             | ciąg     | Tak      | Ciąg sformatowany przy pomocy identyfikatora GUID, który identyfikuje klienta.         |
| subscription-id         | ciąg     | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje subskrypcję.     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SubscriptionRegistrationStatus.](subscription-resources.md#subscriptionregistrationstatus)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
