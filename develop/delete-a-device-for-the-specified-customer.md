---
title: Usuwanie urządzenia dla określonego klienta
description: Jak usunąć urządzenie należące do określonego klienta.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1e05ceb8615d6f84c1df101c542342f9a6eb04b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973081"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="7781e-103">Usuwanie urządzenia dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="7781e-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="7781e-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="7781e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7781e-105">W tym artykule wyjaśniono, jak usunąć urządzenie należące do określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="7781e-105">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7781e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7781e-106">Prerequisites</span></span>

- <span data-ttu-id="7781e-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7781e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7781e-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7781e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7781e-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7781e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7781e-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="7781e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7781e-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="7781e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7781e-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="7781e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7781e-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="7781e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7781e-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7781e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7781e-115">Identyfikator wsadu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="7781e-115">The device batch identifier.</span></span>

- <span data-ttu-id="7781e-116">Identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="7781e-116">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7781e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7781e-117">C\#</span></span>

<span data-ttu-id="7781e-118">Aby usunąć urządzenie dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="7781e-118">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="7781e-119">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na kliencie.</span><span class="sxs-lookup"><span data-stu-id="7781e-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="7781e-120">Wywołaj [**metodę DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) z identyfikatorem wsadowym urządzenia, aby uzyskać interfejs do operacji dla określonej partii.</span><span class="sxs-lookup"><span data-stu-id="7781e-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="7781e-121">Wywołaj [**metodę Devices.ById,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) aby uzyskać interfejs do operacji na określonym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="7781e-121">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="7781e-122">Wywołaj [**metodę Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) lub [**DeleteAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) aby usunąć urządzenie z partii.</span><span class="sxs-lookup"><span data-stu-id="7781e-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="7781e-123">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7781e-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7781e-124">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="7781e-124">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7781e-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7781e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7781e-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7781e-126">Request syntax</span></span>

| <span data-ttu-id="7781e-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="7781e-127">Method</span></span>     | <span data-ttu-id="7781e-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7781e-128">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7781e-129">DELETE</span><span class="sxs-lookup"><span data-stu-id="7781e-129">DELETE</span></span>     | <span data-ttu-id="7781e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7781e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="7781e-131">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="7781e-131">URI parameters</span></span>

<span data-ttu-id="7781e-132">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="7781e-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="7781e-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7781e-133">Name</span></span>           | <span data-ttu-id="7781e-134">Typ</span><span class="sxs-lookup"><span data-stu-id="7781e-134">Type</span></span>   | <span data-ttu-id="7781e-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7781e-135">Required</span></span> | <span data-ttu-id="7781e-136">Opis</span><span class="sxs-lookup"><span data-stu-id="7781e-136">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="7781e-137">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="7781e-137">customer-id</span></span>    | <span data-ttu-id="7781e-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="7781e-138">string</span></span> | <span data-ttu-id="7781e-139">Tak</span><span class="sxs-lookup"><span data-stu-id="7781e-139">Yes</span></span>      | <span data-ttu-id="7781e-140">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="7781e-140">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="7781e-141">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="7781e-141">devicebatch-id</span></span> | <span data-ttu-id="7781e-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="7781e-142">string</span></span> | <span data-ttu-id="7781e-143">Tak</span><span class="sxs-lookup"><span data-stu-id="7781e-143">Yes</span></span>      | <span data-ttu-id="7781e-144">Identyfikator wsadu urządzenia partii zawierającej urządzenie.</span><span class="sxs-lookup"><span data-stu-id="7781e-144">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="7781e-145">identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="7781e-145">device-id</span></span>      | <span data-ttu-id="7781e-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="7781e-146">string</span></span> | <span data-ttu-id="7781e-147">Tak</span><span class="sxs-lookup"><span data-stu-id="7781e-147">Yes</span></span>      | <span data-ttu-id="7781e-148">Identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="7781e-148">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="7781e-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7781e-149">Request headers</span></span>

<span data-ttu-id="7781e-150">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7781e-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7781e-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7781e-151">Request body</span></span>

<span data-ttu-id="7781e-152">Brak</span><span class="sxs-lookup"><span data-stu-id="7781e-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7781e-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7781e-153">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7781e-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7781e-154">REST response</span></span>

<span data-ttu-id="7781e-155">Jeśli to się powiedzie, odpowiedź zwróci kod **stanu 204 Brak** zawartości.</span><span class="sxs-lookup"><span data-stu-id="7781e-155">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7781e-156">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7781e-156">Response success and error codes</span></span>

<span data-ttu-id="7781e-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="7781e-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7781e-158">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7781e-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7781e-159">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7781e-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7781e-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7781e-160">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
