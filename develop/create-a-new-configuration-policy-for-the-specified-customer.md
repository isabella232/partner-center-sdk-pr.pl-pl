---
title: Utwórz nowe zasady konfiguracji klienta
description: Dowiedz się, jak utworzyć nowe zasady konfiguracji dla określonego klienta przy użyciu interfejsów API usługi Partner Center. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 21a0bfde7f931371ff09d6c27de0281a4ed3b3cb
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770164"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="1a783-104">Tworzenie nowych zasad konfiguracji dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="1a783-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="1a783-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="1a783-105">**Applies to:**</span></span>

- <span data-ttu-id="1a783-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="1a783-106">Partner Center</span></span>
- <span data-ttu-id="1a783-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="1a783-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1a783-108">Jak utworzyć nowe zasady konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="1a783-108">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a783-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a783-109">Prerequisites</span></span>

- <span data-ttu-id="1a783-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1a783-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a783-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a783-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1a783-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a783-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1a783-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1a783-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1a783-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="1a783-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1a783-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="1a783-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1a783-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="1a783-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1a783-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a783-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1a783-118">C\#</span><span class="sxs-lookup"><span data-stu-id="1a783-118">C\#</span></span>

<span data-ttu-id="1a783-119">Aby utworzyć nowe zasady konfiguracji dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="1a783-119">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="1a783-120">Utwórz wystąpienie nowego obiektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="1a783-120">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="1a783-121">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="1a783-121">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="1a783-122">Pobierz Właściwość [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) , aby uzyskać interfejs do operacji zbierania zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a783-122">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="1a783-123">Wywoływanie metody [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) w celu utworzenia zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a783-123">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="1a783-124">\#Przykład C</span><span class="sxs-lookup"><span data-stu-id="1a783-124">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

<span data-ttu-id="1a783-125">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1a783-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1a783-126">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="1a783-126">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1a783-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1a783-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a783-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1a783-128">Request syntax</span></span>

| <span data-ttu-id="1a783-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="1a783-129">Method</span></span>   | <span data-ttu-id="1a783-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1a783-130">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a783-131">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="1a783-131">**POST**</span></span> | <span data-ttu-id="1a783-132">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="1a783-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1a783-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1a783-133">URI parameter</span></span>

<span data-ttu-id="1a783-134">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="1a783-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="1a783-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1a783-135">Name</span></span>        | <span data-ttu-id="1a783-136">Typ</span><span class="sxs-lookup"><span data-stu-id="1a783-136">Type</span></span>   | <span data-ttu-id="1a783-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1a783-137">Required</span></span> | <span data-ttu-id="1a783-138">Opis</span><span class="sxs-lookup"><span data-stu-id="1a783-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1a783-139">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="1a783-139">customer-id</span></span> | <span data-ttu-id="1a783-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="1a783-140">string</span></span> | <span data-ttu-id="1a783-141">Tak</span><span class="sxs-lookup"><span data-stu-id="1a783-141">Yes</span></span>      | <span data-ttu-id="1a783-142">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="1a783-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a783-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1a783-143">Request headers</span></span>

<span data-ttu-id="1a783-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1a783-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a783-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1a783-145">Request body</span></span>

<span data-ttu-id="1a783-146">Treść żądania musi zawierać obiekt z informacjami o zasadach konfiguracji, zgodnie z opisem w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="1a783-146">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="1a783-147">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1a783-147">Name</span></span>           | <span data-ttu-id="1a783-148">Typ</span><span class="sxs-lookup"><span data-stu-id="1a783-148">Type</span></span>             | <span data-ttu-id="1a783-149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1a783-149">Required</span></span> | <span data-ttu-id="1a783-150">Opis</span><span class="sxs-lookup"><span data-stu-id="1a783-150">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="1a783-151">name</span><span class="sxs-lookup"><span data-stu-id="1a783-151">name</span></span>           | <span data-ttu-id="1a783-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="1a783-152">string</span></span>           | <span data-ttu-id="1a783-153">Tak</span><span class="sxs-lookup"><span data-stu-id="1a783-153">Yes</span></span>      | <span data-ttu-id="1a783-154">Przyjazna nazwa zasad.</span><span class="sxs-lookup"><span data-stu-id="1a783-154">The friendly name of the policy.</span></span> |
| <span data-ttu-id="1a783-155">category</span><span class="sxs-lookup"><span data-stu-id="1a783-155">category</span></span>       | <span data-ttu-id="1a783-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="1a783-156">string</span></span>           | <span data-ttu-id="1a783-157">Tak</span><span class="sxs-lookup"><span data-stu-id="1a783-157">Yes</span></span>      | <span data-ttu-id="1a783-158">Kategoria zasad.</span><span class="sxs-lookup"><span data-stu-id="1a783-158">The policy category.</span></span>             |
| <span data-ttu-id="1a783-159">description (opis)</span><span class="sxs-lookup"><span data-stu-id="1a783-159">description</span></span>    | <span data-ttu-id="1a783-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="1a783-160">string</span></span>           | <span data-ttu-id="1a783-161">Nie</span><span class="sxs-lookup"><span data-stu-id="1a783-161">No</span></span>       | <span data-ttu-id="1a783-162">Opis zasad.</span><span class="sxs-lookup"><span data-stu-id="1a783-162">The policy description.</span></span>          |
| <span data-ttu-id="1a783-163">policySettings</span><span class="sxs-lookup"><span data-stu-id="1a783-163">policySettings</span></span> | <span data-ttu-id="1a783-164">tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="1a783-164">array of strings</span></span> | <span data-ttu-id="1a783-165">Tak</span><span class="sxs-lookup"><span data-stu-id="1a783-165">Yes</span></span>      | <span data-ttu-id="1a783-166">Ustawienia zasad.</span><span class="sxs-lookup"><span data-stu-id="1a783-166">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="1a783-167">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1a783-167">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="1a783-168">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1a783-168">REST response</span></span>

<span data-ttu-id="1a783-169">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) dla nowych zasad.</span><span class="sxs-lookup"><span data-stu-id="1a783-169">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a783-170">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1a783-170">Response success and error codes</span></span>

<span data-ttu-id="1a783-171">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="1a783-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a783-172">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1a783-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a783-173">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1a783-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a783-174">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1a783-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
