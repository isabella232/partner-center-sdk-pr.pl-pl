---
title: Pobieranie listy urządzeń dla określonej partii i klienta
description: Sposób pobierania kolekcji urządzeń i szczegółów urządzenia w określonej partii urządzeń dla klienta.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 28af1f568f755ba4c50cfac21529d6c677656c8e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874265"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>Pobieranie listy urządzeń dla określonej partii i klienta

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany

W tym artykule opisano sposób pobierania kolekcji urządzeń w określonej partii urządzeń dla określonego klienta. Każdy zasób urządzenia zawiera szczegółowe informacje o urządzeniu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator wsadu urządzenia.

## <a name="c"></a>C\#

Aby pobrać kolekcję urządzeń w określonej partii urządzeń dla określonego klienta:

1. Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.

2. Wywołaj [**metodę DeviceBatches.ById,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) aby uzyskać interfejs dla operacji zbierania wsadowego urządzeń dla określonej partii.

3. Pobierz właściwość [**Urządzenia,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) aby uzyskać interfejs do operacji zbierania urządzeń dla partii.

4. Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) aby pobrać kolekcję urządzeń.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Przykład można znaleźć w następujących tematach:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Project: **zestaw SDK Centrum partnerskiego przykłady**
- Klasa: **GetDevices.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Podczas tworzenia żądania użyj następujących parametrów ścieżki.

| Nazwa           | Typ   | Wymagane | Opis                                           |
|----------------|--------|----------|-------------------------------------------------------|
| identyfikator klienta    | ciąg | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta. |
| devicebatch-id | ciąg | Tak      | Identyfikator ciągu identyfikujący partię urządzenia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera stronicową kolekcję [zasobów](device-deployment-resources.md#device) urządzenia. Kolekcja zawiera 100 urządzeń na stronie. Aby pobrać następną stronę 100 urządzeń, token continuationToken w treści odpowiedzi musi zostać uwzględniony w kolejnym żądaniu jako MS-ContinuationToken nagłówka.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

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
