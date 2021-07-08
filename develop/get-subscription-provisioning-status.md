---
title: Pobieranie stanu aprowizacji subskrypcji
description: Jak uzyskać stan aprowizowania subskrypcji dla subskrypcji klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8797fa494cd77f11a1179d6406ca021f0d7788c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548706"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="1ee26-103">Pobieranie stanu aprowizacji subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1ee26-103">Get subscription provisioning status</span></span>

<span data-ttu-id="1ee26-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1ee26-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1ee26-105">Jak uzyskać stan aprowizowania subskrypcji dla subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="1ee26-105">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ee26-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1ee26-106">Prerequisites</span></span>

- <span data-ttu-id="1ee26-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1ee26-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ee26-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ee26-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1ee26-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ee26-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1ee26-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1ee26-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1ee26-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="1ee26-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1ee26-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="1ee26-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1ee26-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="1ee26-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1ee26-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ee26-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1ee26-115">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1ee26-115">A subscription identifier.</span></span>

- <span data-ttu-id="1ee26-116">Do wykonania tej operacji wymagane są delegowane uprawnienia administratora w subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1ee26-116">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="1ee26-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1ee26-117">C\#</span></span>

<span data-ttu-id="1ee26-118">Aby uzyskać stan aprowacji subskrypcji, zacznij od użycia metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="1ee26-118">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="1ee26-119">Następnie pobierz interfejs do operacji subskrypcji, wywołując metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1ee26-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="1ee26-120">Następnie użyj właściwości [**ProvisioningStatus,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) aby uzyskać interfejs dla operacji stanu aprowacji bieżącej subskrypcji, a następnie wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) aby pobrać obiekt [**SubscriptionProvisioningStatus.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus)</span><span class="sxs-lookup"><span data-stu-id="1ee26-120">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="1ee26-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1ee26-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1ee26-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1ee26-122">Request syntax</span></span>

| <span data-ttu-id="1ee26-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="1ee26-123">Method</span></span>  | <span data-ttu-id="1ee26-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1ee26-124">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ee26-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1ee26-125">**GET**</span></span> | <span data-ttu-id="1ee26-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1ee26-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="1ee26-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="1ee26-127">URI parameters</span></span>

<span data-ttu-id="1ee26-128">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="1ee26-128">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="1ee26-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1ee26-129">Name</span></span>            | <span data-ttu-id="1ee26-130">Typ</span><span class="sxs-lookup"><span data-stu-id="1ee26-130">Type</span></span>   | <span data-ttu-id="1ee26-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1ee26-131">Required</span></span> | <span data-ttu-id="1ee26-132">Opis</span><span class="sxs-lookup"><span data-stu-id="1ee26-132">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="1ee26-133">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="1ee26-133">customer-id</span></span>     | <span data-ttu-id="1ee26-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="1ee26-134">string</span></span> | <span data-ttu-id="1ee26-135">Tak</span><span class="sxs-lookup"><span data-stu-id="1ee26-135">Yes</span></span>      | <span data-ttu-id="1ee26-136">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="1ee26-136">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="1ee26-137">subscription-id</span><span class="sxs-lookup"><span data-stu-id="1ee26-137">subscription-id</span></span> | <span data-ttu-id="1ee26-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="1ee26-138">string</span></span> | <span data-ttu-id="1ee26-139">Tak</span><span class="sxs-lookup"><span data-stu-id="1ee26-139">Yes</span></span>      | <span data-ttu-id="1ee26-140">Ciąg w formacie identyfikatora GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="1ee26-140">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1ee26-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1ee26-141">Request headers</span></span>

<span data-ttu-id="1ee26-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1ee26-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1ee26-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1ee26-143">Request body</span></span>

<span data-ttu-id="1ee26-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="1ee26-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1ee26-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1ee26-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1ee26-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1ee26-146">REST response</span></span>

<span data-ttu-id="1ee26-147">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób SubscriptionProvisioningStatus.](subscription-resources.md#subscriptionprovisioningstatus)</span><span class="sxs-lookup"><span data-stu-id="1ee26-147">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1ee26-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1ee26-148">Response success and error codes</span></span>

<span data-ttu-id="1ee26-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1ee26-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1ee26-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1ee26-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1ee26-151">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1ee26-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1ee26-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1ee26-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a><span data-ttu-id="1ee26-153">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1ee26-153">Remarks</span></span>

- <span data-ttu-id="1ee26-154">Podczas przypisywania zmiany licencji pole stanu w obszarze [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) jest ustawione na wartość "oczekujące".</span><span class="sxs-lookup"><span data-stu-id="1ee26-154">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="1ee26-155">Pole stanu jest aktualizowane co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="1ee26-155">The status field is updated every 15 minutes.</span></span>
