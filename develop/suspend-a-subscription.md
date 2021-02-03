---
title: Zawieszenie subskrypcji
description: Wstrzymuje zasób subskrypcji, który jest zgodny z IDENTYFIKATORem klienta i subskrypcji z powodu oszustwa lub niepłaty. Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f351c87efe2bdc810a66c64a9d01b7d376f8a6e3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768273"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="b2d1c-103">Zawieszenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b2d1c-103">Suspend a subscription</span></span>

<span data-ttu-id="b2d1c-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-104">**Applies To**</span></span>

- <span data-ttu-id="b2d1c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b2d1c-105">Partner Center</span></span>
- <span data-ttu-id="b2d1c-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b2d1c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b2d1c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="b2d1c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b2d1c-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b2d1c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b2d1c-109">Wstrzymuje zasób [subskrypcji](subscription-resources.md) , który jest zgodny z identyfikatorem klienta i subskrypcji z powodu oszustwa lub niepłaty.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-109">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="b2d1c-110">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="b2d1c-111">Następnie wybierz subskrypcję, której nazwę chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="b2d1c-112">Aby zakończyć, wybierz przycisk **zawieszone** , a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-112">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2d1c-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2d1c-113">Prerequisites</span></span>

- <span data-ttu-id="b2d1c-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b2d1c-115">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b2d1c-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b2d1c-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b2d1c-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b2d1c-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b2d1c-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="b2d1c-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b2d1c-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b2d1c-122">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="b2d1c-123">C\#</span><span class="sxs-lookup"><span data-stu-id="b2d1c-123">C\#</span></span>

<span data-ttu-id="b2d1c-124">Aby wstrzymać subskrypcję klienta, najpierw [Uzyskaj subskrypcję](get-a-subscription-by-id.md), a następnie zmień wartość właściwości [**stan**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-124">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="b2d1c-125">Aby uzyskać informacje na temat kodów **stanu** , zapoznaj się z tematem [SubscriptionStatus Enumeration/dotnet/API/Microsoft. Store. partnercenter. models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="b2d1c-126">Po wprowadzeniu zmiany Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b2d1c-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="b2d1c-127">Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="b2d1c-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="b2d1c-128">Następnie Zakończ, wywołując metodę **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="b2d1c-128">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Suspended
   });
```

<span data-ttu-id="b2d1c-129">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b2d1c-130">**Project**: PartnerSDK. FeatureSample **Klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="b2d1c-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b2d1c-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b2d1c-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b2d1c-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b2d1c-132">Request syntax</span></span>

| <span data-ttu-id="b2d1c-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="b2d1c-133">Method</span></span>    | <span data-ttu-id="b2d1c-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b2d1c-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b2d1c-135">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-135">**PATCH**</span></span> | <span data-ttu-id="b2d1c-136">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b2d1c-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b2d1c-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b2d1c-137">URI parameter</span></span>

<span data-ttu-id="b2d1c-138">Ta tabela zawiera listę wymaganych parametrów zapytania, aby wstrzymać subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="b2d1c-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b2d1c-139">Name</span></span>                    | <span data-ttu-id="b2d1c-140">Typ</span><span class="sxs-lookup"><span data-stu-id="b2d1c-140">Type</span></span>     | <span data-ttu-id="b2d1c-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b2d1c-141">Required</span></span> | <span data-ttu-id="b2d1c-142">Opis</span><span class="sxs-lookup"><span data-stu-id="b2d1c-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="b2d1c-143">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="b2d1c-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-144">**guid**</span></span> | <span data-ttu-id="b2d1c-145">Y</span><span class="sxs-lookup"><span data-stu-id="b2d1c-145">Y</span></span>        | <span data-ttu-id="b2d1c-146">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="b2d1c-147">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-147">**id-for-subscription**</span></span> | <span data-ttu-id="b2d1c-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="b2d1c-148">**guid**</span></span> | <span data-ttu-id="b2d1c-149">Y</span><span class="sxs-lookup"><span data-stu-id="b2d1c-149">Y</span></span>        | <span data-ttu-id="b2d1c-150">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b2d1c-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b2d1c-151">Request headers</span></span>

<span data-ttu-id="b2d1c-152">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b2d1c-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b2d1c-153">Request body</span></span>

<span data-ttu-id="b2d1c-154">W treści żądania jest wymagany pełny zasób **subskrypcji** .</span><span class="sxs-lookup"><span data-stu-id="b2d1c-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="b2d1c-155">Upewnij się, że właściwość **status** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="b2d1c-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b2d1c-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
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
    "Status": "suspended",
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

## <a name="rest-response"></a><span data-ttu-id="b2d1c-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b2d1c-157">REST response</span></span>

<span data-ttu-id="b2d1c-158">Jeśli to się powiedzie, ta metoda zwraca zaktualizowane właściwości zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b2d1c-159">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b2d1c-159">Response success and error codes</span></span>

<span data-ttu-id="b2d1c-160">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b2d1c-161">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b2d1c-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b2d1c-162">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b2d1c-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b2d1c-163">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b2d1c-163">Response example</span></span>

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
    "Status": "suspended",
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
