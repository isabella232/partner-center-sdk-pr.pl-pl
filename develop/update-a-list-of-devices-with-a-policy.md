---
title: Aktualizowanie listy urządzeń za pomocą zasad
description: Jak zaktualizować listę urządzeń za pomocą zasad konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04c2ef33116335db40bd2934dc7e33d57f015097
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768377"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="539e0-103">Aktualizowanie listy urządzeń za pomocą zasad</span><span class="sxs-lookup"><span data-stu-id="539e0-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="539e0-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="539e0-104">**Applies To**</span></span>

- <span data-ttu-id="539e0-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="539e0-105">Partner Center</span></span>
- <span data-ttu-id="539e0-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="539e0-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="539e0-107">Jak zaktualizować listę urządzeń za pomocą zasad konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="539e0-107">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="539e0-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="539e0-108">Prerequisites</span></span>

- <span data-ttu-id="539e0-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="539e0-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="539e0-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="539e0-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="539e0-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="539e0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="539e0-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="539e0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="539e0-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="539e0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="539e0-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="539e0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="539e0-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="539e0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="539e0-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="539e0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="539e0-117">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="539e0-117">The policy identifier.</span></span>

- <span data-ttu-id="539e0-118">Identyfikatory urządzeń, które mają zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="539e0-118">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="539e0-119">C\#</span><span class="sxs-lookup"><span data-stu-id="539e0-119">C\#</span></span>

<span data-ttu-id="539e0-120">Aby zaktualizować listę urządzeń z określonymi zasadami konfiguracji, należy najpierw utworzyć wystąpienie [list/dotnet/API/System. Collections. Generic. list -1) typu [KeyValuePair/dotnet/API/System. Collections. Generic. KeyValuePair -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) i dodać zasady do zastosowania, jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="539e0-120">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="539e0-121">Wymagany jest identyfikator zasad dla zasad.</span><span class="sxs-lookup"><span data-stu-id="539e0-121">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="539e0-122">Następnie utwórz listę obiektów [**urządzeń**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) , które mają zostać zaktualizowane przy użyciu zasad, określając identyfikator urządzenia i listę zawierającą zasady do zastosowania dla każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="539e0-122">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="539e0-123">Następnie Utwórz wystąpienie obiektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) i ustaw właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na listę obiektów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="539e0-123">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="539e0-124">Aby przetworzyć żądanie aktualizacji zasad dotyczących urządzeń, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="539e0-124">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="539e0-125">Następnie Pobierz Właściwość [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) , aby uzyskać interfejs do operacji zbierania urządzeń przez klienta.</span><span class="sxs-lookup"><span data-stu-id="539e0-125">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="539e0-126">Na koniec Wywołaj metodę [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) z obiektem DevicePolicyUpdateRequest, aby zaktualizować urządzenia przy użyciu zasad.</span><span class="sxs-lookup"><span data-stu-id="539e0-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

<span data-ttu-id="539e0-127">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="539e0-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="539e0-128">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="539e0-128">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="539e0-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="539e0-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="539e0-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="539e0-130">Request syntax</span></span>

| <span data-ttu-id="539e0-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="539e0-131">Method</span></span>    | <span data-ttu-id="539e0-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="539e0-132">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="539e0-133">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="539e0-133">**PATCH**</span></span> | <span data-ttu-id="539e0-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/DevicePolicyUpdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="539e0-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="539e0-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="539e0-135">URI parameter</span></span>

<span data-ttu-id="539e0-136">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="539e0-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="539e0-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="539e0-137">Name</span></span>        | <span data-ttu-id="539e0-138">Typ</span><span class="sxs-lookup"><span data-stu-id="539e0-138">Type</span></span>   | <span data-ttu-id="539e0-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="539e0-139">Required</span></span> | <span data-ttu-id="539e0-140">Opis</span><span class="sxs-lookup"><span data-stu-id="539e0-140">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="539e0-141">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="539e0-141">customer-id</span></span> | <span data-ttu-id="539e0-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="539e0-142">string</span></span> | <span data-ttu-id="539e0-143">Tak</span><span class="sxs-lookup"><span data-stu-id="539e0-143">Yes</span></span>      | <span data-ttu-id="539e0-144">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="539e0-144">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="539e0-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="539e0-145">Request headers</span></span>

<span data-ttu-id="539e0-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="539e0-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="539e0-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="539e0-147">Request body</span></span>

<span data-ttu-id="539e0-148">Treść żądania musi zawierać zasób [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) .</span><span class="sxs-lookup"><span data-stu-id="539e0-148">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="539e0-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="539e0-149">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="539e0-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="539e0-150">REST response</span></span>

<span data-ttu-id="539e0-151">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu tego procesu wsadowego.</span><span class="sxs-lookup"><span data-stu-id="539e0-151">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="539e0-152">Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="539e0-152">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="539e0-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="539e0-153">Response success and error codes</span></span>

<span data-ttu-id="539e0-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="539e0-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="539e0-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="539e0-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="539e0-156">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="539e0-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="539e0-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="539e0-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
