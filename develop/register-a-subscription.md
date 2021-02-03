---
title: Rejestrowanie subskrypcji
description: Zarejestruj istniejącą subskrypcję, aby umożliwić jej zamawianie rezerwacji platformy Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768309"
---
# <a name="register-a-subscription"></a><span data-ttu-id="1f957-103">Rejestrowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1f957-103">Register a subscription</span></span>

<span data-ttu-id="1f957-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="1f957-104">**Applies To**</span></span>

- <span data-ttu-id="1f957-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="1f957-105">Partner Center</span></span>

<span data-ttu-id="1f957-106">Zarejestruj istniejącą [subskrypcję](subscription-resources.md) , aby umożliwić jej zamawianie rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f957-106">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="1f957-107">Aby kupić rezerwację platformy Azure, musisz mieć co najmniej jedną istniejącą subskrypcję platformy Azure z dostawcą usług kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="1f957-107">To purchase an Azure reservation you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="1f957-108">Ta metoda umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure w ramach dostawcy CSP i włączenie jej do kupowania rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f957-108">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f957-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f957-109">Prerequisites</span></span>

- <span data-ttu-id="1f957-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1f957-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1f957-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1f957-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1f957-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1f957-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1f957-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1f957-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1f957-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="1f957-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1f957-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="1f957-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1f957-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="1f957-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1f957-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1f957-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1f957-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1f957-118">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="1f957-119">C\#</span><span class="sxs-lookup"><span data-stu-id="1f957-119">C\#</span></span>

<span data-ttu-id="1f957-120">Aby zarejestrować subskrypcję klienta, Pobierz interfejs do operacji subskrypcji, wywołując metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="1f957-120">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="1f957-121">Następnie Wywołaj metodę [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) z identyfikatorem subskrypcji, aby zidentyfikować rejestrację, która zostanie zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="1f957-121">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="1f957-122">Na koniec Wywołaj metodę **Registration. Register ()** w celu zarejestrowania subskrypcji i pobrania identyfikatora URI, którego można użyć do pobrania stanu rejestracji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1f957-122">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="1f957-123">Aby uzyskać więcej informacji, zobacz [pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="1f957-123">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="1f957-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1f957-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1f957-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1f957-125">Request syntax</span></span>

| <span data-ttu-id="1f957-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="1f957-126">Method</span></span>    | <span data-ttu-id="1f957-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1f957-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f957-128">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="1f957-128">**POST**</span></span>  | <span data-ttu-id="1f957-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/registrations http/1.1</span><span class="sxs-lookup"><span data-stu-id="1f957-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="1f957-130">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="1f957-130">URI parameters</span></span>

<span data-ttu-id="1f957-131">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="1f957-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="1f957-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1f957-132">Name</span></span>                    | <span data-ttu-id="1f957-133">Typ</span><span class="sxs-lookup"><span data-stu-id="1f957-133">Type</span></span>       | <span data-ttu-id="1f957-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1f957-134">Required</span></span> | <span data-ttu-id="1f957-135">Opis</span><span class="sxs-lookup"><span data-stu-id="1f957-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="1f957-136">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="1f957-136">customer-id</span></span>             | <span data-ttu-id="1f957-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="1f957-137">string</span></span>     | <span data-ttu-id="1f957-138">Tak</span><span class="sxs-lookup"><span data-stu-id="1f957-138">Yes</span></span>      | <span data-ttu-id="1f957-139">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="1f957-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="1f957-140">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1f957-140">subscription-id</span></span>         | <span data-ttu-id="1f957-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="1f957-141">string</span></span>     | <span data-ttu-id="1f957-142">Tak</span><span class="sxs-lookup"><span data-stu-id="1f957-142">Yes</span></span>      | <span data-ttu-id="1f957-143">Ciąg w formacie GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="1f957-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="1f957-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1f957-144">Request headers</span></span>

<span data-ttu-id="1f957-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1f957-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1f957-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1f957-146">Request body</span></span>

<span data-ttu-id="1f957-147">Brak.</span><span class="sxs-lookup"><span data-stu-id="1f957-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1f957-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1f957-148">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="1f957-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1f957-149">REST response</span></span>

<span data-ttu-id="1f957-150">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **lokalizacji** z identyfikatorem URI, którego można użyć do pobrania stanu rejestracji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1f957-150">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="1f957-151">Zapisz ten identyfikator URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="1f957-151">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="1f957-152">Aby zapoznać się z przykładem sposobu pobierania stanu, zobacz [pobieranie stanu rejestracji subskrypcji](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="1f957-152">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1f957-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1f957-153">Response success and error codes</span></span>

<span data-ttu-id="1f957-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="1f957-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1f957-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1f957-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1f957-156">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1f957-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1f957-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1f957-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
