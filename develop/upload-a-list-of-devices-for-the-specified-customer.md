---
title: Przekazywanie listy urządzeń do istniejącej partii dla określonego klienta
description: Jak przekazać listę informacji o urządzeniach do istniejącej partii dla określonego klienta. Spowoduje to skojarzenie urządzeń z już utworzoną grupą urządzeń.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d01ac1a42c50416487167070be9d104562300baf
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768370"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>Przekazywanie listy urządzeń do istniejącej partii dla określonego klienta

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

Jak przekazać listę informacji o urządzeniach do istniejącej partii dla określonego klienta. Spowoduje to skojarzenie urządzeń z już utworzoną grupą urządzeń.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator partii urządzeń.

- Lista zasobów urządzeń, które zawierają informacje o poszczególnych urządzeniach.

## <a name="c"></a>C\#

Aby przekazać listę urządzeń do istniejącej partii urządzeń, najpierw Utwórz wystąpienie nowego pliku [list/dotnet/API/System. Collections. Generic. list -1) typu [**urządzenie**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) i wypełnij listę urządzeniami. Następujące kombinacje wypełnionych właściwości są wymagane co najmniej do identyfikowania poszczególnych urządzeń:

- [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).

- [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- Tylko [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .

- Tylko [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .

- Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie. Następnie Wywołaj metodę [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) z identyfikatorem partii urządzeń, aby uzyskać interfejs do operacji dla określonej partii. Na koniec Wywołaj metodę [**Devices. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) z listą urządzeń, aby dodać urządzenia do partii urządzeń.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateDevices.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania Użyj następującej ścieżki i parametrów zapytania.

| Nazwa           | Typ   | Wymagane | Opis                                           |
|----------------|--------|----------|-------------------------------------------------------|
| Identyfikator klienta    | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |
| devicebatch — identyfikator | ciąg | Tak      | Identyfikator ciągu, który identyfikuje partię urządzenia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać tablicę obiektów [urządzeń](device-deployment-resources.md#device) . Następujące kombinacje pól do identyfikacji urządzenia są akceptowane:

- hardwareHash + productKey.
- hardwareHash + numer seryjny.
- hardwareHash + productKey + numer seryjny.
- tylko hardwareHash.
- tylko productKey.
- Numer seryjny i oemManufacturerName + ModelName.

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu przekazywania urządzenia. Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
