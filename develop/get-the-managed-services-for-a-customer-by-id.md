---
title: Pobieranie usług zarządzanych dla klienta według identyfikatora
description: Pobiera zarządzane usługi dla klienta. Innymi słowy, uzyskaj linki do wszystkich subskrypcji klienta, do których masz uprawnienia administratora delegowanego. Możesz użyć tych linków, aby zapewnić pomoc techniczną i żądania usług plików firmie Microsoft.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4764fce6a80035ea4b9dcc6677a3da28fc863eb7
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768409"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a>Pobieranie usług zarządzanych dla klienta według identyfikatora

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Pobiera zarządzane usługi dla klienta. Innymi słowy, uzyskaj linki do wszystkich subskrypcji klienta, do których masz uprawnienia administratora delegowanego. Możesz użyć tych linków, aby zapewnić pomoc techniczną i żądania usług plików firmie Microsoft.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby wyświetlić listę wszystkich usług zarządzanych dla klienta, Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Następnie Wywołaj Właściwość [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) , a następnie metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: CustomerManagedServices.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/managedservices http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby pobrać zarządzane usługi klienta.

| Nazwa                   | Typ     | Wymagane | Opis                           |
|------------------------|----------|----------|---------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Identyfikator GUID odpowiadający klientowi. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję obiektów **usługi zarządzanej** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
