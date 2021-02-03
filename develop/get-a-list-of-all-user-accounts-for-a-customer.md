---
title: Pobieranie listy wszystkich kont użytkowników dla klienta
description: Jak uzyskać listę wszystkich kont użytkowników należących do jednego z klientów.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f2b1bcf9926e02232b6e2cc68b71e992b015324
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768097"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="be398-103">Pobieranie listy wszystkich kont użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="be398-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="be398-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="be398-104">**Applies to:**</span></span>

- <span data-ttu-id="be398-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="be398-105">Partner Center</span></span>

<span data-ttu-id="be398-106">W tym artykule opisano, jak uzyskać listę wszystkich kont użytkowników należących do jednego z klientów.</span><span class="sxs-lookup"><span data-stu-id="be398-106">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="be398-107">Aby wyszukać jedno konto użytkownika według identyfikatora, zobacz [pobieranie konta użytkownika według identyfikatora](get-a-user-account-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="be398-107">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be398-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be398-108">Prerequisites</span></span>

- <span data-ttu-id="be398-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="be398-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="be398-110">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be398-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="be398-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be398-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="be398-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="be398-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="be398-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="be398-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="be398-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="be398-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="be398-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="be398-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="be398-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be398-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="be398-117">C\#</span><span class="sxs-lookup"><span data-stu-id="be398-117">C\#</span></span>

<span data-ttu-id="be398-118">Aby pobrać kolekcję wszystkich kont użytkowników dla określonego klienta:</span><span class="sxs-lookup"><span data-stu-id="be398-118">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="be398-119">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="be398-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="be398-120">Wywołaj metodę [**users. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) w celu pobrania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="be398-120">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="be398-121">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="be398-121">For an example, see the following:</span></span>

- <span data-ttu-id="be398-122">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="be398-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="be398-123">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="be398-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="be398-124">Klasa: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="be398-124">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="be398-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="be398-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="be398-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="be398-126">Request syntax</span></span>

| <span data-ttu-id="be398-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="be398-127">Method</span></span>  | <span data-ttu-id="be398-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="be398-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="be398-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="be398-129">**GET**</span></span> | <span data-ttu-id="be398-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users http/1.1</span><span class="sxs-lookup"><span data-stu-id="be398-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="be398-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="be398-131">URI parameter</span></span>

<span data-ttu-id="be398-132">Użyj następującego parametru identyfikatora URI, aby zidentyfikować odpowiedniego klienta.</span><span class="sxs-lookup"><span data-stu-id="be398-132">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="be398-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="be398-133">Name</span></span>                   | <span data-ttu-id="be398-134">Typ</span><span class="sxs-lookup"><span data-stu-id="be398-134">Type</span></span>     | <span data-ttu-id="be398-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="be398-135">Required</span></span> | <span data-ttu-id="be398-136">Opis</span><span class="sxs-lookup"><span data-stu-id="be398-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="be398-137">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="be398-137">**customer-tenant-id**</span></span> | <span data-ttu-id="be398-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="be398-138">**guid**</span></span> | <span data-ttu-id="be398-139">Y</span><span class="sxs-lookup"><span data-stu-id="be398-139">Y</span></span>        | <span data-ttu-id="be398-140">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="be398-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="be398-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="be398-141">Request headers</span></span>

<span data-ttu-id="be398-142">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="be398-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="be398-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="be398-143">Request body</span></span>

<span data-ttu-id="be398-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="be398-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="be398-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="be398-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="be398-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="be398-146">REST response</span></span>

<span data-ttu-id="be398-147">Jeśli to się powiedzie, ta metoda zwraca kolekcję kont użytkowników dla klienta.</span><span class="sxs-lookup"><span data-stu-id="be398-147">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="be398-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="be398-148">Response success and error codes</span></span>

<span data-ttu-id="be398-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="be398-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="be398-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="be398-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="be398-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="be398-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="be398-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="be398-152">Response example</span></span>

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
