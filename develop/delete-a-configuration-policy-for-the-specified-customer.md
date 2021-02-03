---
title: Usuwanie zasad konfiguracji dla określonego klienta
description: Jak usunąć zasady konfiguracji dla określonego identyfikatora klienta i zasad.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 586878367fc0873ef0fb1415799b2b7022954053
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768134"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="731f6-103">Usuwanie zasad konfiguracji dla określonego klienta</span><span class="sxs-lookup"><span data-stu-id="731f6-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="731f6-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="731f6-104">**Applies to:**</span></span>

- <span data-ttu-id="731f6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="731f6-105">Partner Center</span></span>
- <span data-ttu-id="731f6-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="731f6-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="731f6-107">Jak usunąć zasady konfiguracji dla określonego identyfikatora klienta i zasad.</span><span class="sxs-lookup"><span data-stu-id="731f6-107">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="731f6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="731f6-108">Prerequisites</span></span>

- <span data-ttu-id="731f6-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="731f6-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="731f6-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="731f6-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="731f6-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="731f6-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="731f6-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="731f6-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="731f6-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="731f6-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="731f6-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="731f6-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="731f6-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="731f6-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="731f6-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="731f6-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="731f6-117">Identyfikator zasad.</span><span class="sxs-lookup"><span data-stu-id="731f6-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="731f6-118">C\#</span><span class="sxs-lookup"><span data-stu-id="731f6-118">C\#</span></span>

<span data-ttu-id="731f6-119">Aby usunąć zasady konfiguracji dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="731f6-119">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="731f6-120">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="731f6-120">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="731f6-121">Wywołaj metodę [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) z identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.</span><span class="sxs-lookup"><span data-stu-id="731f6-121">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="731f6-122">Wywołaj metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) lub [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) , aby usunąć zasady konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="731f6-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="731f6-123">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="731f6-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="731f6-124">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="731f6-124">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="731f6-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="731f6-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="731f6-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="731f6-126">Request syntax</span></span>

| <span data-ttu-id="731f6-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="731f6-127">Method</span></span>     | <span data-ttu-id="731f6-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="731f6-128">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="731f6-129">**USUNIĘTY**</span><span class="sxs-lookup"><span data-stu-id="731f6-129">**DELETE**</span></span> | <span data-ttu-id="731f6-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="731f6-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="731f6-131">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="731f6-131">URI parameters</span></span>

<span data-ttu-id="731f6-132">Podczas tworzenia żądania Użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="731f6-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="731f6-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="731f6-133">Name</span></span>        | <span data-ttu-id="731f6-134">Typ</span><span class="sxs-lookup"><span data-stu-id="731f6-134">Type</span></span>   | <span data-ttu-id="731f6-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="731f6-135">Required</span></span> | <span data-ttu-id="731f6-136">Opis</span><span class="sxs-lookup"><span data-stu-id="731f6-136">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="731f6-137">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="731f6-137">customer-id</span></span> | <span data-ttu-id="731f6-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="731f6-138">string</span></span> | <span data-ttu-id="731f6-139">Tak</span><span class="sxs-lookup"><span data-stu-id="731f6-139">Yes</span></span>      | <span data-ttu-id="731f6-140">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="731f6-140">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="731f6-141">Identyfikator zasad</span><span class="sxs-lookup"><span data-stu-id="731f6-141">policy-id</span></span>   | <span data-ttu-id="731f6-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="731f6-142">string</span></span> | <span data-ttu-id="731f6-143">Tak</span><span class="sxs-lookup"><span data-stu-id="731f6-143">Yes</span></span>      | <span data-ttu-id="731f6-144">Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje zasady do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="731f6-144">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="731f6-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="731f6-145">Request headers</span></span>

<span data-ttu-id="731f6-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="731f6-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="731f6-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="731f6-147">Request body</span></span>

<span data-ttu-id="731f6-148">Brak</span><span class="sxs-lookup"><span data-stu-id="731f6-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="731f6-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="731f6-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="731f6-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="731f6-150">REST response</span></span>

<span data-ttu-id="731f6-151">Jeśli to się powiedzie, odpowiedź zwróci 204 kod stanu zawartości.</span><span class="sxs-lookup"><span data-stu-id="731f6-151">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="731f6-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="731f6-152">Response success and error codes</span></span>

<span data-ttu-id="731f6-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="731f6-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="731f6-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="731f6-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="731f6-155">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="731f6-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="731f6-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="731f6-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
