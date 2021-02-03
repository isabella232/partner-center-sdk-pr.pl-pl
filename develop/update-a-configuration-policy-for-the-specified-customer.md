---
title: Aktualizowanie zasad konfiguracji dla określonego klienta
description: Jak zaktualizować określone zasady konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bf3b6f4db7516779c157b647725368ff0e4a570
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768402"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="27b8e-103">Aktualizowanie zasad konfiguracji dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="27b8e-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="27b8e-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="27b8e-104">**Applies To**</span></span>

- <span data-ttu-id="27b8e-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="27b8e-105">Partner Center</span></span>
- <span data-ttu-id="27b8e-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="27b8e-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="27b8e-107">Jak zaktualizować określone zasady konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="27b8e-107">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27b8e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="27b8e-108">Prerequisites</span></span>

- <span data-ttu-id="27b8e-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="27b8e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="27b8e-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="27b8e-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="27b8e-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="27b8e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="27b8e-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="27b8e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="27b8e-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="27b8e-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="27b8e-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="27b8e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="27b8e-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="27b8e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="27b8e-117">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="27b8e-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="27b8e-118">C\#</span><span class="sxs-lookup"><span data-stu-id="27b8e-118">C\#</span></span>

<span data-ttu-id="27b8e-119">Aby zaktualizować istniejące zasady konfiguracji dla określonego klienta, Utwórz wystąpienie nowego obiektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="27b8e-119">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="27b8e-120">Wartości w tym nowym obiekcie zastępują odpowiednie wartości w istniejącym obiekcie.</span><span class="sxs-lookup"><span data-stu-id="27b8e-120">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="27b8e-121">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="27b8e-121">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="27b8e-122">Następnie Wywołaj metodę [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) z identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.</span><span class="sxs-lookup"><span data-stu-id="27b8e-122">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="27b8e-123">Na koniec Wywołaj metodę [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) lub [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) w celu zaktualizowania zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="27b8e-123">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

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

<span data-ttu-id="27b8e-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="27b8e-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="27b8e-125">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="27b8e-125">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="27b8e-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="27b8e-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="27b8e-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="27b8e-127">Request syntax</span></span>

| <span data-ttu-id="27b8e-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="27b8e-128">Method</span></span>  | <span data-ttu-id="27b8e-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="27b8e-129">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="27b8e-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="27b8e-130">**PUT**</span></span> | <span data-ttu-id="27b8e-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="27b8e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="27b8e-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="27b8e-132">URI parameter</span></span>

<span data-ttu-id="27b8e-133">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="27b8e-133">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="27b8e-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="27b8e-134">Name</span></span>        | <span data-ttu-id="27b8e-135">Typ</span><span class="sxs-lookup"><span data-stu-id="27b8e-135">Type</span></span>   | <span data-ttu-id="27b8e-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="27b8e-136">Required</span></span> | <span data-ttu-id="27b8e-137">Opis</span><span class="sxs-lookup"><span data-stu-id="27b8e-137">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="27b8e-138">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="27b8e-138">customer-id</span></span> | <span data-ttu-id="27b8e-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="27b8e-139">string</span></span> | <span data-ttu-id="27b8e-140">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-140">Yes</span></span>      | <span data-ttu-id="27b8e-141">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="27b8e-141">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="27b8e-142">Identyfikator zasad</span><span class="sxs-lookup"><span data-stu-id="27b8e-142">policy-id</span></span>   | <span data-ttu-id="27b8e-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="27b8e-143">string</span></span> | <span data-ttu-id="27b8e-144">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-144">Yes</span></span>      | <span data-ttu-id="27b8e-145">Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje zasady do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="27b8e-145">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="27b8e-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="27b8e-146">Request headers</span></span>

<span data-ttu-id="27b8e-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="27b8e-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="27b8e-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="27b8e-148">Request body</span></span>

