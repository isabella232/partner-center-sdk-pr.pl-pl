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
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="f784a-103">Pobieranie listy urządzeń dla określonej partii i klienta</span><span class="sxs-lookup"><span data-stu-id="f784a-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="f784a-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="f784a-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f784a-105">W tym artykule opisano sposób pobierania kolekcji urządzeń w określonej partii urządzeń dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="f784a-105">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="f784a-106">Każdy zasób urządzenia zawiera szczegółowe informacje o urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="f784a-106">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f784a-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f784a-107">Prerequisites</span></span>

- <span data-ttu-id="f784a-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f784a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f784a-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f784a-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f784a-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f784a-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f784a-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f784a-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f784a-112">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="f784a-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f784a-113">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="f784a-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f784a-114">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="f784a-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f784a-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f784a-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f784a-116">Identyfikator wsadu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f784a-116">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="f784a-117">C\#</span><span class="sxs-lookup"><span data-stu-id="f784a-117">C\#</span></span>

<span data-ttu-id="f784a-118">Aby pobrać kolekcję urządzeń w określonej partii urządzeń dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="f784a-118">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="f784a-119">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="f784a-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="f784a-120">Wywołaj [**metodę DeviceBatches.ById,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) aby uzyskać interfejs dla operacji zbierania wsadowego urządzeń dla określonej partii.</span><span class="sxs-lookup"><span data-stu-id="f784a-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="f784a-121">Pobierz właściwość [**Urządzenia,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) aby uzyskać interfejs do operacji zbierania urządzeń dla partii.</span><span class="sxs-lookup"><span data-stu-id="f784a-121">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="f784a-122">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) aby pobrać kolekcję urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f784a-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="f784a-123">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="f784a-123">For an example, see the following:</span></span>

- <span data-ttu-id="f784a-124">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f784a-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f784a-125">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="f784a-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="f784a-126">Klasa: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="f784a-126">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f784a-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f784a-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f784a-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f784a-128">Request syntax</span></span>

| <span data-ttu-id="f784a-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="f784a-129">Method</span></span>  | <span data-ttu-id="f784a-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f784a-130">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f784a-131">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f784a-131">**GET**</span></span> | <span data-ttu-id="f784a-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f784a-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f784a-133">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="f784a-133">URI parameters</span></span>

<span data-ttu-id="f784a-134">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="f784a-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="f784a-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f784a-135">Name</span></span>           | <span data-ttu-id="f784a-136">Typ</span><span class="sxs-lookup"><span data-stu-id="f784a-136">Type</span></span>   | <span data-ttu-id="f784a-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f784a-137">Required</span></span> | <span data-ttu-id="f784a-138">Opis</span><span class="sxs-lookup"><span data-stu-id="f784a-138">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="f784a-139">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="f784a-139">customer-id</span></span>    | <span data-ttu-id="f784a-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="f784a-140">string</span></span> | <span data-ttu-id="f784a-141">Tak</span><span class="sxs-lookup"><span data-stu-id="f784a-141">Yes</span></span>      | <span data-ttu-id="f784a-142">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="f784a-142">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="f784a-143">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="f784a-143">devicebatch-id</span></span> | <span data-ttu-id="f784a-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="f784a-144">string</span></span> | <span data-ttu-id="f784a-145">Tak</span><span class="sxs-lookup"><span data-stu-id="f784a-145">Yes</span></span>      | <span data-ttu-id="f784a-146">Identyfikator ciągu identyfikujący partię urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f784a-146">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f784a-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f784a-147">Request headers</span></span>

<span data-ttu-id="f784a-148">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f784a-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f784a-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f784a-149">Request body</span></span>

<span data-ttu-id="f784a-150">Brak</span><span class="sxs-lookup"><span data-stu-id="f784a-150">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f784a-151">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f784a-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f784a-152">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f784a-152">REST response</span></span>

<span data-ttu-id="f784a-153">Jeśli to się powiedzie, treść odpowiedzi zawiera stronicową kolekcję [zasobów](device-deployment-resources.md#device) urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f784a-153">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="f784a-154">Kolekcja zawiera 100 urządzeń na stronie.</span><span class="sxs-lookup"><span data-stu-id="f784a-154">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="f784a-155">Aby pobrać następną stronę 100 urządzeń, token continuationToken w treści odpowiedzi musi zostać uwzględniony w kolejnym żądaniu jako MS-ContinuationToken nagłówka.</span><span class="sxs-lookup"><span data-stu-id="f784a-155">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f784a-156">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f784a-156">Response success and error codes</span></span>

<span data-ttu-id="f784a-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="f784a-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f784a-158">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f784a-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f784a-159">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f784a-159">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f784a-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f784a-160">Response example</span></span>

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
