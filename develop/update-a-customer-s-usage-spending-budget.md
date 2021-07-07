---
title: Aktualizowanie budżetu wydatków na użycie przez klienta
description: Zaktualizuj budżet wydatków przydzielony na potrzeby użycia przez klienta.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 043bd442266d081105e5e8767b6d597e89fc9e8b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529719"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="cdbce-103">Aktualizowanie budżetu wydatków na użycie przez klienta</span><span class="sxs-lookup"><span data-stu-id="cdbce-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="cdbce-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cdbce-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cdbce-105">Zaktualizuj budżet [wydatków](customer-usage-resources.md#customerusagesummary) przydzielony na potrzeby użycia przez klienta.</span><span class="sxs-lookup"><span data-stu-id="cdbce-105">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdbce-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cdbce-106">Prerequisites</span></span>

- <span data-ttu-id="cdbce-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cdbce-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cdbce-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cdbce-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cdbce-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cdbce-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cdbce-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="cdbce-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cdbce-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="cdbce-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cdbce-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="cdbce-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cdbce-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="cdbce-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cdbce-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cdbce-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="cdbce-115">C\#</span><span class="sxs-lookup"><span data-stu-id="cdbce-115">C\#</span></span>

<span data-ttu-id="cdbce-116">Aby zaktualizować budżet wydatków na użycie klienta, najpierw utwórz nowy obiekt [**SpendingBudget ze**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="cdbce-116">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="cdbce-117">Następnie użyj [**kolekcji IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) i wywołaj metodę [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta.</span><span class="sxs-lookup"><span data-stu-id="cdbce-117">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="cdbce-118">Następnie uzyskaj dostęp [**do właściwości UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) i przekaż zaktualizowany budżet użycia do metody [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) lub [**PatchAsync().**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync)</span><span class="sxs-lookup"><span data-stu-id="cdbce-118">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="cdbce-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cdbce-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cdbce-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cdbce-120">Request syntax</span></span>

| <span data-ttu-id="cdbce-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="cdbce-121">Method</span></span>    | <span data-ttu-id="cdbce-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cdbce-122">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cdbce-123">**Patch**</span><span class="sxs-lookup"><span data-stu-id="cdbce-123">**PATCH**</span></span> | <span data-ttu-id="cdbce-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cdbce-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cdbce-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cdbce-125">URI parameter</span></span>

<span data-ttu-id="cdbce-126">Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="cdbce-126">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="cdbce-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cdbce-127">Name</span></span>                   | <span data-ttu-id="cdbce-128">Typ</span><span class="sxs-lookup"><span data-stu-id="cdbce-128">Type</span></span>     | <span data-ttu-id="cdbce-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cdbce-129">Required</span></span> | <span data-ttu-id="cdbce-130">Opis</span><span class="sxs-lookup"><span data-stu-id="cdbce-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cdbce-131">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="cdbce-131">**customer-tenant-id**</span></span> | <span data-ttu-id="cdbce-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="cdbce-132">**guid**</span></span> | <span data-ttu-id="cdbce-133">Y</span><span class="sxs-lookup"><span data-stu-id="cdbce-133">Y</span></span>        | <span data-ttu-id="cdbce-134">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="cdbce-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cdbce-135">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cdbce-135">Request headers</span></span>

<span data-ttu-id="cdbce-136">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cdbce-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cdbce-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cdbce-137">Request body</span></span>

<span data-ttu-id="cdbce-138">Pełny zasób.</span><span class="sxs-lookup"><span data-stu-id="cdbce-138">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="cdbce-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cdbce-139">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cdbce-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cdbce-140">REST response</span></span>

<span data-ttu-id="cdbce-141">W przypadku powodzenia ta metoda zwraca budżet wydatków użytkownika ze zaktualizowaną kwotą.</span><span class="sxs-lookup"><span data-stu-id="cdbce-141">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cdbce-142">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cdbce-142">Response success and error codes</span></span>

<span data-ttu-id="cdbce-143">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="cdbce-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cdbce-144">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cdbce-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cdbce-145">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cdbce-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cdbce-146">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cdbce-146">Response example</span></span>

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
