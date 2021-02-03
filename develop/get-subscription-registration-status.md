---
title: Pobieranie stanu rejestracji subskrypcji
description: Pobierz stan subskrypcji, która została zarejestrowana do użycia z Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768441"
---
# <a name="get-subscription-registration-status"></a>Pobieranie stanu rejestracji subskrypcji

**Dotyczy**

- Centrum partnerskie

Jak uzyskać informacje o stanie rejestracji subskrypcji klienta, dla którego włączono kupowanie Azure Reserved VM Instances.

Aby kupić wystąpienie zarezerwowane maszyny wirtualnej platformy Azure przy użyciu interfejsu API Centrum partnerskiego, musisz mieć co najmniej jedną subskrypcję platformy Azure dla dostawcy CSP. Metoda [zarejestruj subskrypcję](register-a-subscription.md) umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure w ramach dostawcy CSP i włączenie jej do Azure Reserved VM Instances zakupów. Ta metoda umożliwia pobranie stanu rejestracji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby uzyskać stan rejestracji subskrypcji, Zacznij od użycia metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) przy użyciu identyfikatora subskrypcji, aby zidentyfikować subskrypcję. Następnie użyj właściwości RegistrationStatus, aby uzyskać interfejs do operacji stanu rejestracji bieżącej subskrypcji, i Wywołaj metodę **Get** lub **GetAsync** , aby pobrać obiekt **SubscriptionRegistrationStatus** .

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
| **Pobierz**  | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/registrationstatus http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.

| Nazwa                    | Typ       | Wymagane | Opis                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| Identyfikator klienta             | ciąg     | Tak      | Ciąg w formacie GUID, który identyfikuje klienta.         |
| Identyfikator subskrypcji         | ciąg     | Tak      | Ciąg w formacie GUID, który identyfikuje subskrypcję.     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

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
