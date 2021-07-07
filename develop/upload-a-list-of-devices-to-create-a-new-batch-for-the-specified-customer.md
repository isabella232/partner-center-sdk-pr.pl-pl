---
title: Przekazywanie listy urządzeń w celu utworzenia nowej partii dla określonego klienta
description: Jak przekazać listę informacji o urządzeniach w celu utworzenia nowej partii dla określonego klienta. Powoduje to utworzenie partii urządzeń na potrzeby rejestracji we wdrożeniu bez dotykowym oraz skojarzenie urządzeń i partii urządzeń z określonym klientem.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 285af12034562262c99b2aa3b139e948b0fdd462
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529736"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="c8107-104">Przekazywanie listy urządzeń w celu utworzenia nowej partii dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="c8107-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="c8107-105">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="c8107-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="c8107-106">Jak przekazać listę informacji o urządzeniach w celu utworzenia nowej partii dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="c8107-106">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="c8107-107">Powoduje to utworzenie partii urządzeń na potrzeby rejestracji we wdrożeniu bez dotykowym oraz skojarzenie urządzeń i partii urządzeń z określonym klientem.</span><span class="sxs-lookup"><span data-stu-id="c8107-107">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8107-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c8107-108">Prerequisites</span></span>

- <span data-ttu-id="c8107-109">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c8107-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c8107-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8107-110">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="c8107-111">Postępuj zgodnie z [modelem bezpiecznej aplikacji podczas](enable-secure-app-model.md) korzystania z uwierzytelniania app+user z Partner Center API.</span><span class="sxs-lookup"><span data-stu-id="c8107-111">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="c8107-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8107-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c8107-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c8107-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c8107-114">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="c8107-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c8107-115">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="c8107-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c8107-116">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="c8107-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c8107-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8107-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c8107-118">Lista zasobów urządzeń, które zawierają informacje o poszczególnych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="c8107-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="c8107-119">C\#</span><span class="sxs-lookup"><span data-stu-id="c8107-119">C\#</span></span>

<span data-ttu-id="c8107-120">Aby przekazać listę urządzeń w celu utworzenia nowej partii urządzeń:</span><span class="sxs-lookup"><span data-stu-id="c8107-120">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="c8107-121">Utworzyć nowe wystąpienia typu [List/dotnet/api/system.collections.generic.list-1) typu [**Urządzenie**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) i wypełnić listę urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="c8107-121">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="c8107-122">Następujące kombinacje wypełnionych właściwości są wymagane co najmniej do identyfikowania poszczególnych urządzeń:</span><span class="sxs-lookup"><span data-stu-id="c8107-122">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="c8107-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)( Klucz produktu).</span><span class="sxs-lookup"><span data-stu-id="c8107-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="c8107-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Numer seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="c8107-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="c8107-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Klucz produktu)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Numer seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="c8107-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="c8107-126">[**Tylko sprzętHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)</span><span class="sxs-lookup"><span data-stu-id="c8107-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="c8107-127">[**Tylko ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="c8107-127">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="c8107-128">[**Numer seryjny**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Nazwa modelu**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="c8107-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="c8107-129">Należy utworzyć wystąpienia obiektu [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) i ustawić właściwość [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) na unikatową nazwę, a właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na listę urządzeń do przekazania.</span><span class="sxs-lookup"><span data-stu-id="c8107-129">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="c8107-130">Przetwarzanie żądania utworzenia partii urządzeń przez wywołanie metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu pobrania interfejsu do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="c8107-130">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="c8107-131">Wywołaj [**metodę DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) lub [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) przy użyciu żądania utworzenia partii urządzeń, aby utworzyć partię.</span><span class="sxs-lookup"><span data-stu-id="c8107-131">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

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

<span data-ttu-id="c8107-132">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c8107-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c8107-133">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: CreateDeviceBatch.cs</span><span class="sxs-lookup"><span data-stu-id="c8107-133">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c8107-134">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c8107-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c8107-135">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c8107-135">Request syntax</span></span>

| <span data-ttu-id="c8107-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="c8107-136">Method</span></span>   | <span data-ttu-id="c8107-137">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c8107-137">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="c8107-138">**Post**</span><span class="sxs-lookup"><span data-stu-id="c8107-138">**POST**</span></span> | <span data-ttu-id="c8107-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c8107-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c8107-140">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c8107-140">URI parameter</span></span>

<span data-ttu-id="c8107-141">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c8107-141">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="c8107-142">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c8107-142">Name</span></span>        | <span data-ttu-id="c8107-143">Typ</span><span class="sxs-lookup"><span data-stu-id="c8107-143">Type</span></span>   | <span data-ttu-id="c8107-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c8107-144">Required</span></span> | <span data-ttu-id="c8107-145">Opis</span><span class="sxs-lookup"><span data-stu-id="c8107-145">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="c8107-146">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="c8107-146">customer-id</span></span> | <span data-ttu-id="c8107-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="c8107-147">string</span></span> | <span data-ttu-id="c8107-148">Tak</span><span class="sxs-lookup"><span data-stu-id="c8107-148">Yes</span></span>      | <span data-ttu-id="c8107-149">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="c8107-149">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c8107-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c8107-150">Request headers</span></span>

<span data-ttu-id="c8107-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c8107-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c8107-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c8107-152">Request body</span></span>

<span data-ttu-id="c8107-153">Treść żądania musi zawierać [zasób DeviceBatchCreationRequest.](device-deployment-resources.md#devicebatchcreationrequest)</span><span class="sxs-lookup"><span data-stu-id="c8107-153">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="c8107-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c8107-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c8107-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c8107-155">REST response</span></span>

<span data-ttu-id="c8107-156">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** (Lokalizacja) z polem URI, który może służyć do pobierania stanu przekazywania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c8107-156">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="c8107-157">Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="c8107-157">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c8107-158">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c8107-158">Response success and error codes</span></span>

<span data-ttu-id="c8107-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="c8107-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c8107-160">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c8107-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c8107-161">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c8107-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="c8107-162">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c8107-162">Response example</span></span>

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
