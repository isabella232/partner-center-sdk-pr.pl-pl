---
title: Zmiana ilości subskrypcji
description: Dowiedz się, jak zmienić liczbę licencji dla subskrypcji klienta przy użyciu interfejsów API usługi Partner Center. Można to również zrobić na pulpicie nawigacyjnym Centrum partnerskiego.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768589"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="cf22a-104">Zmień liczbę licencji w ramach subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="cf22a-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="cf22a-105">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="cf22a-105">**Applies to:**</span></span>

- <span data-ttu-id="cf22a-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="cf22a-106">Partner Center</span></span>
- <span data-ttu-id="cf22a-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cf22a-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cf22a-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="cf22a-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cf22a-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cf22a-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cf22a-110">Aktualizuje [subskrypcję](subscription-resources.md) , aby zwiększyć lub zmniejszyć liczbę licencji.</span><span class="sxs-lookup"><span data-stu-id="cf22a-110">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="cf22a-111">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="cf22a-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="cf22a-112">Następnie wybierz subskrypcję, której nazwę chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="cf22a-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="cf22a-113">Aby zakończyć, Zmień wartość w polu **ilość** , a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="cf22a-113">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf22a-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf22a-114">Prerequisites</span></span>

- <span data-ttu-id="cf22a-115">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cf22a-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cf22a-116">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cf22a-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cf22a-117">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cf22a-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cf22a-118">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="cf22a-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cf22a-119">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="cf22a-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cf22a-120">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="cf22a-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cf22a-121">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="cf22a-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cf22a-122">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cf22a-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cf22a-123">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cf22a-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="cf22a-124">C\#</span><span class="sxs-lookup"><span data-stu-id="cf22a-124">C\#</span></span>

<span data-ttu-id="cf22a-125">Aby zmienić liczbę subskrypcji klienta, najpierw [Uzyskaj subskrypcję](get-a-subscription-by-id.md), a następnie [**Zmień właściwość wartość**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cf22a-125">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="cf22a-126">Po wprowadzeniu zmiany Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="cf22a-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="cf22a-127">Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="cf22a-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="cf22a-128">Następnie Zakończ, wywołując metodę **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="cf22a-128">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="cf22a-129">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cf22a-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cf22a-130">**Project**: PartnerSDK. FeatureSample **Klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="cf22a-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cf22a-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cf22a-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cf22a-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cf22a-132">Request syntax</span></span>

| <span data-ttu-id="cf22a-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="cf22a-133">Method</span></span>    | <span data-ttu-id="cf22a-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cf22a-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf22a-135">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="cf22a-135">**PATCH**</span></span> | <span data-ttu-id="cf22a-136">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cf22a-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cf22a-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cf22a-137">URI parameter</span></span>

<span data-ttu-id="cf22a-138">Ta tabela zawiera listę wymaganych parametrów zapytania, aby zmienić liczbę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cf22a-138">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="cf22a-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf22a-139">Name</span></span>                    | <span data-ttu-id="cf22a-140">Typ</span><span class="sxs-lookup"><span data-stu-id="cf22a-140">Type</span></span>     | <span data-ttu-id="cf22a-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cf22a-141">Required</span></span> | <span data-ttu-id="cf22a-142">Opis</span><span class="sxs-lookup"><span data-stu-id="cf22a-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="cf22a-143">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="cf22a-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="cf22a-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="cf22a-144">**guid**</span></span> | <span data-ttu-id="cf22a-145">Y</span><span class="sxs-lookup"><span data-stu-id="cf22a-145">Y</span></span>        | <span data-ttu-id="cf22a-146">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="cf22a-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="cf22a-147">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="cf22a-147">**id-for-subscription**</span></span> | <span data-ttu-id="cf22a-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="cf22a-148">**guid**</span></span> | <span data-ttu-id="cf22a-149">Y</span><span class="sxs-lookup"><span data-stu-id="cf22a-149">Y</span></span>        | <span data-ttu-id="cf22a-150">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cf22a-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cf22a-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cf22a-151">Request headers</span></span>

<span data-ttu-id="cf22a-152">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cf22a-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cf22a-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cf22a-153">Request body</span></span>

<span data-ttu-id="cf22a-154">W treści żądania jest wymagany pełny zasób **subskrypcji** .</span><span class="sxs-lookup"><span data-stu-id="cf22a-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="cf22a-155">Upewnij się, że właściwość **ilość** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="cf22a-155">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="cf22a-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cf22a-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cf22a-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cf22a-157">REST response</span></span>

<span data-ttu-id="cf22a-158">Jeśli to się powiedzie, ta metoda zwraca kod stanu **HTTP 200** i zaktualizowane właściwości [zasobów subskrypcji](subscription-resources.md)  w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="cf22a-158">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cf22a-159">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf22a-159">Response success and error codes</span></span>

<span data-ttu-id="cf22a-160">Każda odpowiedź zwraca kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="cf22a-160">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cf22a-161">Użyj narzędzia do śledzenia sieci, aby odczytać kod stanu, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cf22a-161">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="cf22a-162">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cf22a-162">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="cf22a-163">Gdy operacja patch trwa dłużej niż oczekiwany czas, centrum partnerskie wyśle kod stanu **http o stanie 202** i nagłówek lokalizacji wskazujący, gdzie pobrać subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="cf22a-163">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="cf22a-164">W celu monitorowania zmian stanu i ilości można wykonać zapytanie o subskrypcję okresowo.</span><span class="sxs-lookup"><span data-stu-id="cf22a-164">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="cf22a-165">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf22a-165">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="cf22a-166">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="cf22a-166">Response example 1</span></span>

<span data-ttu-id="cf22a-167">Pomyślne żądanie ze **stanem HTTP 200** kod stanu:</span><span class="sxs-lookup"><span data-stu-id="cf22a-167">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="cf22a-168">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="cf22a-168">Response example 2</span></span>

<span data-ttu-id="cf22a-169">Pomyślne żądanie ze **stanem HTTP 202** kod stanu:</span><span class="sxs-lookup"><span data-stu-id="cf22a-169">Successful request with an **HTTP status 202** status code:</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
