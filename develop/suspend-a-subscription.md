---
title: Zawieszenie subskrypcji
description: Wstrzymuje zasób subskrypcji, który pasuje do klienta i identyfikatora subskrypcji z powodu oszustwa lub braku płatności. Na Partner Center nawigacyjnym tę operację można wykonać, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dae7c3422a403c48a2b10424c4ae5dbdbc498ea
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547346"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="0f30f-104">Zawieszenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0f30f-104">Suspend a subscription</span></span>

<span data-ttu-id="0f30f-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0f30f-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0f30f-106">Wstrzymuje [zasób](subscription-resources.md) subskrypcji, który pasuje do klienta i identyfikatora subskrypcji z powodu oszustwa lub braku płatności.</span><span class="sxs-lookup"><span data-stu-id="0f30f-106">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="0f30f-107">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="0f30f-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="0f30f-108">Następnie wybierz subskrypcję, którą chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="0f30f-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="0f30f-109">Aby zakończyć, wybierz przycisk **Wstrzymano,** a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="0f30f-109">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f30f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f30f-110">Prerequisites</span></span>

- <span data-ttu-id="0f30f-111">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0f30f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0f30f-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f30f-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0f30f-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f30f-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0f30f-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0f30f-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0f30f-115">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="0f30f-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0f30f-116">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="0f30f-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0f30f-117">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="0f30f-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0f30f-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f30f-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0f30f-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f30f-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="0f30f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="0f30f-120">C\#</span></span>

<span data-ttu-id="0f30f-121">Aby wstrzymać subskrypcję klienta, najpierw [pobierz subskrypcję,](get-a-subscription-by-id.md)a następnie zmień właściwość [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f30f-121">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="0f30f-122">Aby uzyskać informacje **na temat kodów** stanu, zapoznaj się z tematem [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="0f30f-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="0f30f-123">Po wejściu zmiany użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="0f30f-123">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="0f30f-124">Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="0f30f-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="0f30f-125">Następnie zakończ, wywołując **metodę Patch().**</span><span class="sxs-lookup"><span data-stu-id="0f30f-125">Then, finish by calling the **Patch()** method.</span></span>

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

<span data-ttu-id="0f30f-126">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f30f-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0f30f-127">**Project:** Klasa PartnerSDK.FeatureSample: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="0f30f-127">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0f30f-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0f30f-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0f30f-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0f30f-129">Request syntax</span></span>

| <span data-ttu-id="0f30f-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="0f30f-130">Method</span></span>    | <span data-ttu-id="0f30f-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0f30f-131">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0f30f-132">**Patch**</span><span class="sxs-lookup"><span data-stu-id="0f30f-132">**PATCH**</span></span> | <span data-ttu-id="0f30f-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0f30f-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0f30f-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0f30f-134">URI parameter</span></span>

<span data-ttu-id="0f30f-135">W tej tabeli wymieniono parametr zapytania wymagany do wstrzymania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f30f-135">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="0f30f-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0f30f-136">Name</span></span>                    | <span data-ttu-id="0f30f-137">Typ</span><span class="sxs-lookup"><span data-stu-id="0f30f-137">Type</span></span>     | <span data-ttu-id="0f30f-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0f30f-138">Required</span></span> | <span data-ttu-id="0f30f-139">Opis</span><span class="sxs-lookup"><span data-stu-id="0f30f-139">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="0f30f-140">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="0f30f-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="0f30f-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="0f30f-141">**guid**</span></span> | <span data-ttu-id="0f30f-142">Y</span><span class="sxs-lookup"><span data-stu-id="0f30f-142">Y</span></span>        | <span data-ttu-id="0f30f-143">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="0f30f-143">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="0f30f-144">**identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="0f30f-144">**id-for-subscription**</span></span> | <span data-ttu-id="0f30f-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="0f30f-145">**guid**</span></span> | <span data-ttu-id="0f30f-146">Y</span><span class="sxs-lookup"><span data-stu-id="0f30f-146">Y</span></span>        | <span data-ttu-id="0f30f-147">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f30f-147">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0f30f-148">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0f30f-148">Request headers</span></span>

<span data-ttu-id="0f30f-149">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0f30f-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0f30f-150">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0f30f-150">Request body</span></span>

<span data-ttu-id="0f30f-151">W treści **żądania** wymagany jest pełny zasób Subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f30f-151">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="0f30f-152">Upewnij **się, że właściwość Status** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="0f30f-152">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="0f30f-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0f30f-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0f30f-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0f30f-154">REST response</span></span>

<span data-ttu-id="0f30f-155">W przypadku powodzenia ta metoda zwraca zaktualizowane [właściwości](subscription-resources.md) zasobów subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0f30f-155">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0f30f-156">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0f30f-156">Response success and error codes</span></span>

<span data-ttu-id="0f30f-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="0f30f-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0f30f-158">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0f30f-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0f30f-159">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0f30f-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0f30f-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0f30f-160">Response example</span></span>

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
