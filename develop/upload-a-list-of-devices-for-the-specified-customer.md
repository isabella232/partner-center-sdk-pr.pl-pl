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
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="40c1c-104">Przekazywanie listy urządzeń do istniejącej partii dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="40c1c-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="40c1c-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="40c1c-105">**Applies To**</span></span>

- <span data-ttu-id="40c1c-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="40c1c-106">Partner Center</span></span>
- <span data-ttu-id="40c1c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="40c1c-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="40c1c-108">Jak przekazać listę informacji o urządzeniach do istniejącej partii dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="40c1c-108">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="40c1c-109">Spowoduje to skojarzenie urządzeń z już utworzoną grupą urządzeń.</span><span class="sxs-lookup"><span data-stu-id="40c1c-109">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40c1c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="40c1c-110">Prerequisites</span></span>

- <span data-ttu-id="40c1c-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="40c1c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="40c1c-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40c1c-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="40c1c-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40c1c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="40c1c-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="40c1c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="40c1c-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="40c1c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="40c1c-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="40c1c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="40c1c-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="40c1c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="40c1c-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40c1c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="40c1c-119">Identyfikator partii urządzeń.</span><span class="sxs-lookup"><span data-stu-id="40c1c-119">The device batch identifier.</span></span>

- <span data-ttu-id="40c1c-120">Lista zasobów urządzeń, które zawierają informacje o poszczególnych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="40c1c-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="40c1c-121">C\#</span><span class="sxs-lookup"><span data-stu-id="40c1c-121">C\#</span></span>

<span data-ttu-id="40c1c-122">Aby przekazać listę urządzeń do istniejącej partii urządzeń, najpierw Utwórz wystąpienie nowego pliku [list/dotnet/API/System. Collections. Generic. list -1) typu [**urządzenie**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) i wypełnij listę urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="40c1c-122">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="40c1c-123">Następujące kombinacje wypełnionych właściwości są wymagane co najmniej do identyfikowania poszczególnych urządzeń:</span><span class="sxs-lookup"><span data-stu-id="40c1c-123">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="40c1c-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="40c1c-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="40c1c-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="40c1c-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="40c1c-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="40c1c-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="40c1c-127">Tylko [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="40c1c-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="40c1c-128">Tylko [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="40c1c-128">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="40c1c-129">Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="40c1c-129">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="40c1c-130">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="40c1c-130">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="40c1c-131">Następnie Wywołaj metodę [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) z identyfikatorem partii urządzeń, aby uzyskać interfejs do operacji dla określonej partii.</span><span class="sxs-lookup"><span data-stu-id="40c1c-131">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="40c1c-132">Na koniec Wywołaj metodę [**Devices. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) z listą urządzeń, aby dodać urządzenia do partii urządzeń.</span><span class="sxs-lookup"><span data-stu-id="40c1c-132">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

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

<span data-ttu-id="40c1c-133">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="40c1c-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="40c1c-134">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateDevices.cs</span><span class="sxs-lookup"><span data-stu-id="40c1c-134">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="40c1c-135">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="40c1c-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="40c1c-136">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="40c1c-136">Request syntax</span></span>

| <span data-ttu-id="40c1c-137">Metoda</span><span class="sxs-lookup"><span data-stu-id="40c1c-137">Method</span></span>   | <span data-ttu-id="40c1c-138">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="40c1c-138">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40c1c-139">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="40c1c-139">**POST**</span></span> | <span data-ttu-id="40c1c-140">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="40c1c-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="40c1c-141">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="40c1c-141">URI parameter</span></span>

<span data-ttu-id="40c1c-142">Podczas tworzenia żądania Użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="40c1c-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="40c1c-143">Nazwa</span><span class="sxs-lookup"><span data-stu-id="40c1c-143">Name</span></span>           | <span data-ttu-id="40c1c-144">Typ</span><span class="sxs-lookup"><span data-stu-id="40c1c-144">Type</span></span>   | <span data-ttu-id="40c1c-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="40c1c-145">Required</span></span> | <span data-ttu-id="40c1c-146">Opis</span><span class="sxs-lookup"><span data-stu-id="40c1c-146">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="40c1c-147">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="40c1c-147">customer-id</span></span>    | <span data-ttu-id="40c1c-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="40c1c-148">string</span></span> | <span data-ttu-id="40c1c-149">Tak</span><span class="sxs-lookup"><span data-stu-id="40c1c-149">Yes</span></span>      | <span data-ttu-id="40c1c-150">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="40c1c-150">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="40c1c-151">devicebatch — identyfikator</span><span class="sxs-lookup"><span data-stu-id="40c1c-151">devicebatch-id</span></span> | <span data-ttu-id="40c1c-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="40c1c-152">string</span></span> | <span data-ttu-id="40c1c-153">Tak</span><span class="sxs-lookup"><span data-stu-id="40c1c-153">Yes</span></span>      | <span data-ttu-id="40c1c-154">Identyfikator ciągu, który identyfikuje partię urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40c1c-154">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="40c1c-155">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="40c1c-155">Request headers</span></span>

<span data-ttu-id="40c1c-156">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="40c1c-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="40c1c-157">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="40c1c-157">Request body</span></span>

<span data-ttu-id="40c1c-158">Treść żądania musi zawierać tablicę obiektów [urządzeń](device-deployment-resources.md#device) .</span><span class="sxs-lookup"><span data-stu-id="40c1c-158">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="40c1c-159">Następujące kombinacje pól do identyfikacji urządzenia są akceptowane:</span><span class="sxs-lookup"><span data-stu-id="40c1c-159">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="40c1c-160">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="40c1c-160">hardwareHash + productKey.</span></span>
- <span data-ttu-id="40c1c-161">hardwareHash + numer seryjny.</span><span class="sxs-lookup"><span data-stu-id="40c1c-161">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="40c1c-162">hardwareHash + productKey + numer seryjny.</span><span class="sxs-lookup"><span data-stu-id="40c1c-162">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="40c1c-163">tylko hardwareHash.</span><span class="sxs-lookup"><span data-stu-id="40c1c-163">hardwareHash only.</span></span>
- <span data-ttu-id="40c1c-164">tylko productKey.</span><span class="sxs-lookup"><span data-stu-id="40c1c-164">productKey only.</span></span>
- <span data-ttu-id="40c1c-165">Numer seryjny i oemManufacturerName + ModelName.</span><span class="sxs-lookup"><span data-stu-id="40c1c-165">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="40c1c-166">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="40c1c-166">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="40c1c-167">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="40c1c-167">REST response</span></span>

<span data-ttu-id="40c1c-168">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu przekazywania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40c1c-168">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="40c1c-169">Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="40c1c-169">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="40c1c-170">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40c1c-170">Response success and error codes</span></span>

<span data-ttu-id="40c1c-171">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="40c1c-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="40c1c-172">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="40c1c-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="40c1c-173">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="40c1c-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="40c1c-174">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40c1c-174">Response example</span></span>

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
