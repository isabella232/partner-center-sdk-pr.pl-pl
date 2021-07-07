---
title: Pobieranie subskrypcji klienta według identyfikatora MPN partnera
description: Jak uzyskać listę subskrypcji dostarczonych przez danego partnera do określonego klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 857caa667245503f111b27379a5c8f93aa1fb0b0
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760661"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="8fcfd-103">Pobieranie subskrypcji klienta według identyfikatora MPN partnera</span><span class="sxs-lookup"><span data-stu-id="8fcfd-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="8fcfd-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8fcfd-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8fcfd-105">Jak uzyskać listę subskrypcji dostarczonych przez danego partnera Microsoft Partner Network (MPN) do określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-105">How to get a list of subscriptions provided by a given Microsoft Partner Network (MPN) partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fcfd-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8fcfd-106">Prerequisites</span></span>

- <span data-ttu-id="8fcfd-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8fcfd-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8fcfd-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8fcfd-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8fcfd-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8fcfd-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="8fcfd-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8fcfd-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="8fcfd-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8fcfd-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8fcfd-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8fcfd-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8fcfd-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8fcfd-115">Identyfikator MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-115">A partner MPN identifier.</span></span>

## <a name="c"></a><span data-ttu-id="8fcfd-116">C\#</span><span class="sxs-lookup"><span data-stu-id="8fcfd-116">C\#</span></span>

<span data-ttu-id="8fcfd-117">Aby uzyskać listę subskrypcji dostarczonych przez danego partnera dla określonego klienta, najpierw użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-117">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="8fcfd-118">Następnie pobierz interfejs do operacji zbierania subskrypcji klienta z właściwości [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) i wywołaj metodę [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) z identyfikatorem MPN, aby zidentyfikować partnera i pobrać interfejs do operacji subskrypcji partnera.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-118">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="8fcfd-119">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) aby pobrać kolekcję.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="8fcfd-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8fcfd-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8fcfd-121">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="8fcfd-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="8fcfd-122">Java</span><span class="sxs-lookup"><span data-stu-id="8fcfd-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="8fcfd-123">Aby uzyskać listę subskrypcji dostarczonych przez danego partnera określonemu klientowi, najpierw użyj funkcji **IAggregatePartner.getCustomers.byId** z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-123">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="8fcfd-124">Następnie pobierz interfejs do operacji zbierania subskrypcji klienta z funkcji **getSubscriptions** i wywołaj funkcję **byPartner** z identyfikatorem MPN, aby zidentyfikować partnera i pobrać interfejs do operacji subskrypcji partnera.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-124">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="8fcfd-125">Na koniec wywołaj **funkcję get,** aby pobrać kolekcję.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-125">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="8fcfd-126">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fcfd-126">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="8fcfd-127">Aby uzyskać listę subskrypcji dostarczonych przez danego partnera określonemu klientowi, wykonaj polecenie [**Get-PartnerCustomerSubscription.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md)</span><span class="sxs-lookup"><span data-stu-id="8fcfd-127">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="8fcfd-128">Określ identyfikator klienta, aby zidentyfikować klienta przy użyciu parametru **CustomerId,** a następnie wypełnij parametr **MpnId** identyfikatorem MPN, aby zidentyfikować partnera.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-128">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="8fcfd-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8fcfd-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8fcfd-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8fcfd-130">Request syntax</span></span>

| <span data-ttu-id="8fcfd-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="8fcfd-131">Method</span></span>  | <span data-ttu-id="8fcfd-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8fcfd-132">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8fcfd-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="8fcfd-133">**GET**</span></span> | <span data-ttu-id="8fcfd-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscriptions?mpn \_ id={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8fcfd-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="8fcfd-135">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="8fcfd-135">URI parameters</span></span>

<span data-ttu-id="8fcfd-136">Użyj następującej ścieżki i parametrów zapytania, aby zidentyfikować klienta i partnera.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-136">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="8fcfd-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8fcfd-137">Name</span></span>        | <span data-ttu-id="8fcfd-138">Typ</span><span class="sxs-lookup"><span data-stu-id="8fcfd-138">Type</span></span>   | <span data-ttu-id="8fcfd-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8fcfd-139">Required</span></span> | <span data-ttu-id="8fcfd-140">Opis</span><span class="sxs-lookup"><span data-stu-id="8fcfd-140">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="8fcfd-141">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="8fcfd-141">customer-id</span></span> | <span data-ttu-id="8fcfd-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="8fcfd-142">string</span></span> | <span data-ttu-id="8fcfd-143">Tak</span><span class="sxs-lookup"><span data-stu-id="8fcfd-143">Yes</span></span>      | <span data-ttu-id="8fcfd-144">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-144">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="8fcfd-145">identyfikator mpn</span><span class="sxs-lookup"><span data-stu-id="8fcfd-145">mpn-id</span></span>      | <span data-ttu-id="8fcfd-146">int</span><span class="sxs-lookup"><span data-stu-id="8fcfd-146">int</span></span>    | <span data-ttu-id="8fcfd-147">Tak</span><span class="sxs-lookup"><span data-stu-id="8fcfd-147">Yes</span></span>      | <span data-ttu-id="8fcfd-148">Identyfikator Microsoft Partner Network, który identyfikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-148">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8fcfd-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8fcfd-149">Request headers</span></span>

<span data-ttu-id="8fcfd-150">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8fcfd-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8fcfd-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8fcfd-151">Request body</span></span>

<span data-ttu-id="8fcfd-152">Brak.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8fcfd-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8fcfd-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8fcfd-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8fcfd-154">REST response</span></span>

<span data-ttu-id="8fcfd-155">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów](subscription-resources.md) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-155">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8fcfd-156">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8fcfd-156">Response success and error codes</span></span>

<span data-ttu-id="8fcfd-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8fcfd-158">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8fcfd-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8fcfd-159">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8fcfd-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8fcfd-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8fcfd-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a><span data-ttu-id="8fcfd-161">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8fcfd-161">See also</span></span>

- [<span data-ttu-id="8fcfd-162">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="8fcfd-162">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
