---
title: Tworzenie nowych zasad konfiguracji klienta
description: Dowiedz się, jak używać Partner Center API do tworzenia nowych zasad konfiguracji dla określonego klienta. Artykuł zawiera wymagania wstępne, kroki i przykłady.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 530ff72862204bda093385252450f4eb81b63160
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973676"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="c534d-104">Tworzenie nowych zasad konfiguracji dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="c534d-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="c534d-105">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="c534d-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="c534d-106">Jak utworzyć nowe zasady konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="c534d-106">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c534d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c534d-107">Prerequisites</span></span>

- <span data-ttu-id="c534d-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c534d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c534d-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c534d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c534d-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c534d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c534d-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c534d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c534d-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="c534d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c534d-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="c534d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c534d-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="c534d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c534d-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c534d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c534d-116">C\#</span><span class="sxs-lookup"><span data-stu-id="c534d-116">C\#</span></span>

<span data-ttu-id="c534d-117">Aby utworzyć nowe zasady konfiguracji dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="c534d-117">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="c534d-118">Zaimpluj nowy obiekt [**ConfigurationPolicy,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="c534d-118">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="c534d-119">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="c534d-119">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="c534d-120">Pobierz właściwość [**ConfigurationPolicies,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) aby uzyskać interfejs operacji zbierania zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c534d-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="c534d-121">Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) aby utworzyć zasady konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c534d-121">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="c534d-122">Przykład w \# języku C</span><span class="sxs-lookup"><span data-stu-id="c534d-122">C\# example</span></span>

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

<span data-ttu-id="c534d-123">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c534d-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c534d-124">**Project:** zestaw SDK Centrum partnerskiego **Przykłady klasy**: CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="c534d-124">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c534d-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c534d-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c534d-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c534d-126">Request syntax</span></span>

| <span data-ttu-id="c534d-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="c534d-127">Method</span></span>   | <span data-ttu-id="c534d-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c534d-128">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="c534d-129">**Post**</span><span class="sxs-lookup"><span data-stu-id="c534d-129">**POST**</span></span> | <span data-ttu-id="c534d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c534d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c534d-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c534d-131">URI parameter</span></span>

<span data-ttu-id="c534d-132">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c534d-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="c534d-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c534d-133">Name</span></span>        | <span data-ttu-id="c534d-134">Typ</span><span class="sxs-lookup"><span data-stu-id="c534d-134">Type</span></span>   | <span data-ttu-id="c534d-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c534d-135">Required</span></span> | <span data-ttu-id="c534d-136">Opis</span><span class="sxs-lookup"><span data-stu-id="c534d-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="c534d-137">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="c534d-137">customer-id</span></span> | <span data-ttu-id="c534d-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="c534d-138">string</span></span> | <span data-ttu-id="c534d-139">Tak</span><span class="sxs-lookup"><span data-stu-id="c534d-139">Yes</span></span>      | <span data-ttu-id="c534d-140">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="c534d-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c534d-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c534d-141">Request headers</span></span>

<span data-ttu-id="c534d-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c534d-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c534d-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c534d-143">Request body</span></span>

<span data-ttu-id="c534d-144">Treść żądania musi zawierać obiekt z informacjami o zasadach konfiguracji zgodnie z opisem w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="c534d-144">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="c534d-145">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c534d-145">Name</span></span>           | <span data-ttu-id="c534d-146">Typ</span><span class="sxs-lookup"><span data-stu-id="c534d-146">Type</span></span>             | <span data-ttu-id="c534d-147">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c534d-147">Required</span></span> | <span data-ttu-id="c534d-148">Opis</span><span class="sxs-lookup"><span data-stu-id="c534d-148">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="c534d-149">name</span><span class="sxs-lookup"><span data-stu-id="c534d-149">name</span></span>           | <span data-ttu-id="c534d-150">ciąg</span><span class="sxs-lookup"><span data-stu-id="c534d-150">string</span></span>           | <span data-ttu-id="c534d-151">Tak</span><span class="sxs-lookup"><span data-stu-id="c534d-151">Yes</span></span>      | <span data-ttu-id="c534d-152">Przyjazna nazwa zasad.</span><span class="sxs-lookup"><span data-stu-id="c534d-152">The friendly name of the policy.</span></span> |
| <span data-ttu-id="c534d-153">category</span><span class="sxs-lookup"><span data-stu-id="c534d-153">category</span></span>       | <span data-ttu-id="c534d-154">ciąg</span><span class="sxs-lookup"><span data-stu-id="c534d-154">string</span></span>           | <span data-ttu-id="c534d-155">Tak</span><span class="sxs-lookup"><span data-stu-id="c534d-155">Yes</span></span>      | <span data-ttu-id="c534d-156">Kategoria zasad.</span><span class="sxs-lookup"><span data-stu-id="c534d-156">The policy category.</span></span>             |
| <span data-ttu-id="c534d-157">description (opis)</span><span class="sxs-lookup"><span data-stu-id="c534d-157">description</span></span>    | <span data-ttu-id="c534d-158">ciąg</span><span class="sxs-lookup"><span data-stu-id="c534d-158">string</span></span>           | <span data-ttu-id="c534d-159">Nie</span><span class="sxs-lookup"><span data-stu-id="c534d-159">No</span></span>       | <span data-ttu-id="c534d-160">Opis zasad.</span><span class="sxs-lookup"><span data-stu-id="c534d-160">The policy description.</span></span>          |
| <span data-ttu-id="c534d-161">ustawienia zasad</span><span class="sxs-lookup"><span data-stu-id="c534d-161">policySettings</span></span> | <span data-ttu-id="c534d-162">tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="c534d-162">array of strings</span></span> | <span data-ttu-id="c534d-163">Tak</span><span class="sxs-lookup"><span data-stu-id="c534d-163">Yes</span></span>      | <span data-ttu-id="c534d-164">Ustawienia zasad.</span><span class="sxs-lookup"><span data-stu-id="c534d-164">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="c534d-165">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c534d-165">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c534d-166">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c534d-166">REST response</span></span>

<span data-ttu-id="c534d-167">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) dla nowych zasad.</span><span class="sxs-lookup"><span data-stu-id="c534d-167">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c534d-168">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c534d-168">Response success and error codes</span></span>

<span data-ttu-id="c534d-169">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="c534d-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c534d-170">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c534d-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c534d-171">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c534d-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c534d-172">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c534d-172">Response example</span></span>

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
