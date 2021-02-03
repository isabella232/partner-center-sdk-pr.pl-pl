---
title: Pobierz budżet wydatków użycia klienta
description: Możesz użyć budżetu wydatków (obiektu SpendingBudget), aby zaktualizować Podsumowanie użycia klienta (zasób CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768105"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="c8e18-103">Pobierz budżet wydatków użycia klienta</span><span class="sxs-lookup"><span data-stu-id="c8e18-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="c8e18-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="c8e18-104">**Applies to:**</span></span>

- <span data-ttu-id="c8e18-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c8e18-105">Partner Center</span></span>
- <span data-ttu-id="c8e18-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="c8e18-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c8e18-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c8e18-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c8e18-108">Budżet wydatków (obiekt **SpendingBudget** ) można zaktualizować w [podsumowaniu użytkowania klienta (zasób **CustomerUsageSummary** )](customer-usage-resources.md#customerusagesummary).</span><span class="sxs-lookup"><span data-stu-id="c8e18-108">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e18-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c8e18-109">Prerequisites</span></span>

- <span data-ttu-id="c8e18-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c8e18-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c8e18-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8e18-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c8e18-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8e18-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c8e18-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c8e18-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c8e18-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="c8e18-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c8e18-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="c8e18-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c8e18-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="c8e18-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c8e18-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8e18-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c8e18-118">C\#</span><span class="sxs-lookup"><span data-stu-id="c8e18-118">C\#</span></span>

<span data-ttu-id="c8e18-119">Aby zaktualizować budżet wydatków użycia klienta:</span><span class="sxs-lookup"><span data-stu-id="c8e18-119">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="c8e18-120">Utwórz nowy obiekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="c8e18-120">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="c8e18-121">Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) , aby wywołać metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="c8e18-121">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="c8e18-122">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) , aby uzyskać budżet użycia klienta.</span><span class="sxs-lookup"><span data-stu-id="c8e18-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a><span data-ttu-id="c8e18-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c8e18-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c8e18-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c8e18-124">Request syntax</span></span>

| <span data-ttu-id="c8e18-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="c8e18-125">Method</span></span>    | <span data-ttu-id="c8e18-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c8e18-126">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c8e18-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c8e18-127">**GET**</span></span> | <span data-ttu-id="c8e18-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/usagebudget http/1.1</span><span class="sxs-lookup"><span data-stu-id="c8e18-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c8e18-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c8e18-129">URI parameter</span></span>

<span data-ttu-id="c8e18-130">Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="c8e18-130">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="c8e18-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c8e18-131">Name</span></span>                   | <span data-ttu-id="c8e18-132">Typ</span><span class="sxs-lookup"><span data-stu-id="c8e18-132">Type</span></span>     | <span data-ttu-id="c8e18-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c8e18-133">Required</span></span> | <span data-ttu-id="c8e18-134">Opis</span><span class="sxs-lookup"><span data-stu-id="c8e18-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c8e18-135">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="c8e18-135">**customer-tenant-id**</span></span> | <span data-ttu-id="c8e18-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="c8e18-136">**guid**</span></span> | <span data-ttu-id="c8e18-137">Y</span><span class="sxs-lookup"><span data-stu-id="c8e18-137">Y</span></span>        | <span data-ttu-id="c8e18-138">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="c8e18-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c8e18-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c8e18-139">Request headers</span></span>

<span data-ttu-id="c8e18-140">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c8e18-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c8e18-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c8e18-141">Request body</span></span>

<span data-ttu-id="c8e18-142">Pełny zasób.</span><span class="sxs-lookup"><span data-stu-id="c8e18-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="c8e18-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c8e18-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="c8e18-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c8e18-144">REST response</span></span>

<span data-ttu-id="c8e18-145">Jeśli to się powiedzie, ta metoda zwraca budżet wydatków użytkownika ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="c8e18-145">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c8e18-146">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c8e18-146">Response success and error codes</span></span>

<span data-ttu-id="c8e18-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="c8e18-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c8e18-148">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c8e18-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c8e18-149">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c8e18-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c8e18-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c8e18-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```
