---
title: Aktualizowanie listy urządzeń za pomocą zasad
description: Jak zaktualizować listę urządzeń za pomocą zasad konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04c2ef33116335db40bd2934dc7e33d57f015097
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768377"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>Aktualizowanie listy urządzeń za pomocą zasad

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

Jak zaktualizować listę urządzeń za pomocą zasad konfiguracji dla określonego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator zasad.

- Identyfikatory urządzeń, które mają zostać zaktualizowane.

## <a name="c"></a>C\#

Aby zaktualizować listę urządzeń z określonymi zasadami konfiguracji, należy najpierw utworzyć wystąpienie [list/dotnet/API/System. Collections. Generic. list -1) typu [KeyValuePair/dotnet/API/System. Collections. Generic. KeyValuePair -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) i dodać zasady do zastosowania, jak pokazano w poniższym przykładzie kodu. Wymagany jest identyfikator zasad dla zasad.

Następnie utwórz listę obiektów [**urządzeń**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) , które mają zostać zaktualizowane przy użyciu zasad, określając identyfikator urządzenia i listę zawierającą zasady do zastosowania dla każdego urządzenia. Następnie Utwórz wystąpienie obiektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) i ustaw właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na listę obiektów urządzeń.

Aby przetworzyć żądanie aktualizacji zasad dotyczących urządzeń, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie. Następnie Pobierz Właściwość [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) , aby uzyskać interfejs do operacji zbierania urządzeń przez klienta. Na koniec Wywołaj metodę [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) z obiektem DevicePolicyUpdateRequest, aby zaktualizować urządzenia przy użyciu zasad.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdateDevicesPolicy.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **WYSŁANA** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/DevicePolicyUpdates http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania Użyj następujących parametrów ścieżki.

| Nazwa        | Typ   | Wymagane | Opis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać zasób [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) .

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu tego procesu wsadowego. Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
