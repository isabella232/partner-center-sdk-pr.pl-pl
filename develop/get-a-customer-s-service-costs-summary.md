---
title: Pobieranie podsumowania kosztów usług klienta
description: Pobiera koszty usługi klienta dla określonego okresu rozliczeniowego.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 635e61342e13c3676120ec0df02f1e8bffda64ac
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768106"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="f3fda-103">Pobieranie podsumowania kosztów usług klienta</span><span class="sxs-lookup"><span data-stu-id="f3fda-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="f3fda-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="f3fda-104">**Applies to:**</span></span>

- <span data-ttu-id="f3fda-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="f3fda-105">Partner Center</span></span>

<span data-ttu-id="f3fda-106">Pobiera koszty usługi klienta dla określonego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="f3fda-106">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3fda-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f3fda-107">Prerequisites</span></span>

- <span data-ttu-id="f3fda-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f3fda-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f3fda-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3fda-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="f3fda-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f3fda-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f3fda-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="f3fda-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f3fda-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="f3fda-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f3fda-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="f3fda-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f3fda-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="f3fda-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f3fda-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f3fda-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f3fda-116">Wskaźnik okresu rozliczeniowego ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="f3fda-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="f3fda-117">C\#</span><span class="sxs-lookup"><span data-stu-id="f3fda-117">C\#</span></span>

<span data-ttu-id="f3fda-118">Aby pobrać podsumowanie kosztów usługi dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="f3fda-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="f3fda-119">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="f3fda-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="f3fda-120">Użyj właściwości [**Servicecosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) , aby uzyskać interfejs do obsługi kosztów usługi klienta.</span><span class="sxs-lookup"><span data-stu-id="f3fda-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="f3fda-121">Wywołaj metodę [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) z elementem członkowskim wyliczenia [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) , aby zwracał [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="f3fda-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="f3fda-122">Użyj metody [**IServiceCostsCollection. Summary. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) , aby uzyskać podsumowanie kosztów usługi klienta.</span><span class="sxs-lookup"><span data-stu-id="f3fda-122">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="f3fda-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f3fda-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f3fda-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f3fda-124">Request syntax</span></span>

| <span data-ttu-id="f3fda-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="f3fda-125">Method</span></span>  | <span data-ttu-id="f3fda-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f3fda-126">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f3fda-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f3fda-127">**GET**</span></span> | <span data-ttu-id="f3fda-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/servicecosts/{Billing-period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f3fda-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f3fda-129">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="f3fda-129">URI parameters</span></span>

<span data-ttu-id="f3fda-130">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="f3fda-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="f3fda-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f3fda-131">Name</span></span>           | <span data-ttu-id="f3fda-132">Typ</span><span class="sxs-lookup"><span data-stu-id="f3fda-132">Type</span></span>   | <span data-ttu-id="f3fda-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f3fda-133">Required</span></span> | <span data-ttu-id="f3fda-134">Opis</span><span class="sxs-lookup"><span data-stu-id="f3fda-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f3fda-135">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="f3fda-135">customer-id</span></span>    | <span data-ttu-id="f3fda-136">guid</span><span class="sxs-lookup"><span data-stu-id="f3fda-136">guid</span></span>   | <span data-ttu-id="f3fda-137">Tak</span><span class="sxs-lookup"><span data-stu-id="f3fda-137">Yes</span></span>      | <span data-ttu-id="f3fda-138">Identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="f3fda-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="f3fda-139">rozliczenia — okres</span><span class="sxs-lookup"><span data-stu-id="f3fda-139">billing-period</span></span> | <span data-ttu-id="f3fda-140">ciąg</span><span class="sxs-lookup"><span data-stu-id="f3fda-140">string</span></span> | <span data-ttu-id="f3fda-141">Tak</span><span class="sxs-lookup"><span data-stu-id="f3fda-141">Yes</span></span>      | <span data-ttu-id="f3fda-142">Wskaźnik reprezentujący okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="f3fda-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="f3fda-143">Jedyną obsługiwaną wartością jest MostRecent.</span><span class="sxs-lookup"><span data-stu-id="f3fda-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="f3fda-144">Przypadek ciągu nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="f3fda-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f3fda-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f3fda-145">Request headers</span></span>

<span data-ttu-id="f3fda-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f3fda-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f3fda-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f3fda-147">Request body</span></span>

<span data-ttu-id="f3fda-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="f3fda-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f3fda-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f3fda-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f3fda-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f3fda-150">REST response</span></span>

<span data-ttu-id="f3fda-151">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ServiceCostsSummary](service-costs-resources.md) , który zawiera informacje o kosztach usługi.</span><span class="sxs-lookup"><span data-stu-id="f3fda-151">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f3fda-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f3fda-152">Response success and error codes</span></span>

<span data-ttu-id="f3fda-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="f3fda-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f3fda-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f3fda-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f3fda-155">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f3fda-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f3fda-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f3fda-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 766
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "billingStartDate": "2015-12-12T00:00:00Z",
    "billingEndDate": "2016-01-11T00:00:00Z",
    "pretaxTotal": 17.22,
    "tax": 0.0,
    "afterTaxTotal": 17.22,
    "currencySymbol": "$",
    "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
    "details":
     [
        {
            "invoiceType": "Recurring",
            "summary": {
                "billingStartDate": "2015-12-12T00:00:00Z",
                "billingEndDate": "2016-01-11T00:00:00Z",
                "pretaxTotal": 17.22,
                "tax": 0.0,
                "afterTaxTotal": 17.22,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "billingStartDate": "2019-04-01T00:00:00Z",
                "billingEndDate": "2019-04-30T23:59:59.9999999Z",
                "pretaxTotal": 2,
                "tax": 0.2,
                "afterTaxTotal": 2.2,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        }
    ],
    "links": {
        "serviceCostLineItems": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "ServiceCostsSummary"
    }
}
```
