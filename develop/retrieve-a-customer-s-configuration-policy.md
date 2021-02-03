---
title: Pobieranie zasad konfiguracji klienta
description: Jak pobrać określone zasady konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d5d4ee83d1a66f33872d8b1f1327f47eeb4465e
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768401"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="7730c-103">Pobieranie zasad konfiguracji klienta</span><span class="sxs-lookup"><span data-stu-id="7730c-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="7730c-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="7730c-104">**Applies To**</span></span>

- <span data-ttu-id="7730c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="7730c-105">Partner Center</span></span>
- <span data-ttu-id="7730c-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="7730c-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7730c-107">Jak pobrać określone zasady konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="7730c-107">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7730c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7730c-108">Prerequisites</span></span>

- <span data-ttu-id="7730c-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7730c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7730c-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7730c-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7730c-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7730c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7730c-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="7730c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7730c-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="7730c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7730c-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="7730c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7730c-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="7730c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7730c-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7730c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7730c-117">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="7730c-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7730c-118">C\#</span><span class="sxs-lookup"><span data-stu-id="7730c-118">C\#</span></span>

<span data-ttu-id="7730c-119">Aby pobrać zasady konfiguracji dla określonego klienta, najpierw Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="7730c-119">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="7730c-120">Następnie Wywołaj metodę [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) z identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.</span><span class="sxs-lookup"><span data-stu-id="7730c-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="7730c-121">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) w celu pobrania zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7730c-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="7730c-122">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7730c-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7730c-123">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="7730c-123">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7730c-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7730c-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7730c-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7730c-125">Request syntax</span></span>

| <span data-ttu-id="7730c-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="7730c-126">Method</span></span>  | <span data-ttu-id="7730c-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7730c-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7730c-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="7730c-128">**GET**</span></span> | <span data-ttu-id="7730c-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7730c-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7730c-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7730c-130">URI parameter</span></span>

<span data-ttu-id="7730c-131">Podczas tworzenia żądania Użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="7730c-131">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="7730c-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7730c-132">Name</span></span>        | <span data-ttu-id="7730c-133">Typ</span><span class="sxs-lookup"><span data-stu-id="7730c-133">Type</span></span>   | <span data-ttu-id="7730c-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7730c-134">Required</span></span> | <span data-ttu-id="7730c-135">Opis</span><span class="sxs-lookup"><span data-stu-id="7730c-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7730c-136">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="7730c-136">customer-id</span></span> | <span data-ttu-id="7730c-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="7730c-137">string</span></span> | <span data-ttu-id="7730c-138">Tak</span><span class="sxs-lookup"><span data-stu-id="7730c-138">Yes</span></span>      | <span data-ttu-id="7730c-139">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="7730c-139">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="7730c-140">Identyfikator zasad</span><span class="sxs-lookup"><span data-stu-id="7730c-140">policy-id</span></span>   | <span data-ttu-id="7730c-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="7730c-141">string</span></span> | <span data-ttu-id="7730c-142">Tak</span><span class="sxs-lookup"><span data-stu-id="7730c-142">Yes</span></span>      | <span data-ttu-id="7730c-143">Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje zasady.</span><span class="sxs-lookup"><span data-stu-id="7730c-143">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="7730c-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7730c-144">Request headers</span></span>

<span data-ttu-id="7730c-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7730c-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7730c-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7730c-146">Request body</span></span>

<span data-ttu-id="7730c-147">Brak</span><span class="sxs-lookup"><span data-stu-id="7730c-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7730c-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7730c-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7730c-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7730c-149">REST response</span></span>

<span data-ttu-id="7730c-150">Jeśli to się powiedzie, odpowiedź zawiera żądany zasób [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) .</span><span class="sxs-lookup"><span data-stu-id="7730c-150">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7730c-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7730c-151">Response success and error codes</span></span>

<span data-ttu-id="7730c-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="7730c-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7730c-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7730c-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7730c-154">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7730c-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7730c-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7730c-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
