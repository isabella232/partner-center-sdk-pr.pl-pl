---
title: Pobieranie listy partii urządzeń dla określonego klienta
description: Jak pobrać kolekcję partii urządzeń dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea5797bbaff4d4eafd1e63428556ab784bcb0ee2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768414"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="538cd-103">Pobieranie listy partii urządzeń dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="538cd-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="538cd-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="538cd-104">**Applies To**</span></span>

- <span data-ttu-id="538cd-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="538cd-105">Partner Center</span></span>
- <span data-ttu-id="538cd-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="538cd-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="538cd-107">Jak pobrać kolekcję partii urządzeń dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="538cd-107">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="538cd-108">Każda partia urządzeń zawiera podsumowanie informacji o stanie urządzeń, które zostały zarejestrowane w ramach wdrożenia bez dotknięcia.</span><span class="sxs-lookup"><span data-stu-id="538cd-108">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="538cd-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="538cd-109">Prerequisites</span></span>

- <span data-ttu-id="538cd-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="538cd-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="538cd-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="538cd-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="538cd-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="538cd-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="538cd-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="538cd-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="538cd-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="538cd-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="538cd-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="538cd-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="538cd-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="538cd-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="538cd-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="538cd-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="538cd-118">C\#</span><span class="sxs-lookup"><span data-stu-id="538cd-118">C\#</span></span>

<span data-ttu-id="538cd-119">Aby uzyskać kolekcję partii urządzeń dla określonego klienta, najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="538cd-119">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="538cd-120">Następnie Pobierz wartość właściwości [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) , aby uzyskać interfejs do operacji zbierania danych wsadowych na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="538cd-120">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="538cd-121">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) w celu pobrania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="538cd-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="538cd-122">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="538cd-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="538cd-123">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="538cd-123">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="538cd-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="538cd-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="538cd-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="538cd-125">Request syntax</span></span>

| <span data-ttu-id="538cd-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="538cd-126">Method</span></span>  | <span data-ttu-id="538cd-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="538cd-127">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="538cd-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="538cd-128">**GET**</span></span> | <span data-ttu-id="538cd-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/deviceBatches http/1.1</span><span class="sxs-lookup"><span data-stu-id="538cd-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="538cd-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="538cd-130">URI parameter</span></span>

<span data-ttu-id="538cd-131">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="538cd-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="538cd-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="538cd-132">Name</span></span>        | <span data-ttu-id="538cd-133">Typ</span><span class="sxs-lookup"><span data-stu-id="538cd-133">Type</span></span>   | <span data-ttu-id="538cd-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="538cd-134">Required</span></span> | <span data-ttu-id="538cd-135">Opis</span><span class="sxs-lookup"><span data-stu-id="538cd-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="538cd-136">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="538cd-136">customer-id</span></span> | <span data-ttu-id="538cd-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="538cd-137">string</span></span> | <span data-ttu-id="538cd-138">Tak</span><span class="sxs-lookup"><span data-stu-id="538cd-138">Yes</span></span>      | <span data-ttu-id="538cd-139">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="538cd-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="538cd-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="538cd-140">Request headers</span></span>

<span data-ttu-id="538cd-141">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="538cd-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="538cd-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="538cd-142">Request body</span></span>

<span data-ttu-id="538cd-143">Brak</span><span class="sxs-lookup"><span data-stu-id="538cd-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="538cd-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="538cd-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="538cd-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="538cd-145">REST response</span></span>

<span data-ttu-id="538cd-146">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [DeviceBatch](device-deployment-resources.md#devicebatch) .</span><span class="sxs-lookup"><span data-stu-id="538cd-146">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="538cd-147">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="538cd-147">Response success and error codes</span></span>

<span data-ttu-id="538cd-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="538cd-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="538cd-149">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="538cd-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="538cd-150">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="538cd-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="538cd-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="538cd-151">Response example</span></span>

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
