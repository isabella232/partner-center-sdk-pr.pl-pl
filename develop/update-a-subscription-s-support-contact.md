---
title: Aktualizowanie informacji kontaktowych pomocy technicznej subskrypcji
description: Jak zaktualizować kontakt pomocy technicznej subskrypcji do jednego z odsprzedawców z dodaną wartością partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c89f91fc9e89384a7be1237c08d7a9a1cfe3164
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530365"
---
# <a name="update-a-subscriptions-support-contact"></a>Aktualizowanie informacji kontaktowych pomocy technicznej subskrypcji

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak zaktualizować kontakt pomocy technicznej subskrypcji do jednego z odsprzedawców z dodaną wartością partnera.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

- Informacje o nowym kontaktie z pomocą techniczną: identyfikator dzierżawy, Microsoft Partner Network identyfikatora i nazwy. Kontakt z pomocą techniczną musi być jednym z odsprzedawców z wartością dodaną partnera.

## <a name="c"></a>C\#

Aby zaktualizować kontakt pomocy technicznej subskrypcji, należy najpierw utworzyć jego wystąpienia i wypełnić obiekt [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) nowymi wartościami. Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Następnie pobierz interfejs do operacji subskrypcji, wywołując metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji. Następnie użyj właściwości [**SupportContact,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) aby uzyskać interfejs do obsługi operacji kontaktowych. Na koniec wywołaj [**metodę Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) lub [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) za pomocą wypełnionego obiektu SupportContact, aby zaktualizować kontakt pomocy technicznej.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego **Samples, klasa:** UpdateSubscriptionSupportContact.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/supportcontact HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.

| Nazwa            | Typ   | Wymagane | Opis                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| identyfikator klienta     | ciąg | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.           |
| subscription-id | ciąg | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję wersji próbnej. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W treści żądania należy uwzględnić wypełniony zasób [SupportContact.](subscription-resources.md#supportcontact) Kontakt z pomocą techniczną musi być istniejącym odsprzedawcą z relacją z partnerem.

### <a name="request-example"></a>Przykład żądania

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SupportContact.](subscription-resources.md#supportcontact)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
