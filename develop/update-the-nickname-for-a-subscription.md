---
title: Aktualizowanie nicku dla subskrypcji
description: Aktualizuje przyjazną nazwę lub pseudonim subskrypcji klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 195a85fcf29b3e4c9fe0e578d4d8cb80ca068c40
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530008"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="93562-103">Aktualizowanie nicku dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="93562-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="93562-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="93562-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="93562-105">Aktualizuje przyjazną nazwę lub pseudonim subskrypcji [klienta.](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="93562-105">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="93562-106">Ta nazwa jest wyświetlana Partner Center, aby ułatwić odróżnienie subskrypcji na koncie klienta.</span><span class="sxs-lookup"><span data-stu-id="93562-106">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="93562-107">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="93562-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="93562-108">Następnie wybierz subskrypcję, którą chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="93562-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="93562-109">Aby zakończyć, zmień nazwę w polu **Pseudonim subskrypcji,** a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="93562-109">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93562-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="93562-110">Prerequisites</span></span>

- <span data-ttu-id="93562-111">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="93562-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="93562-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="93562-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="93562-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="93562-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="93562-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="93562-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="93562-115">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="93562-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="93562-116">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="93562-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="93562-117">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="93562-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="93562-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="93562-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="93562-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="93562-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="93562-120">C\#</span><span class="sxs-lookup"><span data-stu-id="93562-120">C\#</span></span>

<span data-ttu-id="93562-121">Aby zaktualizować pseudonim subskrypcji klienta, [](get-a-subscription-by-id.md)najpierw pobierz subskrypcję, a następnie zmień właściwość [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="93562-121">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="93562-122">Po wejściu zmiany użyj [**kolekcji IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="93562-122">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="93562-123">Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="93562-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="93562-124">Następnie zakończ, wywołując [**metodę Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="93562-124">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="93562-125">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="93562-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="93562-126">**Project:** PartnerSDK.FeatureSamples, **klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="93562-126">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="93562-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="93562-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="93562-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="93562-128">Request syntax</span></span>

| <span data-ttu-id="93562-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="93562-129">Method</span></span>    | <span data-ttu-id="93562-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="93562-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="93562-131">**Patch**</span><span class="sxs-lookup"><span data-stu-id="93562-131">**PATCH**</span></span> | <span data-ttu-id="93562-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="93562-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="93562-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="93562-133">URI parameter</span></span>

<span data-ttu-id="93562-134">W tej tabeli wymieniono parametr zapytania wymagany do zaktualizowania pseudonimu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="93562-134">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="93562-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="93562-135">Name</span></span>                    | <span data-ttu-id="93562-136">Typ</span><span class="sxs-lookup"><span data-stu-id="93562-136">Type</span></span>     | <span data-ttu-id="93562-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="93562-137">Required</span></span> | <span data-ttu-id="93562-138">Opis</span><span class="sxs-lookup"><span data-stu-id="93562-138">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="93562-139">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="93562-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="93562-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="93562-140">**guid**</span></span> | <span data-ttu-id="93562-141">Y</span><span class="sxs-lookup"><span data-stu-id="93562-141">Y</span></span>        | <span data-ttu-id="93562-142">Identyfikator **dzierżawy klienta** (identyfikator GUID).</span><span class="sxs-lookup"><span data-stu-id="93562-142">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="93562-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="93562-143">**id-for-subscription**</span></span> | <span data-ttu-id="93562-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="93562-144">**guid**</span></span> | <span data-ttu-id="93562-145">Y</span><span class="sxs-lookup"><span data-stu-id="93562-145">Y</span></span>        | <span data-ttu-id="93562-146">Identyfikator subskrypcji (identyfikator GUID).</span><span class="sxs-lookup"><span data-stu-id="93562-146">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="93562-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="93562-147">Request headers</span></span>

<span data-ttu-id="93562-148">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="93562-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="93562-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="93562-149">Request body</span></span>

<span data-ttu-id="93562-150">W treści **żądania** jest wymagany pełny zasób subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="93562-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="93562-151">Upewnij **się, że** właściwość FriendlyName została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="93562-151">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="93562-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="93562-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="93562-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="93562-153">REST response</span></span>

<span data-ttu-id="93562-154">W przypadku powodzenia ta metoda zwraca [zaktualizowane](subscription-resources.md) właściwości zasobu subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="93562-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="93562-155">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="93562-155">Response success and error codes</span></span>

<span data-ttu-id="93562-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="93562-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="93562-157">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="93562-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="93562-158">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="93562-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="93562-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="93562-159">Response example</span></span>

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
