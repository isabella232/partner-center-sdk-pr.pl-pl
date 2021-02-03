---
title: Pobieranie stanu aprowizacji subskrypcji
description: Jak uzyskać status aprowizacji subskrypcji klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38544aa380ba0a6a8804ae45f7d8ae7cb431d3ba
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768437"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="6d7a8-103">Pobieranie stanu aprowizacji subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6d7a8-103">Get subscription provisioning status</span></span>

<span data-ttu-id="6d7a8-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="6d7a8-104">**Applies To**</span></span>

- <span data-ttu-id="6d7a8-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="6d7a8-105">Partner Center</span></span>
- <span data-ttu-id="6d7a8-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="6d7a8-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6d7a8-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="6d7a8-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6d7a8-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6d7a8-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6d7a8-109">Jak uzyskać status aprowizacji subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-109">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d7a8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6d7a8-110">Prerequisites</span></span>

- <span data-ttu-id="6d7a8-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6d7a8-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6d7a8-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6d7a8-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6d7a8-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6d7a8-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6d7a8-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6d7a8-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6d7a8-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="6d7a8-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6d7a8-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6d7a8-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6d7a8-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-119">A subscription identifier.</span></span>

- <span data-ttu-id="6d7a8-120">Do wykonania tej operacji są wymagane uprawnienia administratora delegowanego.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-120">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="6d7a8-121">C\#</span><span class="sxs-lookup"><span data-stu-id="6d7a8-121">C\#</span></span>

<span data-ttu-id="6d7a8-122">Aby uzyskać stan aprowizacji subskrypcji, Zacznij od użycia metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-122">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="6d7a8-123">Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę Subscription [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-123">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="6d7a8-124">Następnie użyj właściwości [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) , aby uzyskać interfejs do operacji stanu aprowizacji bieżącej subskrypcji, a następnie Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) , aby pobrać obiekt [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) .</span><span class="sxs-lookup"><span data-stu-id="6d7a8-124">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="6d7a8-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6d7a8-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6d7a8-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6d7a8-126">Request syntax</span></span>

| <span data-ttu-id="6d7a8-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="6d7a8-127">Method</span></span>  | <span data-ttu-id="6d7a8-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6d7a8-128">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6d7a8-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="6d7a8-129">**GET**</span></span> | <span data-ttu-id="6d7a8-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/provisioningstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="6d7a8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="6d7a8-131">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="6d7a8-131">URI parameters</span></span>

<span data-ttu-id="6d7a8-132">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="6d7a8-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6d7a8-133">Name</span></span>            | <span data-ttu-id="6d7a8-134">Typ</span><span class="sxs-lookup"><span data-stu-id="6d7a8-134">Type</span></span>   | <span data-ttu-id="6d7a8-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6d7a8-135">Required</span></span> | <span data-ttu-id="6d7a8-136">Opis</span><span class="sxs-lookup"><span data-stu-id="6d7a8-136">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="6d7a8-137">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="6d7a8-137">customer-id</span></span>     | <span data-ttu-id="6d7a8-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="6d7a8-138">string</span></span> | <span data-ttu-id="6d7a8-139">Tak</span><span class="sxs-lookup"><span data-stu-id="6d7a8-139">Yes</span></span>      | <span data-ttu-id="6d7a8-140">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-140">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="6d7a8-141">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6d7a8-141">subscription-id</span></span> | <span data-ttu-id="6d7a8-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="6d7a8-142">string</span></span> | <span data-ttu-id="6d7a8-143">Tak</span><span class="sxs-lookup"><span data-stu-id="6d7a8-143">Yes</span></span>      | <span data-ttu-id="6d7a8-144">Ciąg w formacie GUID, który identyfikuje subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-144">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6d7a8-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6d7a8-145">Request headers</span></span>

<span data-ttu-id="6d7a8-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6d7a8-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6d7a8-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6d7a8-147">Request body</span></span>

<span data-ttu-id="6d7a8-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6d7a8-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6d7a8-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6d7a8-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6d7a8-150">REST response</span></span>

<span data-ttu-id="6d7a8-151">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) .</span><span class="sxs-lookup"><span data-stu-id="6d7a8-151">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6d7a8-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6d7a8-152">Response success and error codes</span></span>

<span data-ttu-id="6d7a8-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6d7a8-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6d7a8-155">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6d7a8-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6d7a8-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6d7a8-156">Response example</span></span>

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

## <a name="remarks"></a><span data-ttu-id="6d7a8-157">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6d7a8-157">Remarks</span></span>

- <span data-ttu-id="6d7a8-158">Podczas przypisywania zmiany licencji pole Stan w [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) ma wartość "oczekiwanie".</span><span class="sxs-lookup"><span data-stu-id="6d7a8-158">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="6d7a8-159">Pole Stan jest aktualizowane co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="6d7a8-159">The status field is updated every fifteen minutes.</span></span>
