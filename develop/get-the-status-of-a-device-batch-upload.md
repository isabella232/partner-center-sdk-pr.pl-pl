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
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="a98b4-103">Pobieranie stanu przekazywania wsadowego urządzeń</span><span class="sxs-lookup"><span data-stu-id="a98b4-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="a98b4-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="a98b4-104">**Applies To**</span></span>

- <span data-ttu-id="a98b4-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a98b4-105">Partner Center</span></span>
- <span data-ttu-id="a98b4-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="a98b4-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="a98b4-107">Jak uzyskać stan przekazywania wsadowego urządzenia do określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="a98b4-107">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98b4-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a98b4-108">Prerequisites</span></span>

- <span data-ttu-id="a98b4-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a98b4-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a98b4-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a98b4-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a98b4-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a98b4-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a98b4-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a98b4-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a98b4-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="a98b4-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a98b4-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="a98b4-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a98b4-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="a98b4-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a98b4-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a98b4-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a98b4-117">Identyfikator śledzenia partii zwrócony w nagłówku lokalizacji podczas przesyłania wsadowego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a98b4-117">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="a98b4-118">Aby uzyskać więcej informacji, zobacz [przekazywanie listy urządzeń dla określonego klienta](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="a98b4-118">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="a98b4-119">C\#</span><span class="sxs-lookup"><span data-stu-id="a98b4-119">C\#</span></span>

<span data-ttu-id="a98b4-120">Aby uzyskać stan przekazywania wsadowego urządzeń, najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="a98b4-120">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="a98b4-121">Następnie Wywołaj metodę [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) z identyfikatorem śledzenia partii, aby uzyskać interfejs do przetwarzania wsadowego operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="a98b4-121">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="a98b4-122">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) , aby pobrać stan.</span><span class="sxs-lookup"><span data-stu-id="a98b4-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="a98b4-123">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a98b4-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a98b4-124">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="a98b4-124">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a98b4-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a98b4-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a98b4-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a98b4-126">Request syntax</span></span>

| <span data-ttu-id="a98b4-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="a98b4-127">Method</span></span>  | <span data-ttu-id="a98b4-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a98b4-128">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a98b4-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a98b4-129">**GET**</span></span> | <span data-ttu-id="a98b4-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a98b4-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a98b4-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a98b4-131">URI parameter</span></span>

<span data-ttu-id="a98b4-132">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="a98b4-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="a98b4-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a98b4-133">Name</span></span>             | <span data-ttu-id="a98b4-134">Typ</span><span class="sxs-lookup"><span data-stu-id="a98b4-134">Type</span></span>   | <span data-ttu-id="a98b4-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a98b4-135">Required</span></span> | <span data-ttu-id="a98b4-136">Opis</span><span class="sxs-lookup"><span data-stu-id="a98b4-136">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a98b4-137">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="a98b4-137">customer-id</span></span>      | <span data-ttu-id="a98b4-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="a98b4-138">string</span></span> | <span data-ttu-id="a98b4-139">Tak</span><span class="sxs-lookup"><span data-stu-id="a98b4-139">Yes</span></span>      | <span data-ttu-id="a98b4-140">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="a98b4-140">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="a98b4-141">batchtracking — identyfikator</span><span class="sxs-lookup"><span data-stu-id="a98b4-141">batchtracking-id</span></span> | <span data-ttu-id="a98b4-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="a98b4-142">string</span></span> | <span data-ttu-id="a98b4-143">Tak</span><span class="sxs-lookup"><span data-stu-id="a98b4-143">Yes</span></span>      | <span data-ttu-id="a98b4-144">Identyfikator GUID, który jest używany do pobierania stanu przekazywania wsadowego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a98b4-144">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="a98b4-145">Ten identyfikator jest zwracany w nagłówku lokalizacji po pomyślnym przesłaniu partii urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a98b4-145">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a98b4-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a98b4-146">Request headers</span></span>

<span data-ttu-id="a98b4-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a98b4-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a98b4-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a98b4-148">Request body</span></span>

<span data-ttu-id="a98b4-149">Brak</span><span class="sxs-lookup"><span data-stu-id="a98b4-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="a98b4-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a98b4-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a98b4-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a98b4-151">REST response</span></span>

<span data-ttu-id="a98b4-152">Jeśli to się powiedzie, odpowiedź zawiera zasób [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) .</span><span class="sxs-lookup"><span data-stu-id="a98b4-152">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a98b4-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a98b4-153">Response success and error codes</span></span>

<span data-ttu-id="a98b4-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="a98b4-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a98b4-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a98b4-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a98b4-156">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a98b4-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a98b4-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a98b4-157">Response example</span></span>

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
