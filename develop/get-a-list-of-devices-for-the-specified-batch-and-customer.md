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
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="8696e-103">Pobieranie listy urządzeń dla określonej partii i klienta</span><span class="sxs-lookup"><span data-stu-id="8696e-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="8696e-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="8696e-104">**Applies to:**</span></span>

- <span data-ttu-id="8696e-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="8696e-105">Partner Center</span></span>
- <span data-ttu-id="8696e-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="8696e-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8696e-107">W tym artykule opisano sposób pobierania kolekcji urządzeń w określonej partii urządzeń dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="8696e-107">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="8696e-108">Każdy zasób urządzenia zawiera szczegółowe informacje o urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="8696e-108">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8696e-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8696e-109">Prerequisites</span></span>

- <span data-ttu-id="8696e-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8696e-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8696e-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8696e-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8696e-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8696e-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8696e-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="8696e-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8696e-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="8696e-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8696e-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="8696e-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8696e-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="8696e-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8696e-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8696e-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8696e-118">Identyfikator partii urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8696e-118">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="8696e-119">C\#</span><span class="sxs-lookup"><span data-stu-id="8696e-119">C\#</span></span>

<span data-ttu-id="8696e-120">Aby pobrać kolekcję urządzeń w określonej partii urządzeń dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="8696e-120">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="8696e-121">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="8696e-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="8696e-122">Wywołaj metodę [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) , aby uzyskać interfejs do operacji zbierania wsadowego na urządzeniu dla określonej partii.</span><span class="sxs-lookup"><span data-stu-id="8696e-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="8696e-123">Pobierz Właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) , aby uzyskać interfejs do operacji zbierania urządzeń dla partii.</span><span class="sxs-lookup"><span data-stu-id="8696e-123">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="8696e-124">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) w celu pobrania kolekcji urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8696e-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="8696e-125">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="8696e-125">For an example, see the following:</span></span>

- <span data-ttu-id="8696e-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="8696e-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="8696e-127">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="8696e-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="8696e-128">Klasa: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="8696e-128">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="8696e-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8696e-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8696e-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8696e-130">Request syntax</span></span>

| <span data-ttu-id="8696e-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="8696e-131">Method</span></span>  | <span data-ttu-id="8696e-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8696e-132">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8696e-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="8696e-133">**GET**</span></span> | <span data-ttu-id="8696e-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="8696e-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8696e-135">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="8696e-135">URI parameters</span></span>

<span data-ttu-id="8696e-136">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="8696e-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="8696e-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8696e-137">Name</span></span>           | <span data-ttu-id="8696e-138">Typ</span><span class="sxs-lookup"><span data-stu-id="8696e-138">Type</span></span>   | <span data-ttu-id="8696e-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8696e-139">Required</span></span> | <span data-ttu-id="8696e-140">Opis</span><span class="sxs-lookup"><span data-stu-id="8696e-140">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8696e-141">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="8696e-141">customer-id</span></span>    | <span data-ttu-id="8696e-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="8696e-142">string</span></span> | <span data-ttu-id="8696e-143">Tak</span><span class="sxs-lookup"><span data-stu-id="8696e-143">Yes</span></span>      | <span data-ttu-id="8696e-144">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="8696e-144">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="8696e-145">devicebatch — identyfikator</span><span class="sxs-lookup"><span data-stu-id="8696e-145">devicebatch-id</span></span> | <span data-ttu-id="8696e-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="8696e-146">string</span></span> | <span data-ttu-id="8696e-147">Tak</span><span class="sxs-lookup"><span data-stu-id="8696e-147">Yes</span></span>      | <span data-ttu-id="8696e-148">Identyfikator ciągu, który identyfikuje partię urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8696e-148">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8696e-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8696e-149">Request headers</span></span>

<span data-ttu-id="8696e-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8696e-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8696e-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8696e-151">Request body</span></span>

<span data-ttu-id="8696e-152">Brak</span><span class="sxs-lookup"><span data-stu-id="8696e-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="8696e-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8696e-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8696e-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8696e-154">REST response</span></span>

<span data-ttu-id="8696e-155">Jeśli powodzenie, treść odpowiedzi zawiera stronicowaną kolekcję zasobów [urządzeń](device-deployment-resources.md#device) .</span><span class="sxs-lookup"><span data-stu-id="8696e-155">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="8696e-156">Kolekcja zawiera 100 urządzeń na stronie.</span><span class="sxs-lookup"><span data-stu-id="8696e-156">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="8696e-157">Aby pobrać następną stronę z 100 urządzeń, continuationToken w treści odpowiedzi musi być uwzględniony w następnym żądaniu jako nagłówek MS-ContinuationToken.</span><span class="sxs-lookup"><span data-stu-id="8696e-157">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8696e-158">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8696e-158">Response success and error codes</span></span>

<span data-ttu-id="8696e-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="8696e-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8696e-160">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8696e-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8696e-161">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8696e-161">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8696e-162">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8696e-162">Response example</span></span>

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
