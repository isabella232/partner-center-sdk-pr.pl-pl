---
title: Rejestrowanie subskrypcji
description: Zarejestruj istniejącą subskrypcję, aby umożliwić jej zamawianie rezerwacji platformy Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768309"
---
# <a name="register-a-subscription"></a>Rejestrowanie subskrypcji

**Dotyczy**

- Centrum partnerskie

Zarejestruj istniejącą [subskrypcję](subscription-resources.md) , aby umożliwić jej zamawianie rezerwacji platformy Azure.

Aby kupić rezerwację platformy Azure, musisz mieć co najmniej jedną istniejącą subskrypcję platformy Azure z dostawcą usług kryptograficznych. Ta metoda umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure w ramach dostawcy CSP i włączenie jej do kupowania rezerwacji platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby zarejestrować subskrypcję klienta, Pobierz interfejs do operacji subskrypcji, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta. Następnie Wywołaj metodę [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) z identyfikatorem subskrypcji, aby zidentyfikować rejestrację, która zostanie zarejestrowana.

Na koniec Wywołaj metodę **Registration. Register ()** w celu zarejestrowania subskrypcji i pobrania identyfikatora URI, którego można użyć do pobrania stanu rejestracji subskrypcji. Aby uzyskać więcej informacji, zobacz [pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO**  | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/registrations http/1.1 |

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
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
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

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu rejestracji subskrypcji. Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST. Aby zapoznać się z przykładem sposobu pobierania stanu, zobacz [pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md).

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
