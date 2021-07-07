---
title: Usuwanie zasad konfiguracji dla określonego klienta
description: Jak usunąć zasady konfiguracji dla określonego klienta i identyfikator zasad.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973030"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="041dc-103">Usuwanie zasad konfiguracji dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="041dc-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="041dc-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="041dc-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="041dc-105">Jak usunąć zasady konfiguracji dla określonego klienta i identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="041dc-105">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="041dc-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="041dc-106">Prerequisites</span></span>

- <span data-ttu-id="041dc-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="041dc-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="041dc-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="041dc-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="041dc-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="041dc-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="041dc-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="041dc-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="041dc-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="041dc-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="041dc-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="041dc-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="041dc-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="041dc-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="041dc-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="041dc-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="041dc-115">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="041dc-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="041dc-116">C\#</span><span class="sxs-lookup"><span data-stu-id="041dc-116">C\#</span></span>

<span data-ttu-id="041dc-117">Aby usunąć zasady konfiguracji dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="041dc-117">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="041dc-118">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="041dc-118">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="041dc-119">Wywołaj [**metodę ConfigurationPolicies.ById z**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.</span><span class="sxs-lookup"><span data-stu-id="041dc-119">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="041dc-120">Wywołaj [**metodę Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) lub [**DeleteAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) aby usunąć zasady konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="041dc-120">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="041dc-121">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="041dc-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="041dc-122">**Project**: zestaw SDK Centrum partnerskiego Samples Class : DeleteConfigurationPolicy.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: DeleteConfigurationPolicy.cs)</span><span class="sxs-lookup"><span data-stu-id="041dc-122">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="041dc-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="041dc-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="041dc-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="041dc-124">Request syntax</span></span>

| <span data-ttu-id="041dc-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="041dc-125">Method</span></span>     | <span data-ttu-id="041dc-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="041dc-126">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="041dc-127">**Usunąć**</span><span class="sxs-lookup"><span data-stu-id="041dc-127">**DELETE**</span></span> | <span data-ttu-id="041dc-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="041dc-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="041dc-129">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="041dc-129">URI parameters</span></span>

<span data-ttu-id="041dc-130">Podczas tworzenia żądania użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="041dc-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="041dc-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="041dc-131">Name</span></span>        | <span data-ttu-id="041dc-132">Typ</span><span class="sxs-lookup"><span data-stu-id="041dc-132">Type</span></span>   | <span data-ttu-id="041dc-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="041dc-133">Required</span></span> | <span data-ttu-id="041dc-134">Opis</span><span class="sxs-lookup"><span data-stu-id="041dc-134">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="041dc-135">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="041dc-135">customer-id</span></span> | <span data-ttu-id="041dc-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="041dc-136">string</span></span> | <span data-ttu-id="041dc-137">Tak</span><span class="sxs-lookup"><span data-stu-id="041dc-137">Yes</span></span>      | <span data-ttu-id="041dc-138">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="041dc-138">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="041dc-139">identyfikator zasad</span><span class="sxs-lookup"><span data-stu-id="041dc-139">policy-id</span></span>   | <span data-ttu-id="041dc-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="041dc-140">string</span></span> | <span data-ttu-id="041dc-141">Tak</span><span class="sxs-lookup"><span data-stu-id="041dc-141">Yes</span></span>      | <span data-ttu-id="041dc-142">Ciąg w formacie identyfikatora GUID, który identyfikuje zasady do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="041dc-142">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="041dc-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="041dc-143">Request headers</span></span>

<span data-ttu-id="041dc-144">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="041dc-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="041dc-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="041dc-145">Request body</span></span>

<span data-ttu-id="041dc-146">Brak</span><span class="sxs-lookup"><span data-stu-id="041dc-146">None</span></span>

### <a name="request-example"></a><span data-ttu-id="041dc-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="041dc-147">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="041dc-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="041dc-148">REST response</span></span>

<span data-ttu-id="041dc-149">Jeśli to się powiedzie, odpowiedź zwróci kod stanu 204 Brak zawartości.</span><span class="sxs-lookup"><span data-stu-id="041dc-149">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="041dc-150">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="041dc-150">Response success and error codes</span></span>

<span data-ttu-id="041dc-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="041dc-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="041dc-152">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="041dc-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="041dc-153">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="041dc-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="041dc-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="041dc-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
