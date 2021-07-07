---
title: Pobieranie konta użytkownika według identyfikatora
description: Pobierz określone konto użytkownika dla klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a7cac98a8081a8557dcadfb0724f5497be7d14c
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760270"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="9283c-103">Pobieranie konta użytkownika według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="9283c-103">Get a user account by ID</span></span>

<span data-ttu-id="9283c-104">Pobierz określone konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="9283c-104">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="9283c-105">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9283c-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9283c-106">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9283c-106">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9283c-107">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9283c-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9283c-108">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9283c-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9283c-109">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="9283c-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9283c-110">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="9283c-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9283c-111">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="9283c-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9283c-112">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9283c-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9283c-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9283c-113">C\#</span></span>

<span data-ttu-id="9283c-114">Aby pobrać konto użytkownika dla klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="9283c-114">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="9283c-115">Następnie wywołaj [**metodę Users.ById,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) aby pobrać określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9283c-115">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="9283c-116">Na koniec wywołaj [**metodę Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) aby pobrać konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9283c-116">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="9283c-117">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9283c-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9283c-118">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="9283c-118">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9283c-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9283c-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9283c-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9283c-120">Request syntax</span></span>

| <span data-ttu-id="9283c-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="9283c-121">Method</span></span>  | <span data-ttu-id="9283c-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9283c-122">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9283c-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9283c-123">**GET**</span></span> | <span data-ttu-id="9283c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9283c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9283c-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9283c-125">URI parameter</span></span>

<span data-ttu-id="9283c-126">Użyj następujących parametrów identyfikatorów URI, aby zidentyfikować właściwego klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9283c-126">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="9283c-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9283c-127">Name</span></span>                   | <span data-ttu-id="9283c-128">Typ</span><span class="sxs-lookup"><span data-stu-id="9283c-128">Type</span></span>     | <span data-ttu-id="9283c-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9283c-129">Required</span></span> | <span data-ttu-id="9283c-130">Opis</span><span class="sxs-lookup"><span data-stu-id="9283c-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9283c-131">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="9283c-131">**customer-tenant-id**</span></span> | <span data-ttu-id="9283c-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="9283c-132">**guid**</span></span> | <span data-ttu-id="9283c-133">Y</span><span class="sxs-lookup"><span data-stu-id="9283c-133">Y</span></span>        | <span data-ttu-id="9283c-134">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="9283c-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="9283c-135">**identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="9283c-135">**user-id**</span></span>            | <span data-ttu-id="9283c-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="9283c-136">**guid**</span></span> | <span data-ttu-id="9283c-137">Y</span><span class="sxs-lookup"><span data-stu-id="9283c-137">Y</span></span>        | <span data-ttu-id="9283c-138">Wartość jest identyfikatorem użytkownika sformatowanym w **formacie** GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9283c-138">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="9283c-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9283c-139">Request headers</span></span>

<span data-ttu-id="9283c-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9283c-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9283c-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9283c-141">Request body</span></span>

<span data-ttu-id="9283c-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="9283c-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9283c-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9283c-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="9283c-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9283c-144">REST response</span></span>

<span data-ttu-id="9283c-145">W przypadku powodzenia ta metoda zwraca konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="9283c-145">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9283c-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9283c-146">Response success and error codes</span></span>

<span data-ttu-id="9283c-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9283c-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9283c-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9283c-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9283c-149">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9283c-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9283c-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9283c-150">Response example</span></span>

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
