---
title: Pobieranie listy wszystkich kont użytkowników dla klienta
description: Jak uzyskać listę wszystkich kont użytkowników należących do jednego z twoich klientów.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f3d5fcc610eae8c1bff056c1e4a9e7a74093c87d
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874571"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="1490a-103">Pobieranie listy wszystkich kont użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="1490a-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="1490a-104">W tym artykule opisano sposób uzyskania listy wszystkich kont użytkowników należących do jednego z klientów.</span><span class="sxs-lookup"><span data-stu-id="1490a-104">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="1490a-105">Aby sprawdzić pojedyncze konto użytkownika według identyfikatora, zobacz [Get a user account by ID (Uzyskiwanie konta użytkownika według identyfikatora).](get-a-user-account-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="1490a-105">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1490a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1490a-106">Prerequisites</span></span>

- <span data-ttu-id="1490a-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1490a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1490a-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1490a-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1490a-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1490a-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1490a-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1490a-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1490a-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="1490a-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1490a-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="1490a-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1490a-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="1490a-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1490a-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1490a-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1490a-115">C\#</span><span class="sxs-lookup"><span data-stu-id="1490a-115">C\#</span></span>

<span data-ttu-id="1490a-116">Aby pobrać kolekcję wszystkich kont użytkowników dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="1490a-116">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="1490a-117">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="1490a-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="1490a-118">Wywołaj [**metodę Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) aby pobrać kolekcję.</span><span class="sxs-lookup"><span data-stu-id="1490a-118">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="1490a-119">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="1490a-119">For an example, see the following:</span></span>

- <span data-ttu-id="1490a-120">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1490a-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1490a-121">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="1490a-121">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1490a-122">Klasa: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="1490a-122">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1490a-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1490a-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1490a-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1490a-124">Request syntax</span></span>

| <span data-ttu-id="1490a-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="1490a-125">Method</span></span>  | <span data-ttu-id="1490a-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1490a-126">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="1490a-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1490a-127">**GET**</span></span> | <span data-ttu-id="1490a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1490a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1490a-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1490a-129">URI parameter</span></span>

<span data-ttu-id="1490a-130">Użyj następującego parametru URI, aby zidentyfikować prawidłowego klienta.</span><span class="sxs-lookup"><span data-stu-id="1490a-130">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="1490a-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1490a-131">Name</span></span>                   | <span data-ttu-id="1490a-132">Typ</span><span class="sxs-lookup"><span data-stu-id="1490a-132">Type</span></span>     | <span data-ttu-id="1490a-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1490a-133">Required</span></span> | <span data-ttu-id="1490a-134">Opis</span><span class="sxs-lookup"><span data-stu-id="1490a-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1490a-135">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="1490a-135">**customer-tenant-id**</span></span> | <span data-ttu-id="1490a-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="1490a-136">**guid**</span></span> | <span data-ttu-id="1490a-137">Y</span><span class="sxs-lookup"><span data-stu-id="1490a-137">Y</span></span>        | <span data-ttu-id="1490a-138">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="1490a-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1490a-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1490a-139">Request headers</span></span>

<span data-ttu-id="1490a-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1490a-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1490a-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1490a-141">Request body</span></span>

<span data-ttu-id="1490a-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="1490a-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1490a-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1490a-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1490a-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1490a-144">REST response</span></span>

<span data-ttu-id="1490a-145">W przypadku powodzenia ta metoda zwraca kolekcję kont użytkowników dla klienta.</span><span class="sxs-lookup"><span data-stu-id="1490a-145">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1490a-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1490a-146">Response success and error codes</span></span>

<span data-ttu-id="1490a-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1490a-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1490a-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1490a-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1490a-149">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1490a-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1490a-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1490a-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
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
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