<span data-ttu-id="27b8e-149">Treść żądania musi zawierać obiekt, który dostarcza informacje o zasadach.</span><span class="sxs-lookup"><span data-stu-id="27b8e-149">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="27b8e-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="27b8e-150">Name</span></span>            | <span data-ttu-id="27b8e-151">Typ</span><span class="sxs-lookup"><span data-stu-id="27b8e-151">Type</span></span>             | <span data-ttu-id="27b8e-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="27b8e-152">Required</span></span> | <span data-ttu-id="27b8e-153">Zaktualizowa</span><span class="sxs-lookup"><span data-stu-id="27b8e-153">Updatable</span></span> | <span data-ttu-id="27b8e-154">Opis</span><span class="sxs-lookup"><span data-stu-id="27b8e-154">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="27b8e-155">identyfikator</span><span class="sxs-lookup"><span data-stu-id="27b8e-155">id</span></span>              | <span data-ttu-id="27b8e-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="27b8e-156">string</span></span>           | <span data-ttu-id="27b8e-157">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-157">Yes</span></span>      | <span data-ttu-id="27b8e-158">Nie</span><span class="sxs-lookup"><span data-stu-id="27b8e-158">No</span></span>        | <span data-ttu-id="27b8e-159">Ciąg w formacie GUID, który identyfikuje zasady.</span><span class="sxs-lookup"><span data-stu-id="27b8e-159">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="27b8e-160">name</span><span class="sxs-lookup"><span data-stu-id="27b8e-160">name</span></span>            | <span data-ttu-id="27b8e-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="27b8e-161">string</span></span>           | <span data-ttu-id="27b8e-162">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-162">Yes</span></span>      | <span data-ttu-id="27b8e-163">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-163">Yes</span></span>       | <span data-ttu-id="27b8e-164">Przyjazna nazwa zasad.</span><span class="sxs-lookup"><span data-stu-id="27b8e-164">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="27b8e-165">category</span><span class="sxs-lookup"><span data-stu-id="27b8e-165">category</span></span>        | <span data-ttu-id="27b8e-166">ciąg</span><span class="sxs-lookup"><span data-stu-id="27b8e-166">string</span></span>           | <span data-ttu-id="27b8e-167">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-167">Yes</span></span>      | <span data-ttu-id="27b8e-168">Nie</span><span class="sxs-lookup"><span data-stu-id="27b8e-168">No</span></span>        | <span data-ttu-id="27b8e-169">Kategoria zasad.</span><span class="sxs-lookup"><span data-stu-id="27b8e-169">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="27b8e-170">description (opis)</span><span class="sxs-lookup"><span data-stu-id="27b8e-170">description</span></span>     | <span data-ttu-id="27b8e-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="27b8e-171">string</span></span>           | <span data-ttu-id="27b8e-172">Nie</span><span class="sxs-lookup"><span data-stu-id="27b8e-172">No</span></span>       | <span data-ttu-id="27b8e-173">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-173">Yes</span></span>       | <span data-ttu-id="27b8e-174">Opis zasad.</span><span class="sxs-lookup"><span data-stu-id="27b8e-174">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="27b8e-175">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="27b8e-175">devicesAssigned</span></span> | <span data-ttu-id="27b8e-176">liczba</span><span class="sxs-lookup"><span data-stu-id="27b8e-176">number</span></span>           | <span data-ttu-id="27b8e-177">Nie</span><span class="sxs-lookup"><span data-stu-id="27b8e-177">No</span></span>       | <span data-ttu-id="27b8e-178">Nie</span><span class="sxs-lookup"><span data-stu-id="27b8e-178">No</span></span>        | <span data-ttu-id="27b8e-179">Liczba urządzeń.</span><span class="sxs-lookup"><span data-stu-id="27b8e-179">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="27b8e-180">policySettings</span><span class="sxs-lookup"><span data-stu-id="27b8e-180">policySettings</span></span>  | <span data-ttu-id="27b8e-181">tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="27b8e-181">array of strings</span></span> | <span data-ttu-id="27b8e-182">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-182">Yes</span></span>      | <span data-ttu-id="27b8e-183">Tak</span><span class="sxs-lookup"><span data-stu-id="27b8e-183">Yes</span></span>       | <span data-ttu-id="27b8e-184">Ustawienia zasad: "none", "Usuń \_ \_ preinstalls OEM", "User OOBE \_ \_ nie \_ Local \_ admin", "Pomiń \_ Ustawienia ekspresowe \_ ", "Pomiń \_ rejestrację OEM" \_ , Pomiń \_ umowę EULA.</span><span class="sxs-lookup"><span data-stu-id="27b8e-184">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="27b8e-185">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="27b8e-185">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="27b8e-186">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="27b8e-186">REST response</span></span>

<span data-ttu-id="27b8e-187">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) dla nowych zasad.</span><span class="sxs-lookup"><span data-stu-id="27b8e-187">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="27b8e-188">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="27b8e-188">Response success and error codes</span></span>

<span data-ttu-id="27b8e-189">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="27b8e-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="27b8e-190">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="27b8e-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="27b8e-191">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="27b8e-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="27b8e-192">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="27b8e-192">Response example</span></span>

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
