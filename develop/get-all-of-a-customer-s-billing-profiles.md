---
title: Pobieranie profilu rozliczeniowego klienta
description: Pobiera profil rozliczeń dla klienta. Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6c837c1c220e334df82e75eb680b6012862c9686
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768362"
---
# <a name="get-a-customers-billing-profile"></a>Pobieranie profilu rozliczeniowego klienta

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Pobiera profil rozliczeń dla klienta.

Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md). Następnie w polu Nazwa klienta na lewym pasku bocznym wybierz pozycję **konto**. Profil rozliczeń można znaleźć w nagłówku **informacji dotyczących rachunku** .

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby uzyskać profil rozliczeń klienta, Użyj kolekcji [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Następnie Wywołaj Właściwość [**Profile**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) , a następnie właściwość [**rozliczenia**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) . Na koniec wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSamples **Klasa**: GetCustomerBillingProfile.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Profiles/Billing http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby uzyskać profil rozliczeń.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [profilu](profile-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
