---
title: Usuwanie urządzenia dla określonego klienta
description: Jak usunąć urządzenie należące do określonego klienta.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768133"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="a3e61-103">Usuwanie urządzenia dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="a3e61-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="a3e61-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="a3e61-104">**Applies to:**</span></span>

- <span data-ttu-id="a3e61-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a3e61-105">Partner Center</span></span>
- <span data-ttu-id="a3e61-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="a3e61-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="a3e61-107">W tym artykule wyjaśniono, jak usunąć urządzenie należące do określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="a3e61-107">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3e61-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a3e61-108">Prerequisites</span></span>

- <span data-ttu-id="a3e61-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a3e61-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a3e61-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3e61-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a3e61-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a3e61-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a3e61-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a3e61-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a3e61-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="a3e61-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a3e61-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="a3e61-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a3e61-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="a3e61-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a3e61-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a3e61-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a3e61-117">Identyfikator partii urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a3e61-117">The device batch identifier.</span></span>

- <span data-ttu-id="a3e61-118">Identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a3e61-118">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="a3e61-119">C\#</span><span class="sxs-lookup"><span data-stu-id="a3e61-119">C\#</span></span>

<span data-ttu-id="a3e61-120">Aby usunąć urządzenie dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="a3e61-120">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="a3e61-121">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na kliencie.</span><span class="sxs-lookup"><span data-stu-id="a3e61-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="a3e61-122">Wywołaj metodę [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) z identyfikatorem partii urządzeń, aby uzyskać interfejs do operacji dla określonej partii.</span><span class="sxs-lookup"><span data-stu-id="a3e61-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="a3e61-123">Wywołaj metodę [**Devices. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) , aby uzyskać interfejs do operacji na określonym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a3e61-123">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="a3e61-124">Wywołaj metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) lub [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) , aby usunąć urządzenie z usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="a3e61-124">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="a3e61-125">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a3e61-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a3e61-126">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="a3e61-126">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a3e61-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a3e61-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a3e61-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a3e61-128">Request syntax</span></span>

| <span data-ttu-id="a3e61-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="a3e61-129">Method</span></span>     | <span data-ttu-id="a3e61-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a3e61-130">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a3e61-131">DELETE</span><span class="sxs-lookup"><span data-stu-id="a3e61-131">DELETE</span></span>     | <span data-ttu-id="a3e61-132">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a3e61-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="a3e61-133">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="a3e61-133">URI parameters</span></span>

<span data-ttu-id="a3e61-134">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="a3e61-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="a3e61-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3e61-135">Name</span></span>           | <span data-ttu-id="a3e61-136">Typ</span><span class="sxs-lookup"><span data-stu-id="a3e61-136">Type</span></span>   | <span data-ttu-id="a3e61-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3e61-137">Required</span></span> | <span data-ttu-id="a3e61-138">Opis</span><span class="sxs-lookup"><span data-stu-id="a3e61-138">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="a3e61-139">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="a3e61-139">customer-id</span></span>    | <span data-ttu-id="a3e61-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="a3e61-140">string</span></span> | <span data-ttu-id="a3e61-141">Tak</span><span class="sxs-lookup"><span data-stu-id="a3e61-141">Yes</span></span>      | <span data-ttu-id="a3e61-142">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="a3e61-142">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="a3e61-143">devicebatch — identyfikator</span><span class="sxs-lookup"><span data-stu-id="a3e61-143">devicebatch-id</span></span> | <span data-ttu-id="a3e61-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="a3e61-144">string</span></span> | <span data-ttu-id="a3e61-145">Tak</span><span class="sxs-lookup"><span data-stu-id="a3e61-145">Yes</span></span>      | <span data-ttu-id="a3e61-146">Identyfikator wsadu urządzenia partii zawierającej urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a3e61-146">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="a3e61-147">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="a3e61-147">device-id</span></span>      | <span data-ttu-id="a3e61-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="a3e61-148">string</span></span> | <span data-ttu-id="a3e61-149">Tak</span><span class="sxs-lookup"><span data-stu-id="a3e61-149">Yes</span></span>      | <span data-ttu-id="a3e61-150">Identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a3e61-150">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="a3e61-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a3e61-151">Request headers</span></span>

<span data-ttu-id="a3e61-152">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a3e61-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a3e61-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a3e61-153">Request body</span></span>

<span data-ttu-id="a3e61-154">Brak</span><span class="sxs-lookup"><span data-stu-id="a3e61-154">None</span></span>

### <a name="request-example"></a><span data-ttu-id="a3e61-155">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a3e61-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a3e61-156">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a3e61-156">REST response</span></span>

<span data-ttu-id="a3e61-157">Jeśli to się powiedzie, odpowiedź zwróci 204 kod stanu **zawartości** .</span><span class="sxs-lookup"><span data-stu-id="a3e61-157">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a3e61-158">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a3e61-158">Response success and error codes</span></span>

<span data-ttu-id="a3e61-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="a3e61-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a3e61-160">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a3e61-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a3e61-161">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a3e61-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a3e61-162">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a3e61-162">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
