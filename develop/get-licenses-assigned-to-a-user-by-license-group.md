---
title: Pobieranie licencji przypisanych do użytkownika według grupy licencji
description: Jak uzyskać listę licencji przypisanych do użytkowników dla określonych grup licencji.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 28c10e3e2acb30e4110213344959a87d4ddfcffb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768321"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a>Pobieranie licencji przypisanych do użytkownika według grupy licencji

**Dotyczy**

- Centrum partnerskie

Jak uzyskać listę licencji przypisanych do użytkowników dla określonych grup licencji.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator użytkownika.

- Lista co najmniej jednego z identyfikatorów grup licencji.

## <a name="c"></a>C\#

Aby sprawdzić, które licencje są przypisane do użytkownika z określonych grup licencji, Zacznij od utworzenia wystąpienia [list/dotnet/API/System. Collections. Generic. list -1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), a następnie Dodaj do listy grupy licencji. Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta. Następnie Wywołaj metodę user [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika, aby zidentyfikować użytkownika. Następnie uzyskaj interfejs do operacji licencji użytkownika klienta na podstawie właściwości [**licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) . Na koniec Przekaż listę grup licencji do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) , aby pobrać kolekcję licencji przypisanych do użytkownika.

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses? LicenseGroupIds = grupa1 http/1.1                        |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses? LicenseGroupIds = group2 http/1.1                        |
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses? LicenseGroupIds = grupa1&LicenseGroupIds = group2 http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującej ścieżki i parametrów zapytania, aby zidentyfikować klientów, użytkowników i grupy licencji.

| Nazwa            | Typ   | Wymagane | Opis                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Identyfikator klienta     | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje klienta.                                                                                                                                                                                                                 |
| user-id         | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje użytkownika.                                                                                                                                                                                                                     |
| licenseGroupIds | ciąg | Nie       | Wartość wyliczenia wskazująca grupę licencji przypisanych licencji. Prawidłowe wartości: grupa1, group2 grupa1 — ta grupa zawiera wszystkie produkty, których licencja może być zarządzana w Azure Active Directory (AAD). Group2 — ta grupa ma tylko Minecraft licencje na produkty. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [licencji](license-resources.md#license) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-licenses-found"></a>Przykład odpowiedzi (nie znaleziono pasujących licencji)

Jeśli nie można znaleźć pasujących licencji dla określonych grup licencji, odpowiedź zawiera pustą kolekcję z elementem totalCount, którego wartość wynosi 0.

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
