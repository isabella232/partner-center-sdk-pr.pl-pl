---
title: Pobieranie listy urządzeń dla określonej partii i klienta
description: Jak pobrać kolekcję urządzeń i szczegóły urządzenia w określonej partii urządzeń dla klienta.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768241"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>Pobieranie listy urządzeń dla określonej partii i klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

W tym artykule opisano sposób pobierania kolekcji urządzeń w określonej partii urządzeń dla określonego klienta. Każdy zasób urządzenia zawiera szczegółowe informacje o urządzeniu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator partii urządzeń.

## <a name="c"></a>C\#

Aby pobrać kolekcję urządzeń w określonej partii urządzeń dla określonego klienta:

1. Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.

2. Wywołaj metodę [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) , aby uzyskać interfejs do operacji zbierania wsadowego na urządzeniu dla określonej partii.

3. Pobierz Właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) , aby uzyskać interfejs do operacji zbierania urządzeń dla partii.

4. Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) w celu pobrania kolekcji urządzeń.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Aby zapoznać się z przykładem, zobacz następujące tematy:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**
- Klasa: **GetDevices.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1 |

#### <a name="uri-parameters"></a>Parametry identyfikatora URI

Podczas tworzenia żądania Użyj następujących parametrów ścieżki.

| Nazwa           | Typ   | Wymagane | Opis                                           |
|----------------|--------|----------|-------------------------------------------------------|
| Identyfikator klienta    | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |
| devicebatch — identyfikator | ciąg | Tak      | Identyfikator ciągu, który identyfikuje partię urządzenia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli powodzenie, treść odpowiedzi zawiera stronicowaną kolekcję zasobów [urządzeń](device-deployment-resources.md#device) . Kolekcja zawiera 100 urządzeń na stronie. Aby pobrać następną stronę z 100 urządzeń, continuationToken w treści odpowiedzi musi być uwzględniony w następnym żądaniu jako nagłówek MS-ContinuationToken.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
