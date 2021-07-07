---
title: Pobieranie zasad konfiguracji klienta
description: Jak pobrać określone zasady konfiguracji dla określonego klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f9a8cb435c63d8d02c3b4633abc8723353116f37
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547499"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="bdfba-103">Pobieranie zasad konfiguracji klienta</span><span class="sxs-lookup"><span data-stu-id="bdfba-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="bdfba-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="bdfba-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="bdfba-105">Jak pobrać określone zasady konfiguracji dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="bdfba-105">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdfba-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bdfba-106">Prerequisites</span></span>

- <span data-ttu-id="bdfba-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bdfba-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bdfba-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bdfba-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bdfba-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bdfba-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bdfba-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="bdfba-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bdfba-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="bdfba-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bdfba-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="bdfba-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bdfba-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="bdfba-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bdfba-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bdfba-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="bdfba-115">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="bdfba-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="bdfba-116">C\#</span><span class="sxs-lookup"><span data-stu-id="bdfba-116">C\#</span></span>

<span data-ttu-id="bdfba-117">Aby pobrać zasady konfiguracji dla określonego klienta, najpierw wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="bdfba-117">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="bdfba-118">Następnie wywołaj metodę [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) z identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.</span><span class="sxs-lookup"><span data-stu-id="bdfba-118">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="bdfba-119">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) aby pobrać zasady konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bdfba-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="bdfba-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bdfba-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bdfba-121">**Project:** zestaw SDK Centrum partnerskiego Samples Class : GetConfigurationPolicy.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: GetConfigurationPolicy.cs)</span><span class="sxs-lookup"><span data-stu-id="bdfba-121">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bdfba-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="bdfba-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bdfba-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="bdfba-123">Request syntax</span></span>

| <span data-ttu-id="bdfba-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="bdfba-124">Method</span></span>  | <span data-ttu-id="bdfba-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="bdfba-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bdfba-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="bdfba-126">**GET**</span></span> | <span data-ttu-id="bdfba-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bdfba-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bdfba-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="bdfba-128">URI parameter</span></span>

<span data-ttu-id="bdfba-129">Podczas tworzenia żądania użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="bdfba-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="bdfba-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bdfba-130">Name</span></span>        | <span data-ttu-id="bdfba-131">Typ</span><span class="sxs-lookup"><span data-stu-id="bdfba-131">Type</span></span>   | <span data-ttu-id="bdfba-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bdfba-132">Required</span></span> | <span data-ttu-id="bdfba-133">Opis</span><span class="sxs-lookup"><span data-stu-id="bdfba-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="bdfba-134">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="bdfba-134">customer-id</span></span> | <span data-ttu-id="bdfba-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="bdfba-135">string</span></span> | <span data-ttu-id="bdfba-136">Tak</span><span class="sxs-lookup"><span data-stu-id="bdfba-136">Yes</span></span>      | <span data-ttu-id="bdfba-137">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="bdfba-137">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="bdfba-138">identyfikator zasad</span><span class="sxs-lookup"><span data-stu-id="bdfba-138">policy-id</span></span>   | <span data-ttu-id="bdfba-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="bdfba-139">string</span></span> | <span data-ttu-id="bdfba-140">Tak</span><span class="sxs-lookup"><span data-stu-id="bdfba-140">Yes</span></span>      | <span data-ttu-id="bdfba-141">Ciąg w formacie identyfikatora GUID, który identyfikuje zasady.</span><span class="sxs-lookup"><span data-stu-id="bdfba-141">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="bdfba-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="bdfba-142">Request headers</span></span>

<span data-ttu-id="bdfba-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bdfba-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bdfba-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="bdfba-144">Request body</span></span>

<span data-ttu-id="bdfba-145">Brak</span><span class="sxs-lookup"><span data-stu-id="bdfba-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="bdfba-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="bdfba-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="bdfba-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="bdfba-147">REST response</span></span>

<span data-ttu-id="bdfba-148">W przypadku powodzenia odpowiedź zawiera żądany [zasób ConfigurationPolicy.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="bdfba-148">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bdfba-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bdfba-149">Response success and error codes</span></span>

<span data-ttu-id="bdfba-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="bdfba-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bdfba-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="bdfba-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bdfba-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bdfba-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bdfba-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bdfba-153">Response example</span></span>

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
