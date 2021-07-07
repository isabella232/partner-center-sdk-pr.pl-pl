---
title: Zmiana ilości subskrypcji
description: Dowiedz się, jak Partner Center API, aby zmienić liczbę licencji dla subskrypcji klienta. Możesz to również zrobić na pulpicie nawigacyjnym Partner Center nawigacyjnym.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d57ece4dd19ef2852f39130916222c54a9ccc85a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974101"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="f13da-104">Zmienianie liczby licencji w subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="f13da-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="f13da-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f13da-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f13da-106">Aktualizuje [subskrypcję,](subscription-resources.md) aby zwiększyć lub zmniejszyć liczbę licencji.</span><span class="sxs-lookup"><span data-stu-id="f13da-106">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="f13da-107">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="f13da-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="f13da-108">Następnie wybierz subskrypcję, którą chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="f13da-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="f13da-109">Aby zakończyć, zmień wartość w **polu Ilość,** a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="f13da-109">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f13da-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f13da-110">Prerequisites</span></span>

- <span data-ttu-id="f13da-111">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f13da-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f13da-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f13da-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f13da-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f13da-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f13da-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f13da-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f13da-115">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="f13da-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f13da-116">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="f13da-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f13da-117">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="f13da-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f13da-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f13da-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f13da-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f13da-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="f13da-120">C\#</span><span class="sxs-lookup"><span data-stu-id="f13da-120">C\#</span></span>

<span data-ttu-id="f13da-121">Aby zmienić ilość subskrypcji klienta, najpierw pobierz subskrypcję [,](get-a-subscription-by-id.md)a następnie zmień właściwość [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f13da-121">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="f13da-122">Po wgraniu zmiany użyj kolekcji **IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="f13da-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="f13da-123">Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="f13da-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="f13da-124">Następnie zakończ, wywołując **metodę Patch().**</span><span class="sxs-lookup"><span data-stu-id="f13da-124">Then, finish by calling the **Patch()** method.</span></span>

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

<span data-ttu-id="f13da-125">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f13da-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f13da-126">**Project:** PartnerSDK.FeatureSample, **klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="f13da-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f13da-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f13da-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f13da-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f13da-128">Request syntax</span></span>

| <span data-ttu-id="f13da-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="f13da-129">Method</span></span>    | <span data-ttu-id="f13da-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f13da-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f13da-131">**Patch**</span><span class="sxs-lookup"><span data-stu-id="f13da-131">**PATCH**</span></span> | <span data-ttu-id="f13da-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f13da-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f13da-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f13da-133">URI parameter</span></span>

<span data-ttu-id="f13da-134">W tej tabeli wymieniono parametr zapytania wymagany do zmiany ilości subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f13da-134">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="f13da-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f13da-135">Name</span></span>                    | <span data-ttu-id="f13da-136">Typ</span><span class="sxs-lookup"><span data-stu-id="f13da-136">Type</span></span>     | <span data-ttu-id="f13da-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f13da-137">Required</span></span> | <span data-ttu-id="f13da-138">Opis</span><span class="sxs-lookup"><span data-stu-id="f13da-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f13da-139">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="f13da-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="f13da-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="f13da-140">**guid**</span></span> | <span data-ttu-id="f13da-141">Y</span><span class="sxs-lookup"><span data-stu-id="f13da-141">Y</span></span>        | <span data-ttu-id="f13da-142">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="f13da-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f13da-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="f13da-143">**id-for-subscription**</span></span> | <span data-ttu-id="f13da-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="f13da-144">**guid**</span></span> | <span data-ttu-id="f13da-145">Y</span><span class="sxs-lookup"><span data-stu-id="f13da-145">Y</span></span>        | <span data-ttu-id="f13da-146">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f13da-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f13da-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f13da-147">Request headers</span></span>

<span data-ttu-id="f13da-148">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f13da-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f13da-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f13da-149">Request body</span></span>

<span data-ttu-id="f13da-150">W treści **żądania** jest wymagany pełny zasób subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f13da-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="f13da-151">Upewnij się, **że właściwość Quantity** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="f13da-151">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="f13da-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f13da-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f13da-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f13da-153">REST response</span></span>

<span data-ttu-id="f13da-154">W przypadku powodzenia ta metoda zwraca kod stanu **HTTP 200** i zaktualizowane właściwości zasobów [subskrypcji](subscription-resources.md)  w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f13da-154">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f13da-155">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f13da-155">Response success and error codes</span></span>

<span data-ttu-id="f13da-156">Każda odpowiedź zwraca kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="f13da-156">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f13da-157">Użyj narzędzia śledzenia sieci, aby odczytać kod stanu, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f13da-157">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="f13da-158">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f13da-158">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="f13da-159">Gdy operacja poprawki trwa dłużej niż oczekiwano, Partner Center wysyła kod stanu **http 202** i nagłówek lokalizacji, który wskazuje, gdzie pobrać subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f13da-159">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="f13da-160">Okresowo możesz wysyłać zapytania dotyczące subskrypcji, aby monitorować zmiany stanu i ilości.</span><span class="sxs-lookup"><span data-stu-id="f13da-160">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="f13da-161">Przykłady odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f13da-161">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="f13da-162">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="f13da-162">Response example 1</span></span>

<span data-ttu-id="f13da-163">Pomyślne żądanie z **kodem stanu 200** protokołu HTTP:</span><span class="sxs-lookup"><span data-stu-id="f13da-163">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="f13da-164">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="f13da-164">Response example 2</span></span>

<span data-ttu-id="f13da-165">Pomyślne żądanie z **kodem stanu http 202:**</span><span class="sxs-lookup"><span data-stu-id="f13da-165">Successful request with an **HTTP status 202** status code:</span></span>

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
