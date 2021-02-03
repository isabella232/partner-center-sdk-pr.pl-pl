---
title: Pobieranie elementów wiersza kosztów usług klienta
description: Pobiera pozycje kosztu usługi klienta dla określonego okresu rozliczeniowego.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2034eaf11342493797688b44b634b8e9598e2e4
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768118"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="a916f-103">Pobieranie elementów wiersza kosztów usług klienta</span><span class="sxs-lookup"><span data-stu-id="a916f-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="a916f-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="a916f-104">**Applies to:**</span></span>

- <span data-ttu-id="a916f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="a916f-105">Partner Center</span></span>

<span data-ttu-id="a916f-106">Pobiera pozycje kosztu usługi klienta dla określonego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="a916f-106">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a916f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a916f-107">Prerequisites</span></span>

- <span data-ttu-id="a916f-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a916f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a916f-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a916f-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="a916f-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a916f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a916f-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="a916f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a916f-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="a916f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a916f-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="a916f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a916f-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="a916f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a916f-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a916f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a916f-116">Wskaźnik okresu rozliczeniowego ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="a916f-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="a916f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="a916f-117">C\#</span></span>

<span data-ttu-id="a916f-118">Aby pobrać podsumowanie kosztów usługi dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="a916f-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="a916f-119">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="a916f-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="a916f-120">Użyj właściwości [**Servicecosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) , aby uzyskać interfejs do obsługi kosztów usługi klienta.</span><span class="sxs-lookup"><span data-stu-id="a916f-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="a916f-121">Wywołaj metodę [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) z elementem członkowskim wyliczenia [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) , aby zwracał [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="a916f-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="a916f-122">Użyj metody [**IServiceCostsCollection. LineItems. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) , aby pobrać pozycje kosztów usługi klienta.</span><span class="sxs-lookup"><span data-stu-id="a916f-122">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="a916f-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a916f-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a916f-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a916f-124">Request syntax</span></span>

| <span data-ttu-id="a916f-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="a916f-125">Method</span></span>  | <span data-ttu-id="a916f-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a916f-126">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a916f-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a916f-127">**GET**</span></span> | <span data-ttu-id="a916f-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/servicecosts/{Billing-period}/LineItems http/1.1</span><span class="sxs-lookup"><span data-stu-id="a916f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a916f-129">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="a916f-129">URI parameters</span></span>

<span data-ttu-id="a916f-130">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="a916f-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="a916f-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a916f-131">Name</span></span>           | <span data-ttu-id="a916f-132">Typ</span><span class="sxs-lookup"><span data-stu-id="a916f-132">Type</span></span>   | <span data-ttu-id="a916f-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a916f-133">Required</span></span> | <span data-ttu-id="a916f-134">Opis</span><span class="sxs-lookup"><span data-stu-id="a916f-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a916f-135">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="a916f-135">customer-id</span></span>    | <span data-ttu-id="a916f-136">guid</span><span class="sxs-lookup"><span data-stu-id="a916f-136">guid</span></span>   | <span data-ttu-id="a916f-137">Tak</span><span class="sxs-lookup"><span data-stu-id="a916f-137">Yes</span></span>      | <span data-ttu-id="a916f-138">Identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="a916f-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="a916f-139">rozliczenia — okres</span><span class="sxs-lookup"><span data-stu-id="a916f-139">billing-period</span></span> | <span data-ttu-id="a916f-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="a916f-140">string</span></span> | <span data-ttu-id="a916f-141">Tak</span><span class="sxs-lookup"><span data-stu-id="a916f-141">Yes</span></span>      | <span data-ttu-id="a916f-142">Wskaźnik reprezentujący okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="a916f-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="a916f-143">Jedyną obsługiwaną wartością jest MostRecent.</span><span class="sxs-lookup"><span data-stu-id="a916f-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="a916f-144">Przypadek ciągu nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="a916f-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a916f-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a916f-145">Request headers</span></span>

<span data-ttu-id="a916f-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a916f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a916f-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a916f-147">Request body</span></span>

<span data-ttu-id="a916f-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="a916f-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a916f-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a916f-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a916f-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a916f-150">REST response</span></span>

<span data-ttu-id="a916f-151">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ServiceCostLineItem](service-costs-resources.md) , który zawiera informacje o kosztach usługi.</span><span class="sxs-lookup"><span data-stu-id="a916f-151">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a916f-152">Następujące właściwości *dotyczą tylko* elementów wiersza kosztu usługi, w których produkt jest *jednorazowym zakupem*: **ProductID**, **ProductName**, **identyfikatora skuId**, **skuName**, **availabilityId**, **publisherId**, **PublisherName**, **termAndBillingCycle**, **discountDetails**.</span><span class="sxs-lookup"><span data-stu-id="a916f-152">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="a916f-153">Te właściwości *nie dotyczą* elementów wiersza usługi, w przypadku których produkt jest *cyklicznym zakupem*.</span><span class="sxs-lookup"><span data-stu-id="a916f-153">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="a916f-154">Na przykład te właściwości *nie mają zastosowania* do pakietu Office 365 i platformy Azure opartego na subskrypcjach.</span><span class="sxs-lookup"><span data-stu-id="a916f-154">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a916f-155">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a916f-155">Response success and error codes</span></span>

<span data-ttu-id="a916f-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="a916f-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a916f-157">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a916f-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a916f-158">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a916f-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a916f-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a916f-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": "Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
