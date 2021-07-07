---
title: Aktualizowanie zasad konfiguracji dla określonego klienta
description: Jak zaktualizować określone zasady konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5e008f41a44f2b7cf3ddfd705505175c69bbad38
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530241"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="9da64-103">Aktualizowanie zasad konfiguracji dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="9da64-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="9da64-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="9da64-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="9da64-105">Jak zaktualizować określone zasady konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="9da64-105">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9da64-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9da64-106">Prerequisites</span></span>

- <span data-ttu-id="9da64-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9da64-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9da64-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9da64-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9da64-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9da64-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9da64-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9da64-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9da64-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="9da64-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9da64-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="9da64-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9da64-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="9da64-113">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9da64-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9da64-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9da64-115">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="9da64-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="9da64-116">C\#</span><span class="sxs-lookup"><span data-stu-id="9da64-116">C\#</span></span>

<span data-ttu-id="9da64-117">Aby zaktualizować istniejące zasady konfiguracji dla określonego klienta, należy utworzyć wystąpienia nowego obiektu [**ConfigurationPolicy,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="9da64-117">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="9da64-118">Wartości w tym nowym obiekcie zastępują odpowiednie wartości w istniejącym obiekcie.</span><span class="sxs-lookup"><span data-stu-id="9da64-118">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="9da64-119">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="9da64-119">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="9da64-120">Następnie wywołaj metodę [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) z identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.</span><span class="sxs-lookup"><span data-stu-id="9da64-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="9da64-121">Na koniec wywołaj [**metodę Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) lub [**PatchAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) aby zaktualizować zasady konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9da64-121">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

<span data-ttu-id="9da64-122">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9da64-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9da64-123">**Project:** zestaw SDK Centrum partnerskiego **Przykłady klasy**: UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="9da64-123">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9da64-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9da64-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9da64-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9da64-125">Request syntax</span></span>

| <span data-ttu-id="9da64-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="9da64-126">Method</span></span>  | <span data-ttu-id="9da64-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9da64-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9da64-128">**PUT**</span><span class="sxs-lookup"><span data-stu-id="9da64-128">**PUT**</span></span> | <span data-ttu-id="9da64-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9da64-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9da64-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9da64-130">URI parameter</span></span>

<span data-ttu-id="9da64-131">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="9da64-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="9da64-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9da64-132">Name</span></span>        | <span data-ttu-id="9da64-133">Typ</span><span class="sxs-lookup"><span data-stu-id="9da64-133">Type</span></span>   | <span data-ttu-id="9da64-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9da64-134">Required</span></span> | <span data-ttu-id="9da64-135">Opis</span><span class="sxs-lookup"><span data-stu-id="9da64-135">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="9da64-136">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="9da64-136">customer-id</span></span> | <span data-ttu-id="9da64-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="9da64-137">string</span></span> | <span data-ttu-id="9da64-138">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-138">Yes</span></span>      | <span data-ttu-id="9da64-139">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="9da64-139">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="9da64-140">identyfikator zasad</span><span class="sxs-lookup"><span data-stu-id="9da64-140">policy-id</span></span>   | <span data-ttu-id="9da64-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="9da64-141">string</span></span> | <span data-ttu-id="9da64-142">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-142">Yes</span></span>      | <span data-ttu-id="9da64-143">Ciąg w formacie identyfikatora GUID, który identyfikuje zasady do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="9da64-143">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9da64-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9da64-144">Request headers</span></span>

<span data-ttu-id="9da64-145">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9da64-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9da64-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9da64-146">Request body</span></span>

<span data-ttu-id="9da64-147">Treść żądania musi zawierać obiekt , który dostarcza informacje o zasadach.</span><span class="sxs-lookup"><span data-stu-id="9da64-147">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="9da64-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9da64-148">Name</span></span>            | <span data-ttu-id="9da64-149">Typ</span><span class="sxs-lookup"><span data-stu-id="9da64-149">Type</span></span>             | <span data-ttu-id="9da64-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9da64-150">Required</span></span> | <span data-ttu-id="9da64-151">Aktualizowalna</span><span class="sxs-lookup"><span data-stu-id="9da64-151">Updatable</span></span> | <span data-ttu-id="9da64-152">Opis</span><span class="sxs-lookup"><span data-stu-id="9da64-152">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9da64-153">identyfikator</span><span class="sxs-lookup"><span data-stu-id="9da64-153">id</span></span>              | <span data-ttu-id="9da64-154">ciąg</span><span class="sxs-lookup"><span data-stu-id="9da64-154">string</span></span>           | <span data-ttu-id="9da64-155">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-155">Yes</span></span>      | <span data-ttu-id="9da64-156">Nie</span><span class="sxs-lookup"><span data-stu-id="9da64-156">No</span></span>        | <span data-ttu-id="9da64-157">Ciąg w formacie identyfikatora GUID, który identyfikuje zasady.</span><span class="sxs-lookup"><span data-stu-id="9da64-157">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="9da64-158">name</span><span class="sxs-lookup"><span data-stu-id="9da64-158">name</span></span>            | <span data-ttu-id="9da64-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="9da64-159">string</span></span>           | <span data-ttu-id="9da64-160">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-160">Yes</span></span>      | <span data-ttu-id="9da64-161">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-161">Yes</span></span>       | <span data-ttu-id="9da64-162">Przyjazna nazwa zasad.</span><span class="sxs-lookup"><span data-stu-id="9da64-162">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="9da64-163">category</span><span class="sxs-lookup"><span data-stu-id="9da64-163">category</span></span>        | <span data-ttu-id="9da64-164">ciąg</span><span class="sxs-lookup"><span data-stu-id="9da64-164">string</span></span>           | <span data-ttu-id="9da64-165">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-165">Yes</span></span>      | <span data-ttu-id="9da64-166">Nie</span><span class="sxs-lookup"><span data-stu-id="9da64-166">No</span></span>        | <span data-ttu-id="9da64-167">Kategoria zasad.</span><span class="sxs-lookup"><span data-stu-id="9da64-167">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="9da64-168">description (opis)</span><span class="sxs-lookup"><span data-stu-id="9da64-168">description</span></span>     | <span data-ttu-id="9da64-169">ciąg</span><span class="sxs-lookup"><span data-stu-id="9da64-169">string</span></span>           | <span data-ttu-id="9da64-170">Nie</span><span class="sxs-lookup"><span data-stu-id="9da64-170">No</span></span>       | <span data-ttu-id="9da64-171">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-171">Yes</span></span>       | <span data-ttu-id="9da64-172">Opis zasad.</span><span class="sxs-lookup"><span data-stu-id="9da64-172">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="9da64-173">urządzeniaZapisane</span><span class="sxs-lookup"><span data-stu-id="9da64-173">devicesAssigned</span></span> | <span data-ttu-id="9da64-174">liczba</span><span class="sxs-lookup"><span data-stu-id="9da64-174">number</span></span>           | <span data-ttu-id="9da64-175">Nie</span><span class="sxs-lookup"><span data-stu-id="9da64-175">No</span></span>       | <span data-ttu-id="9da64-176">Nie</span><span class="sxs-lookup"><span data-stu-id="9da64-176">No</span></span>        | <span data-ttu-id="9da64-177">Liczba urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9da64-177">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="9da64-178">ustawienia zasad</span><span class="sxs-lookup"><span data-stu-id="9da64-178">policySettings</span></span>  | <span data-ttu-id="9da64-179">tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="9da64-179">array of strings</span></span> | <span data-ttu-id="9da64-180">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-180">Yes</span></span>      | <span data-ttu-id="9da64-181">Tak</span><span class="sxs-lookup"><span data-stu-id="9da64-181">Yes</span></span>       | <span data-ttu-id="9da64-182">Ustawienia zasad: "none", "remove \_ oem \_ preinstalls", "oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration,"skip \_ eula".</span><span class="sxs-lookup"><span data-stu-id="9da64-182">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="9da64-183">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9da64-183">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="9da64-184">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9da64-184">REST response</span></span>

<span data-ttu-id="9da64-185">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) dla nowych zasad.</span><span class="sxs-lookup"><span data-stu-id="9da64-185">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9da64-186">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9da64-186">Response success and error codes</span></span>

<span data-ttu-id="9da64-187">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9da64-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9da64-188">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9da64-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9da64-189">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9da64-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9da64-190">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9da64-190">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
