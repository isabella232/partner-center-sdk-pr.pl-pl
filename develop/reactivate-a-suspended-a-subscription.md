---
title: Ponowne uaktywnianie zawieszonej subskrypcji
description: Ponownie aktywuje subskrypcję, która została wcześniej zawieszona w przypadku niepłaty. Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17c63e9c6d4c9e111bfea28e97319696534fa122
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768285"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="6f3fd-103">Ponowne uaktywnianie zawieszonej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6f3fd-103">Reactivate a suspended subscription</span></span>

<span data-ttu-id="6f3fd-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-104">**Applies To**</span></span>

- <span data-ttu-id="6f3fd-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="6f3fd-105">Partner Center</span></span>
- <span data-ttu-id="6f3fd-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="6f3fd-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6f3fd-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="6f3fd-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6f3fd-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6f3fd-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6f3fd-109">Ponownie aktywuje [subskrypcję](subscription-resources.md) , która została wcześniej zawieszona w przypadku niepłaty.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-109">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="6f3fd-110">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="6f3fd-111">Następnie wybierz subskrypcję, której nazwę chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="6f3fd-112">Aby zakończyć, wybierz przycisk **aktywny** , a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-112">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f3fd-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6f3fd-113">Prerequisites</span></span>

- <span data-ttu-id="6f3fd-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6f3fd-115">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6f3fd-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6f3fd-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6f3fd-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6f3fd-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6f3fd-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="6f3fd-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6f3fd-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6f3fd-122">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="6f3fd-123">C\#</span><span class="sxs-lookup"><span data-stu-id="6f3fd-123">C\#</span></span>

<span data-ttu-id="6f3fd-124">Aby ponownie uaktywnić subskrypcję klienta, najpierw [Uzyskaj subskrypcję](get-a-subscription-by-id.md), a następnie zmień wartość właściwości [**stan**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-124">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="6f3fd-125">Aby uzyskać informacje na temat kodów **stanu** , zapoznaj się z tematem [SubscriptionStatus Enumeration/dotnet/API/Microsoft. Store. partnercenter. models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="6f3fd-126">Po wprowadzeniu zmiany Użyj kolekcji [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="6f3fd-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="6f3fd-127">Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="6f3fd-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="6f3fd-128">Następnie Zakończ, wywołując metodę [**patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .</span><span class="sxs-lookup"><span data-stu-id="6f3fd-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

<span data-ttu-id="6f3fd-129">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6f3fd-130">**Projekt**: FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-130">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="6f3fd-131">**Klasa**: UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="6f3fd-131">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="6f3fd-132">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6f3fd-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6f3fd-133">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6f3fd-133">Request syntax</span></span>

| <span data-ttu-id="6f3fd-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="6f3fd-134">Method</span></span>    | <span data-ttu-id="6f3fd-135">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6f3fd-135">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6f3fd-136">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-136">**PATCH**</span></span> | <span data-ttu-id="6f3fd-137">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6f3fd-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6f3fd-138">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6f3fd-138">URI parameter</span></span>

<span data-ttu-id="6f3fd-139">Ta tabela zawiera listę wymaganych parametrów zapytania, aby ponownie aktywować subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-139">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="6f3fd-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6f3fd-140">Name</span></span>                    | <span data-ttu-id="6f3fd-141">Typ</span><span class="sxs-lookup"><span data-stu-id="6f3fd-141">Type</span></span>     | <span data-ttu-id="6f3fd-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6f3fd-142">Required</span></span> | <span data-ttu-id="6f3fd-143">Opis</span><span class="sxs-lookup"><span data-stu-id="6f3fd-143">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="6f3fd-144">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-144">**customer-tenant-id**</span></span>  | <span data-ttu-id="6f3fd-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-145">**guid**</span></span> | <span data-ttu-id="6f3fd-146">Y</span><span class="sxs-lookup"><span data-stu-id="6f3fd-146">Y</span></span>        | <span data-ttu-id="6f3fd-147">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="6f3fd-148">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-148">**id-for-subscription**</span></span> | <span data-ttu-id="6f3fd-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="6f3fd-149">**guid**</span></span> | <span data-ttu-id="6f3fd-150">Y</span><span class="sxs-lookup"><span data-stu-id="6f3fd-150">Y</span></span>        | <span data-ttu-id="6f3fd-151">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-151">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6f3fd-152">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6f3fd-152">Request headers</span></span>

<span data-ttu-id="6f3fd-153">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6f3fd-154">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6f3fd-154">Request body</span></span>

<span data-ttu-id="6f3fd-155">W treści żądania jest wymagany pełny zasób **subskrypcji** .</span><span class="sxs-lookup"><span data-stu-id="6f3fd-155">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="6f3fd-156">Upewnij się, że właściwość **status** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-156">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="6f3fd-157">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6f3fd-157">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="6f3fd-158">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6f3fd-158">REST response</span></span>

<span data-ttu-id="6f3fd-159">Jeśli to się powiedzie, ta metoda zwraca zaktualizowane właściwości zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-159">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6f3fd-160">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6f3fd-160">Response success and error codes</span></span>

<span data-ttu-id="6f3fd-161">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6f3fd-162">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6f3fd-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6f3fd-163">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6f3fd-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6f3fd-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6f3fd-164">Response example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
