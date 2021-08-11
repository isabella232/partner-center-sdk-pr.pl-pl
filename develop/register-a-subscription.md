---
title: Rejestrowanie subskrypcji
description: Zarejestruj istniejącą subskrypcję, aby umożliwić jej zamawianie rezerwacji platformy Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4ea2183ab0c2367c7772bdf40b5988c2b7eff7c539686760332bec4addda8bbe
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997196"
---
# <a name="register-a-subscription"></a>Rejestrowanie subskrypcji

Zarejestruj istniejącą [subskrypcję,](subscription-resources.md) aby umożliwić jej zamawianie rezerwacji platformy Azure.

Aby kupić rezerwację platformy Azure, musisz mieć co najmniej jedną istniejącą subskrypcję platformy Azure dla programu CSP. Ta metoda umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure dla programu CSP, co umożliwia zakup rezerwacji platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby zarejestrować subskrypcję klienta, pobierz interfejs do operacji subskrypcji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta. Następnie wywołaj metodę [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) z identyfikatorem subskrypcji, aby zidentyfikować rejestrowany subskrypcję.

Na koniec wywołaj metodę **Registration.Register(),** aby zarejestrować subskrypcję i pobrać jej kod URI, który może służyć do uzyskania stanu rejestracji subskrypcji. Aby uzyskać więcej informacji, zobacz Get subscription registration status (Uzyskiwanie [stanu rejestracji subskrypcji).](get-subscription-registration-status.md)

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
| **Post**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/registrations HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.

| Nazwa                    | Typ       | Wymagane | Opis                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| identyfikator klienta             | ciąg     | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.         |
| subscription-id         | ciąg     | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję.     |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** (Lokalizacja) z URI, który może służyć do pobierania stanu rejestracji subskrypcji. Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST. Aby uzyskać przykład sposobu pobierania stanu, zobacz [Pobieranie stanu rejestracji subskrypcji.](get-subscription-registration-status.md)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
