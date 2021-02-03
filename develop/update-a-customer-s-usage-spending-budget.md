---
title: Aktualizowanie budżetu wydatków użycia klienta
description: Zaktualizuj budżet wydatków przyznany do użycia przez klienta.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 839305fb8fad3ce2442ab93e1d8a4a170b4d41c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768381"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="b5af3-103">Aktualizowanie budżetu wydatków użycia klienta</span><span class="sxs-lookup"><span data-stu-id="b5af3-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="b5af3-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="b5af3-104">**Applies To**</span></span>

- <span data-ttu-id="b5af3-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b5af3-105">Partner Center</span></span>
- <span data-ttu-id="b5af3-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="b5af3-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b5af3-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b5af3-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b5af3-108">Zaktualizuj [budżet wydatków](customer-usage-resources.md#customerusagesummary) przyznany do użycia przez klienta.</span><span class="sxs-lookup"><span data-stu-id="b5af3-108">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5af3-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b5af3-109">Prerequisites</span></span>

- <span data-ttu-id="b5af3-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b5af3-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b5af3-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5af3-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b5af3-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5af3-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b5af3-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="b5af3-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b5af3-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="b5af3-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b5af3-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="b5af3-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b5af3-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="b5af3-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b5af3-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5af3-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b5af3-118">C\#</span><span class="sxs-lookup"><span data-stu-id="b5af3-118">C\#</span></span>

<span data-ttu-id="b5af3-119">Aby zaktualizować budżet wydatków użycia klienta, należy najpierw utworzyć nowy obiekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="b5af3-119">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="b5af3-120">Następnie użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="b5af3-120">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="b5af3-121">Następnie uzyskaj dostęp do właściwości [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) i przekaż zaktualizowany budżet użycia do metody [**patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) lub [**PatchAsync ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) .</span><span class="sxs-lookup"><span data-stu-id="b5af3-121">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a><span data-ttu-id="b5af3-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b5af3-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5af3-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b5af3-123">Request syntax</span></span>

| <span data-ttu-id="b5af3-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="b5af3-124">Method</span></span>    | <span data-ttu-id="b5af3-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b5af3-125">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5af3-126">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="b5af3-126">**PATCH**</span></span> | <span data-ttu-id="b5af3-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/usagebudget http/1.1</span><span class="sxs-lookup"><span data-stu-id="b5af3-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b5af3-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b5af3-128">URI parameter</span></span>

<span data-ttu-id="b5af3-129">Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="b5af3-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="b5af3-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b5af3-130">Name</span></span>                   | <span data-ttu-id="b5af3-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b5af3-131">Type</span></span>     | <span data-ttu-id="b5af3-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b5af3-132">Required</span></span> | <span data-ttu-id="b5af3-133">Opis</span><span class="sxs-lookup"><span data-stu-id="b5af3-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5af3-134">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="b5af3-134">**customer-tenant-id**</span></span> | <span data-ttu-id="b5af3-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="b5af3-135">**guid**</span></span> | <span data-ttu-id="b5af3-136">Y</span><span class="sxs-lookup"><span data-stu-id="b5af3-136">Y</span></span>        | <span data-ttu-id="b5af3-137">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="b5af3-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b5af3-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b5af3-138">Request headers</span></span>

<span data-ttu-id="b5af3-139">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b5af3-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5af3-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b5af3-140">Request body</span></span>

<span data-ttu-id="b5af3-141">Pełny zasób.</span><span class="sxs-lookup"><span data-stu-id="b5af3-141">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="b5af3-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b5af3-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a><span data-ttu-id="b5af3-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b5af3-143">REST response</span></span>

<span data-ttu-id="b5af3-144">Jeśli to się powiedzie, ta metoda zwraca budżet wydatków użytkownika ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="b5af3-144">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5af3-145">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b5af3-145">Response success and error codes</span></span>

<span data-ttu-id="b5af3-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b5af3-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b5af3-147">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b5af3-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5af3-148">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b5af3-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b5af3-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b5af3-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

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
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
