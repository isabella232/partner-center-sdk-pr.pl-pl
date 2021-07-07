---
title: Aktualizowanie listy urządzeń za pomocą zasad
description: Jak zaktualizować listę urządzeń przy użyciu zasad konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b35873eb253b0929bfc01662b0beb9b31d0c6b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530076"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="8f316-103">Aktualizowanie listy urządzeń za pomocą zasad</span><span class="sxs-lookup"><span data-stu-id="8f316-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="8f316-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="8f316-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8f316-105">Jak zaktualizować listę urządzeń przy użyciu zasad konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="8f316-105">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f316-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f316-106">Prerequisites</span></span>

- <span data-ttu-id="8f316-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8f316-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f316-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f316-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8f316-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f316-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8f316-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="8f316-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8f316-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="8f316-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8f316-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="8f316-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8f316-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="8f316-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8f316-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f316-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8f316-115">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="8f316-115">The policy identifier.</span></span>

- <span data-ttu-id="8f316-116">Identyfikatory urządzeń do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="8f316-116">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="8f316-117">C\#</span><span class="sxs-lookup"><span data-stu-id="8f316-117">C\#</span></span>

<span data-ttu-id="8f316-118">Aby zaktualizować listę urządzeń przy użyciu określonych zasad konfiguracji, najpierw należy utworzyć wystąpienia [List/dotnet/api/system.collections.generic.list-1) typu [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) i dodać zasady do zastosowania, jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="8f316-118">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="8f316-119">Będziesz potrzebować identyfikatora zasad.</span><span class="sxs-lookup"><span data-stu-id="8f316-119">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="8f316-120">Następnie utwórz listę obiektów [**urządzeń**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) do zaktualizowania przy użyciu zasad, określając identyfikator urządzenia i listę zawierającą zasady do zastosowania dla każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8f316-120">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="8f316-121">Następnie należy utworzyć wystąpienia obiektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) i ustawić właściwość [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na listę obiektów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8f316-121">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="8f316-122">Aby przetworzyć żądanie aktualizacji zasad urządzenia, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="8f316-122">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="8f316-123">Następnie pobierz właściwość [**DevicePolicy,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) aby uzyskać interfejs operacji zbierania urządzeń przez klienta.</span><span class="sxs-lookup"><span data-stu-id="8f316-123">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="8f316-124">Na koniec wywołaj [**metodę Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) za pomocą obiektu DevicePolicyUpdateRequest, aby zaktualizować urządzenia przy użyciu zasad.</span><span class="sxs-lookup"><span data-stu-id="8f316-124">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

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

<span data-ttu-id="8f316-125">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8f316-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8f316-126">**Project:** zestaw SDK Centrum partnerskiego Samples Class : UpdateDevicesPolicy.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: UpdateDevicesPolicy.cs)</span><span class="sxs-lookup"><span data-stu-id="8f316-126">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8f316-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8f316-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f316-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8f316-128">Request syntax</span></span>

| <span data-ttu-id="8f316-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="8f316-129">Method</span></span>    | <span data-ttu-id="8f316-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8f316-130">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f316-131">**Patch**</span><span class="sxs-lookup"><span data-stu-id="8f316-131">**PATCH**</span></span> | <span data-ttu-id="8f316-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/DevicePolicyUpdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8f316-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8f316-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8f316-133">URI parameter</span></span>

<span data-ttu-id="8f316-134">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="8f316-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="8f316-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8f316-135">Name</span></span>        | <span data-ttu-id="8f316-136">Typ</span><span class="sxs-lookup"><span data-stu-id="8f316-136">Type</span></span>   | <span data-ttu-id="8f316-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8f316-137">Required</span></span> | <span data-ttu-id="8f316-138">Opis</span><span class="sxs-lookup"><span data-stu-id="8f316-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8f316-139">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="8f316-139">customer-id</span></span> | <span data-ttu-id="8f316-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="8f316-140">string</span></span> | <span data-ttu-id="8f316-141">Tak</span><span class="sxs-lookup"><span data-stu-id="8f316-141">Yes</span></span>      | <span data-ttu-id="8f316-142">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="8f316-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8f316-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8f316-143">Request headers</span></span>

<span data-ttu-id="8f316-144">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8f316-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8f316-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8f316-145">Request body</span></span>

<span data-ttu-id="8f316-146">Treść żądania musi zawierać [zasób DevicePolicyUpdateRequest.](device-deployment-resources.md#devicepolicyupdaterequest)</span><span class="sxs-lookup"><span data-stu-id="8f316-146">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="8f316-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8f316-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8f316-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8f316-148">REST response</span></span>

<span data-ttu-id="8f316-149">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** z numerem URI, który może służyć do pobierania stanu tego procesu wsadowego.</span><span class="sxs-lookup"><span data-stu-id="8f316-149">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="8f316-150">Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="8f316-150">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f316-151">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8f316-151">Response success and error codes</span></span>

<span data-ttu-id="8f316-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8f316-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f316-153">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8f316-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f316-154">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8f316-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8f316-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8f316-155">Response example</span></span>

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
