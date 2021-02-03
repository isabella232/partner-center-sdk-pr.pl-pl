---
title: Pobieranie konta użytkownika według identyfikatora
description: Uzyskaj określone konto użytkownika dla klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a2f42001365324a65376318cb1f2d57dc123df0c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768054"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="65736-103">Pobieranie konta użytkownika według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="65736-103">Get a user account by ID</span></span>

<span data-ttu-id="65736-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="65736-104">**Applies To**</span></span>

- <span data-ttu-id="65736-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="65736-105">Partner Center</span></span>

<span data-ttu-id="65736-106">Uzyskaj określone konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="65736-106">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="65736-107">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="65736-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="65736-108">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65736-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="65736-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="65736-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="65736-110">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="65736-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="65736-111">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="65736-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="65736-112">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="65736-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="65736-113">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="65736-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="65736-114">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="65736-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="65736-115">C\#</span><span class="sxs-lookup"><span data-stu-id="65736-115">C\#</span></span>

<span data-ttu-id="65736-116">Aby pobrać konto użytkownika dla klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="65736-116">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="65736-117">Następnie Wywołaj metodę [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby pobrać określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65736-117">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="65736-118">Na koniec Wywołaj metodę [**users. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) , aby pobrać konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65736-118">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="65736-119">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="65736-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="65736-120">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="65736-120">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="65736-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="65736-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="65736-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="65736-122">Request syntax</span></span>

| <span data-ttu-id="65736-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="65736-123">Method</span></span>  | <span data-ttu-id="65736-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="65736-124">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="65736-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="65736-125">**GET**</span></span> | <span data-ttu-id="65736-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="65736-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="65736-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="65736-127">URI parameter</span></span>

<span data-ttu-id="65736-128">Użyj następujących parametrów identyfikatora URI, aby zidentyfikować prawidłowego klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65736-128">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="65736-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="65736-129">Name</span></span>                   | <span data-ttu-id="65736-130">Typ</span><span class="sxs-lookup"><span data-stu-id="65736-130">Type</span></span>     | <span data-ttu-id="65736-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="65736-131">Required</span></span> | <span data-ttu-id="65736-132">Opis</span><span class="sxs-lookup"><span data-stu-id="65736-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="65736-133">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="65736-133">**customer-tenant-id**</span></span> | <span data-ttu-id="65736-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="65736-134">**guid**</span></span> | <span data-ttu-id="65736-135">Y</span><span class="sxs-lookup"><span data-stu-id="65736-135">Y</span></span>        | <span data-ttu-id="65736-136">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="65736-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="65736-137">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="65736-137">**user-id**</span></span>            | <span data-ttu-id="65736-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="65736-138">**guid**</span></span> | <span data-ttu-id="65736-139">Y</span><span class="sxs-lookup"><span data-stu-id="65736-139">Y</span></span>        | <span data-ttu-id="65736-140">Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65736-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="65736-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="65736-141">Request headers</span></span>

<span data-ttu-id="65736-142">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="65736-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="65736-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="65736-143">Request body</span></span>

<span data-ttu-id="65736-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="65736-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="65736-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="65736-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="65736-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="65736-146">REST response</span></span>

<span data-ttu-id="65736-147">Jeśli to się powiedzie, ta metoda zwraca konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="65736-147">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="65736-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="65736-148">Response success and error codes</span></span>

<span data-ttu-id="65736-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="65736-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="65736-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="65736-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="65736-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="65736-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="65736-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="65736-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 432
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CV: uWM1EGU7+0aI2MvV.0
MS-ServerId: 020021921
Date: Wed, 21 Dec 2016 22:59:10 GMT

{
    "usageLocation": "US",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Daniel",
    "lastName": "Tsai",
    "displayName": "Daniel Tsai",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
