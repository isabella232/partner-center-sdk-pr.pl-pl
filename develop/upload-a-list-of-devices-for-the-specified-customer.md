---
title: Przekazywanie listy urządzeń do istniejącej partii dla określonego klienta
description: Jak przekazać listę informacji o urządzeniach do istniejącej partii dla określonego klienta. To skojarzy urządzenia z już utworzoną partią urządzeń.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3fa9cff39113130c54cecfaef1f8ca28e0ac5adf
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530314"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="8b72e-104">Przekazywanie listy urządzeń do istniejącej partii dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="8b72e-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="8b72e-105">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="8b72e-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8b72e-106">Jak przekazać listę informacji o urządzeniach do istniejącej partii dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="8b72e-106">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="8b72e-107">To skojarzy urządzenia z już utworzoną partią urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8b72e-107">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b72e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b72e-108">Prerequisites</span></span>

- <span data-ttu-id="8b72e-109">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8b72e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8b72e-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b72e-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8b72e-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8b72e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8b72e-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="8b72e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8b72e-113">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="8b72e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8b72e-114">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="8b72e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8b72e-115">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="8b72e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8b72e-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8b72e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8b72e-117">Identyfikator wsadu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8b72e-117">The device batch identifier.</span></span>

- <span data-ttu-id="8b72e-118">Lista zasobów urządzeń, które zawierają informacje o poszczególnych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="8b72e-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="8b72e-119">C\#</span><span class="sxs-lookup"><span data-stu-id="8b72e-119">C\#</span></span>

<span data-ttu-id="8b72e-120">Aby przekazać listę urządzeń do istniejącej partii urządzeń, najpierw należy utworzyć nowe wystąpienia typu [List/dotnet/api/system.collections.generic.list-1) typu [**Urządzenie**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) i wypełnić listę urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="8b72e-120">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="8b72e-121">Następujące kombinacje wypełnionych właściwości są wymagane co najmniej do identyfikowania poszczególnych urządzeń:</span><span class="sxs-lookup"><span data-stu-id="8b72e-121">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="8b72e-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)( Klucz produktu).</span><span class="sxs-lookup"><span data-stu-id="8b72e-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="8b72e-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Numer seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="8b72e-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="8b72e-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Klucz produktu)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Numer seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="8b72e-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="8b72e-125">[**Tylko sprzętHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)</span><span class="sxs-lookup"><span data-stu-id="8b72e-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="8b72e-126">[**Tylko ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="8b72e-126">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="8b72e-127">[**Numer seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Nazwa modelu**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="8b72e-127">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="8b72e-128">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="8b72e-128">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="8b72e-129">Następnie wywołaj [**metodę DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) z identyfikatorem wsadowym urządzenia, aby uzyskać interfejs do operacji dla określonej partii.</span><span class="sxs-lookup"><span data-stu-id="8b72e-129">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="8b72e-130">Na koniec wywołaj [**metodę Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) z listą urządzeń, aby dodać urządzenia do partii urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8b72e-130">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

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

<span data-ttu-id="8b72e-131">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b72e-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8b72e-132">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: CreateDevices.cs</span><span class="sxs-lookup"><span data-stu-id="8b72e-132">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8b72e-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8b72e-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8b72e-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8b72e-134">Request syntax</span></span>

| <span data-ttu-id="8b72e-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="8b72e-135">Method</span></span>   | <span data-ttu-id="8b72e-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8b72e-136">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b72e-137">**Post**</span><span class="sxs-lookup"><span data-stu-id="8b72e-137">**POST**</span></span> | <span data-ttu-id="8b72e-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8b72e-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8b72e-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8b72e-139">URI parameter</span></span>

<span data-ttu-id="8b72e-140">Podczas tworzenia żądania użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="8b72e-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="8b72e-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8b72e-141">Name</span></span>           | <span data-ttu-id="8b72e-142">Typ</span><span class="sxs-lookup"><span data-stu-id="8b72e-142">Type</span></span>   | <span data-ttu-id="8b72e-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8b72e-143">Required</span></span> | <span data-ttu-id="8b72e-144">Opis</span><span class="sxs-lookup"><span data-stu-id="8b72e-144">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8b72e-145">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="8b72e-145">customer-id</span></span>    | <span data-ttu-id="8b72e-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="8b72e-146">string</span></span> | <span data-ttu-id="8b72e-147">Tak</span><span class="sxs-lookup"><span data-stu-id="8b72e-147">Yes</span></span>      | <span data-ttu-id="8b72e-148">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="8b72e-148">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="8b72e-149">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="8b72e-149">devicebatch-id</span></span> | <span data-ttu-id="8b72e-150">ciąg</span><span class="sxs-lookup"><span data-stu-id="8b72e-150">string</span></span> | <span data-ttu-id="8b72e-151">Tak</span><span class="sxs-lookup"><span data-stu-id="8b72e-151">Yes</span></span>      | <span data-ttu-id="8b72e-152">Identyfikator ciągu identyfikujący partię urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8b72e-152">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8b72e-153">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8b72e-153">Request headers</span></span>

<span data-ttu-id="8b72e-154">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8b72e-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8b72e-155">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8b72e-155">Request body</span></span>

<span data-ttu-id="8b72e-156">Treść żądania musi zawierać tablicę [obiektów](device-deployment-resources.md#device) Device.</span><span class="sxs-lookup"><span data-stu-id="8b72e-156">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="8b72e-157">Akceptowane są następujące kombinacje pól w celu zidentyfikowania urządzenia:</span><span class="sxs-lookup"><span data-stu-id="8b72e-157">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="8b72e-158">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="8b72e-158">hardwareHash + productKey.</span></span>
- <span data-ttu-id="8b72e-159">hardwareHash + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="8b72e-159">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="8b72e-160">hardwareHash + productKey + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="8b72e-160">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="8b72e-161">hardwareHash tylko.</span><span class="sxs-lookup"><span data-stu-id="8b72e-161">hardwareHash only.</span></span>
- <span data-ttu-id="8b72e-162">Tylko klucz productKey.</span><span class="sxs-lookup"><span data-stu-id="8b72e-162">productKey only.</span></span>
- <span data-ttu-id="8b72e-163">serialNumber + oemManufacturerName + modelName.</span><span class="sxs-lookup"><span data-stu-id="8b72e-163">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="8b72e-164">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8b72e-164">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8b72e-165">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8b72e-165">REST response</span></span>

<span data-ttu-id="8b72e-166">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** (Lokalizacja) z polem URI, który może służyć do pobierania stanu przekazywania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8b72e-166">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="8b72e-167">Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="8b72e-167">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8b72e-168">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b72e-168">Response success and error codes</span></span>

<span data-ttu-id="8b72e-169">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8b72e-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8b72e-170">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8b72e-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8b72e-171">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8b72e-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8b72e-172">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b72e-172">Response example</span></span>

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
