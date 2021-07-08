---
title: Pobieranie podsumowania kosztów usług klienta
description: Pobiera koszty obsługi klienta dla określonego okresu rozliczeniowego.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cab23238b5f62a02a5f7368f626648d5b1b5b7e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874911"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="2ff94-103">Pobieranie podsumowania kosztów usług klienta</span><span class="sxs-lookup"><span data-stu-id="2ff94-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="2ff94-104">Pobiera koszty obsługi klienta dla określonego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="2ff94-104">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ff94-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ff94-105">Prerequisites</span></span>

- <span data-ttu-id="2ff94-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2ff94-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2ff94-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ff94-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="2ff94-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2ff94-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2ff94-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2ff94-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2ff94-110">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="2ff94-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2ff94-111">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="2ff94-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2ff94-112">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="2ff94-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2ff94-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2ff94-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2ff94-114">Wskaźnik okresu rozliczeniowego ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="2ff94-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="2ff94-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2ff94-115">C\#</span></span>

<span data-ttu-id="2ff94-116">Aby pobrać podsumowanie kosztów usługi dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="2ff94-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="2ff94-117">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="2ff94-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="2ff94-118">Użyj właściwości [**ServiceCosts,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) aby uzyskać interfejs do operacji zbierania kosztów obsługi klienta.</span><span class="sxs-lookup"><span data-stu-id="2ff94-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="2ff94-119">Wywołaj [**metodę ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) z elementem członkowskim wyliczenia [**ServiceCostsBillingPeriod,**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) aby zwrócić element [**IServiceCostsCollection.**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)</span><span class="sxs-lookup"><span data-stu-id="2ff94-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="2ff94-120">Użyj metody [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) aby uzyskać podsumowanie kosztów usług klienta.</span><span class="sxs-lookup"><span data-stu-id="2ff94-120">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="2ff94-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2ff94-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2ff94-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2ff94-122">Request syntax</span></span>

| <span data-ttu-id="2ff94-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="2ff94-123">Method</span></span>  | <span data-ttu-id="2ff94-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2ff94-124">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ff94-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="2ff94-125">**GET**</span></span> | <span data-ttu-id="2ff94-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/servicecosts/{okres rozliczeniowy} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2ff94-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2ff94-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="2ff94-127">URI parameters</span></span>

<span data-ttu-id="2ff94-128">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="2ff94-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="2ff94-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2ff94-129">Name</span></span>           | <span data-ttu-id="2ff94-130">Typ</span><span class="sxs-lookup"><span data-stu-id="2ff94-130">Type</span></span>   | <span data-ttu-id="2ff94-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2ff94-131">Required</span></span> | <span data-ttu-id="2ff94-132">Opis</span><span class="sxs-lookup"><span data-stu-id="2ff94-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ff94-133">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="2ff94-133">customer-id</span></span>    | <span data-ttu-id="2ff94-134">guid</span><span class="sxs-lookup"><span data-stu-id="2ff94-134">guid</span></span>   | <span data-ttu-id="2ff94-135">Tak</span><span class="sxs-lookup"><span data-stu-id="2ff94-135">Yes</span></span>      | <span data-ttu-id="2ff94-136">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="2ff94-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="2ff94-137">okres rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="2ff94-137">billing-period</span></span> | <span data-ttu-id="2ff94-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="2ff94-138">string</span></span> | <span data-ttu-id="2ff94-139">Tak</span><span class="sxs-lookup"><span data-stu-id="2ff94-139">Yes</span></span>      | <span data-ttu-id="2ff94-140">Wskaźnik reprezentujący okres rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="2ff94-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="2ff94-141">Jedyną obsługiwaną wartością jest MostRecent.</span><span class="sxs-lookup"><span data-stu-id="2ff94-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="2ff94-142">Przypadek ciągu nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="2ff94-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2ff94-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2ff94-143">Request headers</span></span>

<span data-ttu-id="2ff94-144">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2ff94-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2ff94-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2ff94-145">Request body</span></span>

<span data-ttu-id="2ff94-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="2ff94-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2ff94-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2ff94-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2ff94-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2ff94-148">REST response</span></span>

<span data-ttu-id="2ff94-149">W przypadku powodzenia treść odpowiedzi zawiera [zasób ServiceCostsSummary](service-costs-resources.md) zawierający informacje o kosztach usługi.</span><span class="sxs-lookup"><span data-stu-id="2ff94-149">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2ff94-150">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2ff94-150">Response success and error codes</span></span>

<span data-ttu-id="2ff94-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2ff94-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2ff94-152">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2ff94-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2ff94-153">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2ff94-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2ff94-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2ff94-154">Response example</span></span>

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
