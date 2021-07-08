---
title: Pobieranie elementów wiersza kosztów usług klienta
description: Pobiera pozycje kosztów obsługi klienta dla określonego okresu rozliczeniowego.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1bc2914d7c8d41c6d806131444fdc241aa1feb90
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874945"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="3b716-103">Pobieranie elementów wiersza kosztów usług klienta</span><span class="sxs-lookup"><span data-stu-id="3b716-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="3b716-104">Pobiera pozycje kosztów obsługi klienta dla określonego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="3b716-104">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b716-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3b716-105">Prerequisites</span></span>

- <span data-ttu-id="3b716-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3b716-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3b716-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3b716-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="3b716-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3b716-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3b716-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="3b716-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3b716-110">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="3b716-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3b716-111">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="3b716-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3b716-112">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="3b716-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3b716-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3b716-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3b716-114">Wskaźnik okresu rozliczeniowego ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="3b716-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="3b716-115">C\#</span><span class="sxs-lookup"><span data-stu-id="3b716-115">C\#</span></span>

<span data-ttu-id="3b716-116">Aby pobrać podsumowanie kosztów usługi dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="3b716-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="3b716-117">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="3b716-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="3b716-118">Użyj właściwości [**ServiceCosts,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) aby uzyskać interfejs do operacji zbierania kosztów obsługi klienta.</span><span class="sxs-lookup"><span data-stu-id="3b716-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="3b716-119">Wywołaj [**metodę ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) z elementem członkowskim wyliczenia [**ServiceCostsBillingPeriod,**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) aby zwrócić element [**IServiceCostsCollection.**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)</span><span class="sxs-lookup"><span data-stu-id="3b716-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="3b716-120">Użyj metody [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) aby pobrać pozycje kosztów usług klienta.</span><span class="sxs-lookup"><span data-stu-id="3b716-120">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="3b716-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3b716-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3b716-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3b716-122">Request syntax</span></span>

| <span data-ttu-id="3b716-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="3b716-123">Method</span></span>  | <span data-ttu-id="3b716-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3b716-124">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3b716-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3b716-125">**GET**</span></span> | <span data-ttu-id="3b716-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/servicecosts/{billing-period}/lineitems HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3b716-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3b716-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="3b716-127">URI parameters</span></span>

<span data-ttu-id="3b716-128">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="3b716-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="3b716-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3b716-129">Name</span></span>           | <span data-ttu-id="3b716-130">Typ</span><span class="sxs-lookup"><span data-stu-id="3b716-130">Type</span></span>   | <span data-ttu-id="3b716-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3b716-131">Required</span></span> | <span data-ttu-id="3b716-132">Opis</span><span class="sxs-lookup"><span data-stu-id="3b716-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3b716-133">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="3b716-133">customer-id</span></span>    | <span data-ttu-id="3b716-134">guid</span><span class="sxs-lookup"><span data-stu-id="3b716-134">guid</span></span>   | <span data-ttu-id="3b716-135">Tak</span><span class="sxs-lookup"><span data-stu-id="3b716-135">Yes</span></span>      | <span data-ttu-id="3b716-136">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="3b716-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="3b716-137">okres rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="3b716-137">billing-period</span></span> | <span data-ttu-id="3b716-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="3b716-138">string</span></span> | <span data-ttu-id="3b716-139">Tak</span><span class="sxs-lookup"><span data-stu-id="3b716-139">Yes</span></span>      | <span data-ttu-id="3b716-140">Wskaźnik reprezentujący okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="3b716-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="3b716-141">Jedyną obsługiwaną wartością jest MostRecent.</span><span class="sxs-lookup"><span data-stu-id="3b716-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="3b716-142">Przypadek ciągu nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="3b716-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3b716-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3b716-143">Request headers</span></span>

<span data-ttu-id="3b716-144">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3b716-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3b716-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3b716-145">Request body</span></span>

<span data-ttu-id="3b716-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="3b716-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3b716-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3b716-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3b716-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3b716-148">REST response</span></span>

<span data-ttu-id="3b716-149">W przypadku powodzenia treść odpowiedzi zawiera [zasób ServiceCostLineItem,](service-costs-resources.md) który zawiera informacje o kosztach usługi.</span><span class="sxs-lookup"><span data-stu-id="3b716-149">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b716-150">Następujące właściwości  dotyczą tylko elementów wiersza kosztu usługi, w przypadku których produkt jest zakupem tylko *raz:* **productId,** **productName,** **skuId,** **skuName,** **availabilityId,** **publisherId,** **publisherName,** **termAndBillingCycle,** **discountDetails.**</span><span class="sxs-lookup"><span data-stu-id="3b716-150">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="3b716-151">Te właściwości *nie dotyczą pozycji* usług, w przypadku których produkt jest *cyklicznym zakupem.*</span><span class="sxs-lookup"><span data-stu-id="3b716-151">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="3b716-152">Na przykład te właściwości *nie mają zastosowania do* zasobów opartych na Office 365 azure.</span><span class="sxs-lookup"><span data-stu-id="3b716-152">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3b716-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3b716-153">Response success and error codes</span></span>

<span data-ttu-id="3b716-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="3b716-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3b716-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3b716-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3b716-156">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3b716-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3b716-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3b716-157">Response example</span></span>

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
