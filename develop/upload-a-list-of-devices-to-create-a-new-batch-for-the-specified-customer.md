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
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="303fc-104">Przekazywanie listy urządzeń w celu utworzenia nowej partii dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="303fc-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="303fc-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="303fc-105">**Applies to:**</span></span>

- <span data-ttu-id="303fc-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="303fc-106">Partner Center</span></span>
- <span data-ttu-id="303fc-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="303fc-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="303fc-108">Jak przesłać listę informacji o urządzeniach, aby utworzyć nową partię dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="303fc-108">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="303fc-109">Spowoduje to utworzenie partii urządzeń do rejestracji w ramach wdrożenia bez dotknięcia i skojarzenie urządzeń i partii urządzeń z określonym klientem.</span><span class="sxs-lookup"><span data-stu-id="303fc-109">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="303fc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="303fc-110">Prerequisites</span></span>

- <span data-ttu-id="303fc-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="303fc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="303fc-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="303fc-112">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="303fc-113">Postępuj zgodnie z [bezpiecznym modelem aplikacji](enable-secure-app-model.md) podczas korzystania z aplikacji i uwierzytelniania użytkowników za pomocą interfejsów API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="303fc-113">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="303fc-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="303fc-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="303fc-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="303fc-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="303fc-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="303fc-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="303fc-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="303fc-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="303fc-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="303fc-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="303fc-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="303fc-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="303fc-120">Lista zasobów urządzeń, które zawierają informacje o poszczególnych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="303fc-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="303fc-121">C\#</span><span class="sxs-lookup"><span data-stu-id="303fc-121">C\#</span></span>

<span data-ttu-id="303fc-122">Aby przesłać listę urządzeń w celu utworzenia nowej partii urządzeń:</span><span class="sxs-lookup"><span data-stu-id="303fc-122">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="303fc-123">Utwórz wystąpienie nowego elementu [list/dotnet/API/System. Collections. Generic. list -1) typu [**urządzenie**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) i wypełnij listę urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="303fc-123">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="303fc-124">Następujące kombinacje wypełnionych właściwości są wymagane co najmniej do identyfikowania poszczególnych urządzeń:</span><span class="sxs-lookup"><span data-stu-id="303fc-124">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="303fc-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="303fc-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="303fc-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="303fc-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="303fc-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="303fc-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="303fc-128">Tylko [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="303fc-128">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="303fc-129">Tylko [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="303fc-129">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="303fc-130">Numer [**seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="303fc-130">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="303fc-131">Utwórz wystąpienie obiektu [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) i ustaw właściwość [**Identyfikator partii**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) na unikatową wybraną nazwę i Właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na liście urządzeń do przekazania.</span><span class="sxs-lookup"><span data-stu-id="303fc-131">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="303fc-132">Przetwórz żądanie tworzenia wsadowego urządzeń, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu pobrania interfejsu do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="303fc-132">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="303fc-133">Wywołaj metodę [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) z żądaniem tworzenia wsadowego urządzenia, aby utworzyć partię.</span><span class="sxs-lookup"><span data-stu-id="303fc-133">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

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

<span data-ttu-id="303fc-134">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="303fc-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="303fc-135">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateDeviceBatch.cs</span><span class="sxs-lookup"><span data-stu-id="303fc-135">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="303fc-136">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="303fc-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="303fc-137">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="303fc-137">Request syntax</span></span>

| <span data-ttu-id="303fc-138">Metoda</span><span class="sxs-lookup"><span data-stu-id="303fc-138">Method</span></span>   | <span data-ttu-id="303fc-139">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="303fc-139">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="303fc-140">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="303fc-140">**POST**</span></span> | <span data-ttu-id="303fc-141">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches http/1.1</span><span class="sxs-lookup"><span data-stu-id="303fc-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="303fc-142">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="303fc-142">URI parameter</span></span>

<span data-ttu-id="303fc-143">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="303fc-143">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="303fc-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="303fc-144">Name</span></span>        | <span data-ttu-id="303fc-145">Typ</span><span class="sxs-lookup"><span data-stu-id="303fc-145">Type</span></span>   | <span data-ttu-id="303fc-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="303fc-146">Required</span></span> | <span data-ttu-id="303fc-147">Opis</span><span class="sxs-lookup"><span data-stu-id="303fc-147">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="303fc-148">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="303fc-148">customer-id</span></span> | <span data-ttu-id="303fc-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="303fc-149">string</span></span> | <span data-ttu-id="303fc-150">Tak</span><span class="sxs-lookup"><span data-stu-id="303fc-150">Yes</span></span>      | <span data-ttu-id="303fc-151">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="303fc-151">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="303fc-152">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="303fc-152">Request headers</span></span>

<span data-ttu-id="303fc-153">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="303fc-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="303fc-154">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="303fc-154">Request body</span></span>

<span data-ttu-id="303fc-155">Treść żądania musi zawierać zasób [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) .</span><span class="sxs-lookup"><span data-stu-id="303fc-155">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="303fc-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="303fc-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="303fc-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="303fc-157">REST response</span></span>

<span data-ttu-id="303fc-158">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu przekazywania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="303fc-158">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="303fc-159">Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="303fc-159">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="303fc-160">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="303fc-160">Response success and error codes</span></span>

<span data-ttu-id="303fc-161">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="303fc-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="303fc-162">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="303fc-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="303fc-163">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="303fc-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="303fc-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="303fc-164">Response example</span></span>

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
