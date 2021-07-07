---
title: Ponowne uaktywnianie zawieszonej subskrypcji
description: Aktywuje ponownie subskrypcję, która została wcześniej wstrzymana z powodu niepłacenia. Na Partner Center nawigacyjnym tę operację można wykonać, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b6e3574119f9c645cc3f730047d2a23484ad8a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547718"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="01097-104">Ponowne uaktywnianie zawieszonej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="01097-104">Reactivate a suspended subscription</span></span>

<span data-ttu-id="01097-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="01097-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="01097-106">Aktywuje ponownie [subskrypcję,](subscription-resources.md) która została wcześniej wstrzymana z powodu niepłacenia.</span><span class="sxs-lookup"><span data-stu-id="01097-106">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="01097-107">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="01097-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="01097-108">Następnie wybierz subskrypcję, którą chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="01097-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="01097-109">Aby zakończyć, wybierz przycisk **Aktywne,** a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="01097-109">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01097-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="01097-110">Prerequisites</span></span>

- <span data-ttu-id="01097-111">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="01097-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="01097-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01097-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="01097-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01097-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="01097-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="01097-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="01097-115">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="01097-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="01097-116">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="01097-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="01097-117">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="01097-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="01097-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01097-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="01097-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01097-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="01097-120">C\#</span><span class="sxs-lookup"><span data-stu-id="01097-120">C\#</span></span>

<span data-ttu-id="01097-121">Aby ponownie uaktywnić subskrypcję klienta, najpierw pobierz [subskrypcję,](get-a-subscription-by-id.md)a następnie zmień właściwość [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01097-121">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="01097-122">Aby uzyskać informacje **na temat kodów** stanu, zapoznaj się z tematem [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="01097-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="01097-123">Po wejściu zmiany użyj [**kolekcji IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="01097-123">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="01097-124">Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="01097-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="01097-125">Następnie zakończ, wywołując [**metodę Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="01097-125">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

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

<span data-ttu-id="01097-126">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="01097-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="01097-127">**Project:** FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="01097-127">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="01097-128">**Klasa**: UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="01097-128">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="01097-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="01097-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="01097-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="01097-130">Request syntax</span></span>

| <span data-ttu-id="01097-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="01097-131">Method</span></span>    | <span data-ttu-id="01097-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="01097-132">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="01097-133">**Patch**</span><span class="sxs-lookup"><span data-stu-id="01097-133">**PATCH**</span></span> | <span data-ttu-id="01097-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="01097-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="01097-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="01097-135">URI parameter</span></span>

<span data-ttu-id="01097-136">W tej tabeli wymieniono parametr zapytania wymagany do ponownego aktywowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01097-136">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="01097-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="01097-137">Name</span></span>                    | <span data-ttu-id="01097-138">Typ</span><span class="sxs-lookup"><span data-stu-id="01097-138">Type</span></span>     | <span data-ttu-id="01097-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="01097-139">Required</span></span> | <span data-ttu-id="01097-140">Opis</span><span class="sxs-lookup"><span data-stu-id="01097-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="01097-141">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="01097-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="01097-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="01097-142">**guid**</span></span> | <span data-ttu-id="01097-143">Y</span><span class="sxs-lookup"><span data-stu-id="01097-143">Y</span></span>        | <span data-ttu-id="01097-144">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="01097-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="01097-145">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="01097-145">**id-for-subscription**</span></span> | <span data-ttu-id="01097-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="01097-146">**guid**</span></span> | <span data-ttu-id="01097-147">Y</span><span class="sxs-lookup"><span data-stu-id="01097-147">Y</span></span>        | <span data-ttu-id="01097-148">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01097-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="01097-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="01097-149">Request headers</span></span>

<span data-ttu-id="01097-150">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="01097-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="01097-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="01097-151">Request body</span></span>

<span data-ttu-id="01097-152">W treści **żądania** jest wymagany pełny zasób subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01097-152">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="01097-153">Upewnij się, **że właściwość Status** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="01097-153">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="01097-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="01097-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="01097-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="01097-155">REST response</span></span>

<span data-ttu-id="01097-156">W przypadku powodzenia ta metoda zwraca [zaktualizowane](subscription-resources.md) właściwości zasobu subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="01097-156">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="01097-157">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="01097-157">Response success and error codes</span></span>

<span data-ttu-id="01097-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="01097-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="01097-159">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="01097-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="01097-160">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="01097-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="01097-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="01097-161">Response example</span></span>

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
