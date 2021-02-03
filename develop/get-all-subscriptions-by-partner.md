---
title: Pobieranie subskrypcji klienta według identyfikatora MPN partnera
description: Jak uzyskać listę subskrypcji dostarczonych przez danego partnera do określonego klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c95488b62449e1ab6bd2eeefea58d6686c291f4c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768349"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="3e757-103">Pobieranie subskrypcji klienta według identyfikatora MPN partnera</span><span class="sxs-lookup"><span data-stu-id="3e757-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="3e757-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="3e757-104">**Applies To**</span></span>

- <span data-ttu-id="3e757-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="3e757-105">Partner Center</span></span>
- <span data-ttu-id="3e757-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="3e757-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3e757-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="3e757-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3e757-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3e757-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3e757-109">Jak uzyskać listę subskrypcji dostarczonych przez danego partnera do określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="3e757-109">How to get a list of subscriptions provided by a given partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e757-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e757-110">Prerequisites</span></span>

- <span data-ttu-id="3e757-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3e757-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3e757-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e757-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3e757-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3e757-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3e757-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="3e757-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3e757-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="3e757-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3e757-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="3e757-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3e757-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="3e757-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3e757-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3e757-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3e757-119">Identyfikator Microsoft Partner Network partnera (MPN).</span><span class="sxs-lookup"><span data-stu-id="3e757-119">A partner Microsoft Partner Network (MPN) identifier.</span></span>

## <a name="c"></a><span data-ttu-id="3e757-120">C\#</span><span class="sxs-lookup"><span data-stu-id="3e757-120">C\#</span></span>

<span data-ttu-id="3e757-121">Aby uzyskać listę subskrypcji dostarczonych przez danego partnera do określonego klienta, najpierw Użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="3e757-121">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="3e757-122">Następnie uzyskaj interfejs do operacji zbierania danych subskrypcji klienta z właściwości [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) i Wywołaj metodę [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) z identyfikatorem MPN, aby zidentyfikować partnera i pobrać interfejs do operacji subskrypcji partnerskich.</span><span class="sxs-lookup"><span data-stu-id="3e757-122">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="3e757-123">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) w celu pobrania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="3e757-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="3e757-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3e757-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3e757-125">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="3e757-125">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="3e757-126">Java</span><span class="sxs-lookup"><span data-stu-id="3e757-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="3e757-127">Aby uzyskać listę subskrypcji dostarczonych przez danego partnera do określonego klienta, najpierw Użyj funkcji **IAggregatePartner. GetCustomers. byId** z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="3e757-127">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="3e757-128">Następnie uzyskaj interfejs do operacji zbierania subskrypcji klienta z funkcji **Getsubscriptions** i wywołaj funkcję **byPartner** z identyfikatorem MPN, aby zidentyfikować partnera i pobrać interfejs do operacji subskrypcji partnerskich.</span><span class="sxs-lookup"><span data-stu-id="3e757-128">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="3e757-129">Na koniec wywołaj funkcję **Get** w celu pobrania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="3e757-129">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="3e757-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e757-130">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3e757-131">Aby uzyskać listę subskrypcji dostarczonych przez danego partnera do określonego klienta, uruchom polecenie [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) .</span><span class="sxs-lookup"><span data-stu-id="3e757-131">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="3e757-132">Określ identyfikator klienta, który będzie identyfikować klienta przy użyciu parametru **CustomerID** , i wypełnij parametr **MPNID** identyfikatorem MPN, aby zidentyfikować partnera.</span><span class="sxs-lookup"><span data-stu-id="3e757-132">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="3e757-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3e757-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3e757-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3e757-134">Request syntax</span></span>

| <span data-ttu-id="3e757-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="3e757-135">Method</span></span>  | <span data-ttu-id="3e757-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3e757-136">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3e757-137">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3e757-137">**GET**</span></span> | <span data-ttu-id="3e757-138">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions? MPN \_ ID = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3e757-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3e757-139">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="3e757-139">URI parameters</span></span>

<span data-ttu-id="3e757-140">Użyj następującej ścieżki i parametrów zapytania, aby zidentyfikować klienta i partnera.</span><span class="sxs-lookup"><span data-stu-id="3e757-140">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="3e757-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3e757-141">Name</span></span>        | <span data-ttu-id="3e757-142">Typ</span><span class="sxs-lookup"><span data-stu-id="3e757-142">Type</span></span>   | <span data-ttu-id="3e757-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3e757-143">Required</span></span> | <span data-ttu-id="3e757-144">Opis</span><span class="sxs-lookup"><span data-stu-id="3e757-144">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="3e757-145">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="3e757-145">customer-id</span></span> | <span data-ttu-id="3e757-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="3e757-146">string</span></span> | <span data-ttu-id="3e757-147">Tak</span><span class="sxs-lookup"><span data-stu-id="3e757-147">Yes</span></span>      | <span data-ttu-id="3e757-148">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="3e757-148">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="3e757-149">MPN — identyfikator</span><span class="sxs-lookup"><span data-stu-id="3e757-149">mpn-id</span></span>      | <span data-ttu-id="3e757-150">int</span><span class="sxs-lookup"><span data-stu-id="3e757-150">int</span></span>    | <span data-ttu-id="3e757-151">Tak</span><span class="sxs-lookup"><span data-stu-id="3e757-151">Yes</span></span>      | <span data-ttu-id="3e757-152">Identyfikator Microsoft Partner Network, który identyfikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="3e757-152">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3e757-153">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3e757-153">Request headers</span></span>

<span data-ttu-id="3e757-154">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3e757-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3e757-155">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3e757-155">Request body</span></span>

<span data-ttu-id="3e757-156">Brak.</span><span class="sxs-lookup"><span data-stu-id="3e757-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3e757-157">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3e757-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="3e757-158">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3e757-158">REST response</span></span>

<span data-ttu-id="3e757-159">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [subskrypcji](subscription-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="3e757-159">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3e757-160">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3e757-160">Response success and error codes</span></span>

<span data-ttu-id="3e757-161">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="3e757-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3e757-162">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3e757-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3e757-163">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3e757-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3e757-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3e757-164">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="3e757-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3e757-165">See also</span></span>

- [<span data-ttu-id="3e757-166">Analiza Centrum partnerskiego — zasoby</span><span class="sxs-lookup"><span data-stu-id="3e757-166">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
