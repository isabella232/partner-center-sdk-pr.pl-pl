---
title: Pobieranie stanu przekazywania wsadowego urządzeń
description: Jak uzyskać stan przekazywania wsadowego urządzenia dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd8726af41fe4399797f39a0790cf962fde64acc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548485"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="fe494-103">Pobieranie stanu przekazywania wsadowego urządzeń</span><span class="sxs-lookup"><span data-stu-id="fe494-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="fe494-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="fe494-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="fe494-105">Jak uzyskać stan przekazywania wsadowego urządzenia dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="fe494-105">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe494-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe494-106">Prerequisites</span></span>

- <span data-ttu-id="fe494-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fe494-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fe494-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe494-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fe494-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fe494-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fe494-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="fe494-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fe494-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="fe494-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fe494-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="fe494-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fe494-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="fe494-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fe494-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fe494-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fe494-115">Identyfikator śledzenia partii zwrócony w nagłówku Lokalizacja podczas przesłania partii urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fe494-115">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="fe494-116">Aby uzyskać więcej informacji, [Upload listę urządzeń dla określonego klienta.](upload-a-list-of-devices-for-the-specified-customer.md)</span><span class="sxs-lookup"><span data-stu-id="fe494-116">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="fe494-117">C\#</span><span class="sxs-lookup"><span data-stu-id="fe494-117">C\#</span></span>

<span data-ttu-id="fe494-118">Aby uzyskać stan przekazywania wsadowego urządzenia, najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="fe494-118">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="fe494-119">Następnie wywołaj metodę [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) z identyfikatorem śledzenia partii, aby uzyskać interfejs do operacji stanu przekazywania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="fe494-119">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="fe494-120">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) aby pobrać stan.</span><span class="sxs-lookup"><span data-stu-id="fe494-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="fe494-121">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fe494-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fe494-122">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="fe494-122">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fe494-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fe494-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fe494-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fe494-124">Request syntax</span></span>

| <span data-ttu-id="fe494-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="fe494-125">Method</span></span>  | <span data-ttu-id="fe494-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fe494-126">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fe494-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fe494-127">**GET**</span></span> | <span data-ttu-id="fe494-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/batchJobStatus/{batchtracking-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fe494-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fe494-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fe494-129">URI parameter</span></span>

<span data-ttu-id="fe494-130">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="fe494-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="fe494-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fe494-131">Name</span></span>             | <span data-ttu-id="fe494-132">Typ</span><span class="sxs-lookup"><span data-stu-id="fe494-132">Type</span></span>   | <span data-ttu-id="fe494-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fe494-133">Required</span></span> | <span data-ttu-id="fe494-134">Opis</span><span class="sxs-lookup"><span data-stu-id="fe494-134">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fe494-135">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="fe494-135">customer-id</span></span>      | <span data-ttu-id="fe494-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="fe494-136">string</span></span> | <span data-ttu-id="fe494-137">Tak</span><span class="sxs-lookup"><span data-stu-id="fe494-137">Yes</span></span>      | <span data-ttu-id="fe494-138">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="fe494-138">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="fe494-139">batchtracking-id</span><span class="sxs-lookup"><span data-stu-id="fe494-139">batchtracking-id</span></span> | <span data-ttu-id="fe494-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="fe494-140">string</span></span> | <span data-ttu-id="fe494-141">Tak</span><span class="sxs-lookup"><span data-stu-id="fe494-141">Yes</span></span>      | <span data-ttu-id="fe494-142">Identyfikator w formacie GUID, który służy do pobierania stanu przekazywania wsadowego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fe494-142">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="fe494-143">Ten identyfikator jest zwracany w nagłówku Lokalizacja po pomyślnym przesłaniu partii urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fe494-143">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fe494-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fe494-144">Request headers</span></span>

<span data-ttu-id="fe494-145">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fe494-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fe494-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fe494-146">Request body</span></span>

<span data-ttu-id="fe494-147">Brak</span><span class="sxs-lookup"><span data-stu-id="fe494-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="fe494-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fe494-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="fe494-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fe494-149">REST response</span></span>

<span data-ttu-id="fe494-150">Jeśli to się powiedzie, odpowiedź zawiera [zasób BatchUploadDetails.](device-deployment-resources.md#batchuploaddetails)</span><span class="sxs-lookup"><span data-stu-id="fe494-150">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fe494-151">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fe494-151">Response success and error codes</span></span>

<span data-ttu-id="fe494-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="fe494-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fe494-153">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fe494-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fe494-154">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fe494-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fe494-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fe494-155">Response example</span></span>

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
