---
title: Pobieranie stanu przekazywania wsadowego urządzeń
description: Jak uzyskać stan przekazywania wsadowego urządzenia do określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fb887ba257d6fbe68f95ae4b59d701ac4c934860
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768405"
---
# <a name="get-the-status-of-a-device-batch-upload"></a>Pobieranie stanu przekazywania wsadowego urządzeń

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

Jak uzyskać stan przekazywania wsadowego urządzenia do określonego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator śledzenia partii zwrócony w nagłówku lokalizacji podczas przesyłania wsadowego urządzenia. Aby uzyskać więcej informacji, zobacz [przekazywanie listy urządzeń dla określonego klienta](upload-a-list-of-devices-for-the-specified-customer.md).

## <a name="c"></a>C\#

Aby uzyskać stan przekazywania wsadowego urządzeń, najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie. Następnie Wywołaj metodę [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) z identyfikatorem śledzenia partii, aby uzyskać interfejs do przetwarzania wsadowego operacji przekazywania. Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) , aby pobrać stan.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetBatchUploadStatus.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podczas tworzenia żądania Użyj następujących parametrów ścieżki.

| Nazwa             | Typ   | Wymagane | Opis                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Identyfikator klienta      | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.                                                                                                                          |
| batchtracking — identyfikator | ciąg | Tak      | Identyfikator GUID, który jest używany do pobierania stanu przekazywania wsadowego urządzenia. Ten identyfikator jest zwracany w nagłówku lokalizacji po pomyślnym przesłaniu partii urządzeń. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zawiera zasób [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
