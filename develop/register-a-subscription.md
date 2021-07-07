---
title: Rejestrowanie subskrypcji
description: Zarejestruj istniejącą subskrypcję, aby umożliwić jej zamawianie rezerwacji platformy Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446619"
---
# <a name="register-a-subscription"></a><span data-ttu-id="fe369-103">Rejestrowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fe369-103">Register a subscription</span></span>

<span data-ttu-id="fe369-104">Zarejestruj istniejącą [subskrypcję,](subscription-resources.md) aby umożliwić jej zamawianie rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe369-104">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="fe369-105">Aby kupić rezerwację platformy Azure, musisz mieć co najmniej jedną istniejącą subskrypcję platformy Azure dla programu CSP.</span><span class="sxs-lookup"><span data-stu-id="fe369-105">To purchase an Azure reservation, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="fe369-106">Ta metoda umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure dla programu CSP, co umożliwia zakup rezerwacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe369-106">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe369-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe369-107">Prerequisites</span></span>

- <span data-ttu-id="fe369-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fe369-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fe369-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe369-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fe369-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fe369-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fe369-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="fe369-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fe369-112">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="fe369-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fe369-113">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="fe369-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fe369-114">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="fe369-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fe369-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fe369-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fe369-116">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fe369-116">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="fe369-117">C\#</span><span class="sxs-lookup"><span data-stu-id="fe369-117">C\#</span></span>

<span data-ttu-id="fe369-118">Aby zarejestrować subskrypcję klienta, pobierz interfejs do operacji subskrypcji, wywołując metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="fe369-118">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="fe369-119">Następnie wywołaj metodę [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) z identyfikatorem subskrypcji, aby zidentyfikować rejestrowany subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="fe369-119">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="fe369-120">Na koniec wywołaj metodę **Registration.Register(),** aby zarejestrować subskrypcję i pobrać jej kod URI, który może służyć do uzyskania stanu rejestracji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fe369-120">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="fe369-121">Aby uzyskać więcej informacji, zobacz Get subscription registration status (Uzyskiwanie [stanu rejestracji subskrypcji).](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="fe369-121">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="fe369-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fe369-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fe369-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fe369-123">Request syntax</span></span>

| <span data-ttu-id="fe369-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="fe369-124">Method</span></span>    | <span data-ttu-id="fe369-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fe369-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fe369-126">**Post**</span><span class="sxs-lookup"><span data-stu-id="fe369-126">**POST**</span></span>  | <span data-ttu-id="fe369-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/registrations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fe369-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="fe369-128">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="fe369-128">URI parameters</span></span>

<span data-ttu-id="fe369-129">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="fe369-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="fe369-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fe369-130">Name</span></span>                    | <span data-ttu-id="fe369-131">Typ</span><span class="sxs-lookup"><span data-stu-id="fe369-131">Type</span></span>       | <span data-ttu-id="fe369-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fe369-132">Required</span></span> | <span data-ttu-id="fe369-133">Opis</span><span class="sxs-lookup"><span data-stu-id="fe369-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="fe369-134">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="fe369-134">customer-id</span></span>             | <span data-ttu-id="fe369-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="fe369-135">string</span></span>     | <span data-ttu-id="fe369-136">Tak</span><span class="sxs-lookup"><span data-stu-id="fe369-136">Yes</span></span>      | <span data-ttu-id="fe369-137">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="fe369-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="fe369-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="fe369-138">subscription-id</span></span>         | <span data-ttu-id="fe369-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="fe369-139">string</span></span>     | <span data-ttu-id="fe369-140">Tak</span><span class="sxs-lookup"><span data-stu-id="fe369-140">Yes</span></span>      | <span data-ttu-id="fe369-141">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="fe369-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="fe369-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fe369-142">Request headers</span></span>

<span data-ttu-id="fe369-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fe369-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fe369-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fe369-144">Request body</span></span>

<span data-ttu-id="fe369-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="fe369-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fe369-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fe369-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fe369-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fe369-147">REST response</span></span>

<span data-ttu-id="fe369-148">Jeśli to się powiedzie, odpowiedź zawiera nagłówek **Location** (Lokalizacja) z URI, który może służyć do pobierania stanu rejestracji subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fe369-148">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="fe369-149">Zapisz ten URI do użycia z innymi powiązanymi interfejsami API REST.</span><span class="sxs-lookup"><span data-stu-id="fe369-149">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="fe369-150">Aby uzyskać przykład sposobu pobierania stanu, zobacz [Pobieranie stanu rejestracji subskrypcji.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="fe369-150">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fe369-151">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fe369-151">Response success and error codes</span></span>

<span data-ttu-id="fe369-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="fe369-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fe369-153">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fe369-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fe369-154">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fe369-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fe369-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fe369-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
