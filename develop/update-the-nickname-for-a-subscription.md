---
title: Aktualizowanie nicku dla subskrypcji
description: Aktualizuje przyjazną nazwę lub pseudonim dla subskrypcji klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 57a9fec4b69d4a64128425ea58b4bb84d0d7dd54
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768305"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="c1ae8-103">Aktualizowanie nicku dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c1ae8-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="c1ae8-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-104">**Applies To**</span></span>

- <span data-ttu-id="c1ae8-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c1ae8-105">Partner Center</span></span>
- <span data-ttu-id="c1ae8-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c1ae8-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c1ae8-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="c1ae8-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c1ae8-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c1ae8-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c1ae8-109">Aktualizuje przyjazną nazwę lub pseudonim dla [subskrypcji](subscription-resources.md)klienta.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-109">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="c1ae8-110">Ta nazwa jest wyświetlana w centrum partnerskim, aby ułatwić odróżnienie subskrypcji na koncie klienta.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-110">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="c1ae8-111">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="c1ae8-112">Następnie wybierz subskrypcję, której nazwę chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="c1ae8-113">Aby zakończyć, Zmień nazwę w polu **pseudonim subskrypcji** , a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-113">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1ae8-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c1ae8-114">Prerequisites</span></span>

- <span data-ttu-id="c1ae8-115">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c1ae8-116">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c1ae8-117">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c1ae8-118">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c1ae8-119">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c1ae8-120">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c1ae8-121">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="c1ae8-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c1ae8-122">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c1ae8-123">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="c1ae8-124">C\#</span><span class="sxs-lookup"><span data-stu-id="c1ae8-124">C\#</span></span>

<span data-ttu-id="c1ae8-125">Aby zaktualizować pseudonim subskrypcji klienta, najpierw [Uzyskaj subskrypcję](get-a-subscription-by-id.md), a następnie zmień właściwość [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-125">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="c1ae8-126">Po wprowadzeniu zmiany Użyj kolekcji [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="c1ae8-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="c1ae8-127">Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="c1ae8-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="c1ae8-128">Następnie Zakończ, wywołując metodę [**patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .</span><span class="sxs-lookup"><span data-stu-id="c1ae8-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="c1ae8-129">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c1ae8-130">**Project**: PartnerSDK. FeatureSamples **Klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="c1ae8-130">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c1ae8-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c1ae8-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c1ae8-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c1ae8-132">Request syntax</span></span>

| <span data-ttu-id="c1ae8-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="c1ae8-133">Method</span></span>    | <span data-ttu-id="c1ae8-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c1ae8-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c1ae8-135">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-135">**PATCH**</span></span> | <span data-ttu-id="c1ae8-136">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c1ae8-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c1ae8-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c1ae8-137">URI parameter</span></span>

<span data-ttu-id="c1ae8-138">W tej tabeli przedstawiono parametr zapytania wymaganego do zaktualizowania pseudonimu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-138">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="c1ae8-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c1ae8-139">Name</span></span>                    | <span data-ttu-id="c1ae8-140">Typ</span><span class="sxs-lookup"><span data-stu-id="c1ae8-140">Type</span></span>     | <span data-ttu-id="c1ae8-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c1ae8-141">Required</span></span> | <span data-ttu-id="c1ae8-142">Opis</span><span class="sxs-lookup"><span data-stu-id="c1ae8-142">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="c1ae8-143">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="c1ae8-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-144">**guid**</span></span> | <span data-ttu-id="c1ae8-145">Y</span><span class="sxs-lookup"><span data-stu-id="c1ae8-145">Y</span></span>        | <span data-ttu-id="c1ae8-146">**Identyfikator dzierżawy klienta** (identyfikator GUID).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-146">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="c1ae8-147">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-147">**id-for-subscription**</span></span> | <span data-ttu-id="c1ae8-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="c1ae8-148">**guid**</span></span> | <span data-ttu-id="c1ae8-149">Y</span><span class="sxs-lookup"><span data-stu-id="c1ae8-149">Y</span></span>        | <span data-ttu-id="c1ae8-150">Identyfikator subskrypcji (GUID).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-150">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="c1ae8-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c1ae8-151">Request headers</span></span>

<span data-ttu-id="c1ae8-152">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c1ae8-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c1ae8-153">Request body</span></span>

<span data-ttu-id="c1ae8-154">W treści żądania jest wymagany pełny zasób **subskrypcji** .</span><span class="sxs-lookup"><span data-stu-id="c1ae8-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="c1ae8-155">Upewnij się, że właściwość **FriendlyName** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-155">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="c1ae8-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c1ae8-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
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
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="c1ae8-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c1ae8-157">REST response</span></span>

<span data-ttu-id="c1ae8-158">Jeśli to się powiedzie, ta metoda zwraca zaktualizowane właściwości zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c1ae8-159">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c1ae8-159">Response success and error codes</span></span>

<span data-ttu-id="c1ae8-160">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c1ae8-161">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c1ae8-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c1ae8-162">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c1ae8-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c1ae8-163">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c1ae8-163">Response example</span></span>

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
    "Id": "<subscriptionID>",
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
