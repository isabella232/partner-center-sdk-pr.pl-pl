---
title: Pobieranie listy partii urządzeń dla określonego klienta
description: Pobieranie kolekcji partii urządzeń dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d020bbfa1faef0be423d2fef2d8982465dfa21f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548424"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="1a3cb-103">Pobieranie listy partii urządzeń dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="1a3cb-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="1a3cb-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="1a3cb-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1a3cb-105">Pobieranie kolekcji partii urządzeń dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-105">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="1a3cb-106">Każda partia urządzeń zawiera podsumowanie informacji o stanie urządzeń zarejestrowanych we wdrożeniu bez dotykowym.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-106">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a3cb-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a3cb-107">Prerequisites</span></span>

- <span data-ttu-id="1a3cb-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1a3cb-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a3cb-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1a3cb-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a3cb-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1a3cb-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1a3cb-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1a3cb-112">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="1a3cb-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1a3cb-113">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1a3cb-114">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1a3cb-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a3cb-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1a3cb-116">C\#</span><span class="sxs-lookup"><span data-stu-id="1a3cb-116">C\#</span></span>

<span data-ttu-id="1a3cb-117">Aby pobrać kolekcję partii urządzeń dla określonego klienta, najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-117">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="1a3cb-118">Następnie pobierz wartość właściwości [**DeviceBatches,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) aby uzyskać interfejs operacji zbierania wsadowego urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-118">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="1a3cb-119">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) aby pobrać kolekcję.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="1a3cb-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1a3cb-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1a3cb-121">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="1a3cb-121">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1a3cb-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1a3cb-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a3cb-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1a3cb-123">Request syntax</span></span>

| <span data-ttu-id="1a3cb-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="1a3cb-124">Method</span></span>  | <span data-ttu-id="1a3cb-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1a3cb-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a3cb-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1a3cb-126">**GET**</span></span> | <span data-ttu-id="1a3cb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1a3cb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1a3cb-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1a3cb-128">URI parameter</span></span>

<span data-ttu-id="1a3cb-129">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-129">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="1a3cb-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1a3cb-130">Name</span></span>        | <span data-ttu-id="1a3cb-131">Typ</span><span class="sxs-lookup"><span data-stu-id="1a3cb-131">Type</span></span>   | <span data-ttu-id="1a3cb-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1a3cb-132">Required</span></span> | <span data-ttu-id="1a3cb-133">Opis</span><span class="sxs-lookup"><span data-stu-id="1a3cb-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1a3cb-134">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="1a3cb-134">customer-id</span></span> | <span data-ttu-id="1a3cb-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="1a3cb-135">string</span></span> | <span data-ttu-id="1a3cb-136">Tak</span><span class="sxs-lookup"><span data-stu-id="1a3cb-136">Yes</span></span>      | <span data-ttu-id="1a3cb-137">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a3cb-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1a3cb-138">Request headers</span></span>

<span data-ttu-id="1a3cb-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1a3cb-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a3cb-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1a3cb-140">Request body</span></span>

<span data-ttu-id="1a3cb-141">Brak</span><span class="sxs-lookup"><span data-stu-id="1a3cb-141">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1a3cb-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1a3cb-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1a3cb-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1a3cb-143">REST response</span></span>

<span data-ttu-id="1a3cb-144">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów DeviceBatch.](device-deployment-resources.md#devicebatch)</span><span class="sxs-lookup"><span data-stu-id="1a3cb-144">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a3cb-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1a3cb-145">Response success and error codes</span></span>

<span data-ttu-id="1a3cb-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a3cb-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1a3cb-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a3cb-148">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1a3cb-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a3cb-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1a3cb-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
