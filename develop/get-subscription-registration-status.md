---
title: Pobieranie stanu rejestracji subskrypcji
description: Uzyskaj stan subskrypcji, która została zarejestrowana do użycia z Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e39f94c0eac402a0be3afde84279aa637868f96
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445956"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="6a2a0-103">Pobieranie stanu rejestracji subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6a2a0-103">Get subscription registration status</span></span>

<span data-ttu-id="6a2a0-104">Jak uzyskać stan rejestracji subskrypcji dla subskrypcji klienta, dla których włączono obsługę zakupu Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-104">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="6a2a0-105">Aby kupić wystąpienie zarezerwowane maszyny wirtualnej platformy Azure przy użyciu interfejsu API Partner Center, musisz mieć co najmniej jedną istniejącą subskrypcję platformy Azure dostawcy usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-105">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="6a2a0-106">Metoda [Rejestrowania subskrypcji](register-a-subscription.md) umożliwia zarejestrowanie istniejącej subskrypcji platformy Azure w programie CSP, umożliwiając jej zakup Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-106">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="6a2a0-107">Ta metoda umożliwia pobranie stanu tej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-107">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a2a0-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6a2a0-108">Prerequisites</span></span>

- <span data-ttu-id="6a2a0-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6a2a0-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6a2a0-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6a2a0-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6a2a0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6a2a0-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6a2a0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6a2a0-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="6a2a0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6a2a0-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6a2a0-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6a2a0-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6a2a0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6a2a0-117">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="6a2a0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="6a2a0-118">C\#</span></span>

<span data-ttu-id="6a2a0-119">Aby uzyskać stan rejestracji subskrypcji, zacznij od użycia metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-119">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="6a2a0-120">Następnie pobierz interfejs do operacji subskrypcji, wywołując metodę [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) z identyfikatorem subskrypcji w celu zidentyfikowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-120">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="6a2a0-121">Następnie użyj właściwości RegistrationStatus, aby uzyskać interfejs dla operacji stanu rejestracji bieżącej subskrypcji, i wywołaj metodę **Get** lub **GetAsync,** aby pobrać obiekt **SubscriptionRegistrationStatus.**</span><span class="sxs-lookup"><span data-stu-id="6a2a0-121">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="6a2a0-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6a2a0-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6a2a0-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6a2a0-123">Request syntax</span></span>

| <span data-ttu-id="6a2a0-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="6a2a0-124">Method</span></span>    | <span data-ttu-id="6a2a0-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6a2a0-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6a2a0-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="6a2a0-126">**GET**</span></span>  | <span data-ttu-id="6a2a0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6a2a0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="6a2a0-128">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="6a2a0-128">URI parameters</span></span>

<span data-ttu-id="6a2a0-129">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="6a2a0-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6a2a0-130">Name</span></span>                    | <span data-ttu-id="6a2a0-131">Typ</span><span class="sxs-lookup"><span data-stu-id="6a2a0-131">Type</span></span>       | <span data-ttu-id="6a2a0-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a2a0-132">Required</span></span> | <span data-ttu-id="6a2a0-133">Opis</span><span class="sxs-lookup"><span data-stu-id="6a2a0-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="6a2a0-134">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="6a2a0-134">customer-id</span></span>             | <span data-ttu-id="6a2a0-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="6a2a0-135">string</span></span>     | <span data-ttu-id="6a2a0-136">Tak</span><span class="sxs-lookup"><span data-stu-id="6a2a0-136">Yes</span></span>      | <span data-ttu-id="6a2a0-137">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="6a2a0-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="6a2a0-138">subscription-id</span></span>         | <span data-ttu-id="6a2a0-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="6a2a0-139">string</span></span>     | <span data-ttu-id="6a2a0-140">Tak</span><span class="sxs-lookup"><span data-stu-id="6a2a0-140">Yes</span></span>      | <span data-ttu-id="6a2a0-141">Ciąg w formacie identyfikatora GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="6a2a0-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6a2a0-142">Request headers</span></span>

<span data-ttu-id="6a2a0-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6a2a0-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6a2a0-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6a2a0-144">Request body</span></span>

<span data-ttu-id="6a2a0-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6a2a0-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6a2a0-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6a2a0-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6a2a0-147">REST response</span></span>

<span data-ttu-id="6a2a0-148">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SubscriptionRegistrationStatus.](subscription-resources.md#subscriptionregistrationstatus)</span><span class="sxs-lookup"><span data-stu-id="6a2a0-148">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6a2a0-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6a2a0-149">Response success and error codes</span></span>

<span data-ttu-id="6a2a0-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6a2a0-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6a2a0-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6a2a0-152">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6a2a0-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6a2a0-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6a2a0-153">Response example</span></span>

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
