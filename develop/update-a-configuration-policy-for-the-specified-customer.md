---
title: Aktualizowanie zasad konfiguracji dla określonego klienta
description: Jak zaktualizować określone zasady konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 42c57a92020723415b4621e9f9d7c5c3278bfb77
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505343"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Aktualizowanie zasad konfiguracji dla określonego klienta

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

Jak zaktualizować określone zasady konfiguracji dla określonego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator zasad.

## <a name="c"></a>C\#

Aby zaktualizować istniejące zasady konfiguracji dla określonego klienta, Utwórz wystąpienie nowego obiektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak pokazano w poniższym fragmencie kodu. Wartości w tym nowym obiekcie zastępują odpowiednie wartości w istniejącym obiekcie. Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie. Następnie Wywołaj metodę [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) z identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad. Na koniec Wywołaj metodę [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) lub [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) w celu zaktualizowania zasad konfiguracji.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdateConfigurationPolicy.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania Użyj następujących parametrów ścieżki.

| Nazwa        | Typ   | Wymagane | Opis                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.         |
| Identyfikator zasad   | ciąg | Tak      | Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje zasady do zaktualizowania. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać obiekt, który dostarcza informacje o zasadach.

| Nazwa            | Typ             | Wymagane | Zaktualizowa | Opis                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator              | ciąg           | Tak      | Nie        | Ciąg w formacie GUID, który identyfikuje zasady.                                                                                                    |
| name            | ciąg           | Tak      | Tak       | Przyjazna nazwa zasad.                                                                                                                         |
| category        | ciąg           | Tak      | Nie        | Kategoria zasad.                                                                                                                                     |
| description (opis)     | ciąg           | Nie       | Tak       | Opis zasad.                                                                                                                                  |
| devicesAssigned | liczba           | Nie       | Nie        | Liczba urządzeń.                                                                                                                                   |
| policySettings  | tablica ciągów | Tak      | Tak       | Ustawienia zasad: "none", "Usuń \_ \_ preinstalls OEM", "User OOBE \_ \_ nie \_ Local \_ admin", "Pomiń \_ Ustawienia ekspresowe \_ ", "Pomiń \_ rejestrację OEM" \_ , Pomiń \_ umowę EULA. |

### <a name="request-example"></a>Przykład żądania

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) dla nowych zasad.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
