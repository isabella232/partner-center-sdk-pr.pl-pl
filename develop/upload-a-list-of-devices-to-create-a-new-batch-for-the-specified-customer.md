---
title: Przekazywanie listy urządzeń w celu utworzenia nowej partii dla określonego klienta
description: Jak przesłać listę informacji o urządzeniach, aby utworzyć nową partię dla określonego klienta. Spowoduje to utworzenie partii urządzeń do rejestracji w ramach wdrożenia bez dotknięcia i skojarzenie urządzeń i partii urządzeń z określonym klientem.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b48971b862418136c42e78ae973a5aea27404a1
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768366"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>Przekazywanie listy urządzeń w celu utworzenia nowej partii dla określonego klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

Jak przesłać listę informacji o urządzeniach, aby utworzyć nową partię dla określonego klienta. Spowoduje to utworzenie partii urządzeń do rejestracji w ramach wdrożenia bez dotknięcia i skojarzenie urządzeń i partii urządzeń z określonym klientem.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika. Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Lista zasobów urządzeń, które zawierają informacje o poszczególnych urządzeniach.

## <a name="c"></a>C\#

Aby przesłać listę urządzeń w celu utworzenia nowej partii urządzeń:

1. Utwórz wystąpienie nowego elementu [list/dotnet/API/System. Collections. Generic. list -1) typu [**urządzenie**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) i wypełnij listę urządzeniami. Następujące kombinacje wypełnionych właściwości są wymagane co najmniej do identyfikowania poszczególnych urządzeń:

   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - Tylko [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .
   - Tylko [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .
   - Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

2. Utwórz wystąpienie obiektu [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) i ustaw właściwość [**Identyfikator partii**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) na unikatową wybraną nazwę i Właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na liście urządzeń do przekazania.

3. Przetwórz żądanie tworzenia wsadowego urządzeń, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu pobrania interfejsu do operacji na określonym kliencie.

4. Wywołaj metodę [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) z żądaniem tworzenia wsadowego urządzenia, aby utworzyć partię.

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateDeviceBatch.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania Użyj następujących parametrów ścieżki.

| Nazwa        | Typ   | Wymagane | Opis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| Identyfikator klienta | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Treść żądania musi zawierać zasób [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) .

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu przekazywania urządzenia. Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

#### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
