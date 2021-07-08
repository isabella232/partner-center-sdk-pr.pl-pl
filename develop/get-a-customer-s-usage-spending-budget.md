---
title: Uzyskiwanie budżetu wydatków na użycie przez klienta
description: Budżet wydatków (obiekt SpendingBudget) umożliwia zaktualizowanie podsumowania użycia klienta (zasobu CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b55f59fff7e5d7865811ecab3e901848126d31f7
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874877"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="d67f9-103">Uzyskiwanie budżetu wydatków na użycie przez klienta</span><span class="sxs-lookup"><span data-stu-id="d67f9-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="d67f9-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d67f9-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d67f9-105">Budżet wydatków (obiekt **SpendingBudget)** można zaktualizować w podsumowaniu użycia klienta [(zasób **CustomerUsageSummary).**](customer-usage-resources.md#customerusagesummary)</span><span class="sxs-lookup"><span data-stu-id="d67f9-105">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d67f9-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d67f9-106">Prerequisites</span></span>

- <span data-ttu-id="d67f9-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d67f9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d67f9-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d67f9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d67f9-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d67f9-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d67f9-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d67f9-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d67f9-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="d67f9-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d67f9-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="d67f9-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d67f9-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="d67f9-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d67f9-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d67f9-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d67f9-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d67f9-115">C\#</span></span>

<span data-ttu-id="d67f9-116">Aby zaktualizować budżet wydatków na użycie przez klienta:</span><span class="sxs-lookup"><span data-stu-id="d67f9-116">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="d67f9-117">Utwórz nowy obiekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="d67f9-117">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="d67f9-118">Użyj [**kolekcji IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) aby wywołać metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="d67f9-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="d67f9-119">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) aby uzyskać budżet użycia klienta.</span><span class="sxs-lookup"><span data-stu-id="d67f9-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="d67f9-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d67f9-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d67f9-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d67f9-121">Request syntax</span></span>

| <span data-ttu-id="d67f9-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="d67f9-122">Method</span></span>    | <span data-ttu-id="d67f9-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d67f9-123">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d67f9-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d67f9-124">**GET**</span></span> | <span data-ttu-id="d67f9-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d67f9-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d67f9-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d67f9-126">URI parameter</span></span>

<span data-ttu-id="d67f9-127">Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="d67f9-127">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="d67f9-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d67f9-128">Name</span></span>                   | <span data-ttu-id="d67f9-129">Typ</span><span class="sxs-lookup"><span data-stu-id="d67f9-129">Type</span></span>     | <span data-ttu-id="d67f9-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d67f9-130">Required</span></span> | <span data-ttu-id="d67f9-131">Opis</span><span class="sxs-lookup"><span data-stu-id="d67f9-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d67f9-132">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="d67f9-132">**customer-tenant-id**</span></span> | <span data-ttu-id="d67f9-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="d67f9-133">**guid**</span></span> | <span data-ttu-id="d67f9-134">Y</span><span class="sxs-lookup"><span data-stu-id="d67f9-134">Y</span></span>        | <span data-ttu-id="d67f9-135">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="d67f9-135">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d67f9-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d67f9-136">Request headers</span></span>

<span data-ttu-id="d67f9-137">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d67f9-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d67f9-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d67f9-138">Request body</span></span>

<span data-ttu-id="d67f9-139">Pełny zasób.</span><span class="sxs-lookup"><span data-stu-id="d67f9-139">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="d67f9-140">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d67f9-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="d67f9-141">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d67f9-141">REST response</span></span>

<span data-ttu-id="d67f9-142">W przypadku powodzenia ta metoda zwraca budżet wydatków użytkownika ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="d67f9-142">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d67f9-143">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d67f9-143">Response success and error codes</span></span>

<span data-ttu-id="d67f9-144">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d67f9-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d67f9-145">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d67f9-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d67f9-146">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d67f9-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d67f9-147">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d67f9-147">Response example</span></span>

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
