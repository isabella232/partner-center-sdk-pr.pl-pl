---
title: Pobieranie stanu rejestracji subskrypcji
description: Pobierz stan subskrypcji, która została zarejestrowana do użycia z Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768441"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="cc006-103">Pobieranie stanu rejestracji subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cc006-103">Get subscription registration status</span></span>

<span data-ttu-id="cc006-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="cc006-104">**Applies To**</span></span>

- <span data-ttu-id="cc006-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="cc006-105">Partner Center</span></span>

<span data-ttu-id="cc006-106">Jak uzyskać informacje o stanie rejestracji subskrypcji klienta, dla którego włączono kupowanie Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="cc006-106">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="cc006-107">Aby kupić wystąpienie zarezerwowane maszyny wirtualnej platformy Azure przy użyciu interfejsu API Centrum partnerskiego, musisz mieć co najmniej jedną subskrypcję platformy Azure dla dostawcy CSP.</span><span class="sxs-lookup"><span data-stu-id="cc006-107">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="cc006-108">Metoda [zarejestruj subskrypcję](register-a-subscription.md) umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure w ramach dostawcy CSP i włączenie jej do Azure Reserved VM Instances zakupów.</span><span class="sxs-lookup"><span data-stu-id="cc006-108">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="cc006-109">Ta metoda umożliwia pobranie stanu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cc006-109">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc006-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cc006-110">Prerequisites</span></span>

- <span data-ttu-id="cc006-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cc006-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cc006-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc006-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cc006-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cc006-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cc006-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="cc006-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cc006-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="cc006-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cc006-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="cc006-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cc006-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="cc006-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cc006-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cc006-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cc006-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cc006-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="cc006-120">C\#</span><span class="sxs-lookup"><span data-stu-id="cc006-120">C\#</span></span>

<span data-ttu-id="cc006-121">Aby uzyskać stan rejestracji subskrypcji, Zacznij od użycia metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="cc006-121">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="cc006-122">Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) przy użyciu identyfikatora subskrypcji, aby zidentyfikować subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="cc006-122">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="cc006-123">Następnie użyj właściwości RegistrationStatus, aby uzyskać interfejs do operacji stanu rejestracji bieżącej subskrypcji, i Wywołaj metodę **Get** lub **GetAsync** , aby pobrać obiekt **SubscriptionRegistrationStatus** .</span><span class="sxs-lookup"><span data-stu-id="cc006-123">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="cc006-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cc006-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cc006-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cc006-125">Request syntax</span></span>

| <span data-ttu-id="cc006-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="cc006-126">Method</span></span>    | <span data-ttu-id="cc006-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cc006-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc006-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cc006-128">**GET**</span></span>  | <span data-ttu-id="cc006-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/registrationstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="cc006-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="cc006-130">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="cc006-130">URI parameters</span></span>

<span data-ttu-id="cc006-131">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="cc006-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="cc006-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cc006-132">Name</span></span>                    | <span data-ttu-id="cc006-133">Typ</span><span class="sxs-lookup"><span data-stu-id="cc006-133">Type</span></span>       | <span data-ttu-id="cc006-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cc006-134">Required</span></span> | <span data-ttu-id="cc006-135">Opis</span><span class="sxs-lookup"><span data-stu-id="cc006-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="cc006-136">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="cc006-136">customer-id</span></span>             | <span data-ttu-id="cc006-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc006-137">string</span></span>     | <span data-ttu-id="cc006-138">Tak</span><span class="sxs-lookup"><span data-stu-id="cc006-138">Yes</span></span>      | <span data-ttu-id="cc006-139">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="cc006-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="cc006-140">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cc006-140">subscription-id</span></span>         | <span data-ttu-id="cc006-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc006-141">string</span></span>     | <span data-ttu-id="cc006-142">Tak</span><span class="sxs-lookup"><span data-stu-id="cc006-142">Yes</span></span>      | <span data-ttu-id="cc006-143">Ciąg w formacie GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="cc006-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="cc006-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cc006-144">Request headers</span></span>

<span data-ttu-id="cc006-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cc006-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cc006-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cc006-146">Request body</span></span>

<span data-ttu-id="cc006-147">Brak.</span><span class="sxs-lookup"><span data-stu-id="cc006-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cc006-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cc006-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="cc006-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cc006-149">REST response</span></span>

<span data-ttu-id="cc006-150">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) .</span><span class="sxs-lookup"><span data-stu-id="cc006-150">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cc006-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cc006-151">Response success and error codes</span></span>

<span data-ttu-id="cc006-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="cc006-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cc006-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cc006-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cc006-154">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cc006-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cc006-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cc006-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
