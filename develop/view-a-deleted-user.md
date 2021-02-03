---
title: Wyświetlanie użytkowników usuniętych dla klienta
description: Pobiera listę usuniętych zasobów CustomerUser dla klienta według identyfikatora klienta. Opcjonalnie można ustawić rozmiar strony. Musisz podać filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768230"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="f4f70-105">Wyświetlanie użytkowników usuniętych dla klienta</span><span class="sxs-lookup"><span data-stu-id="f4f70-105">View deleted users for a customer</span></span>

<span data-ttu-id="f4f70-106">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="f4f70-106">**Applies To**</span></span>

- <span data-ttu-id="f4f70-107">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="f4f70-107">Partner Center</span></span>

<span data-ttu-id="f4f70-108">Pobiera listę usuniętych zasobów CustomerUser dla klienta według identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="f4f70-108">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="f4f70-109">Opcjonalnie można ustawić rozmiar strony.</span><span class="sxs-lookup"><span data-stu-id="f4f70-109">You can optionally set a page size.</span></span> <span data-ttu-id="f4f70-110">Musisz podać filtr.</span><span class="sxs-lookup"><span data-stu-id="f4f70-110">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4f70-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f4f70-111">Prerequisites</span></span>

- <span data-ttu-id="f4f70-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f4f70-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f4f70-113">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f4f70-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f4f70-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f4f70-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f4f70-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="f4f70-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f4f70-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="f4f70-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f4f70-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="f4f70-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f4f70-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="f4f70-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f4f70-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f4f70-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="f4f70-120">Co się stanie po usunięciu konta użytkownika?</span><span class="sxs-lookup"><span data-stu-id="f4f70-120">What happens when you delete a user account?</span></span>

<span data-ttu-id="f4f70-121">Po usunięciu konta użytkownika stan użytkownika ma wartość "nieaktywne".</span><span class="sxs-lookup"><span data-stu-id="f4f70-121">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="f4f70-122">Nie jest to możliwe przez 30 dni, po upływie których konto użytkownika i powiązane z nim dane zostaną usunięte i nie można ich odzyskać.</span><span class="sxs-lookup"><span data-stu-id="f4f70-122">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="f4f70-123">Jeśli chcesz przywrócić usunięte konto użytkownika w oknie trzydziestu dni, zobacz [Przywracanie usuniętego użytkownika dla klienta](restore-a-user-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="f4f70-123">If you want to restore a deleted user account within the thirty day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="f4f70-124">Po usunięciu i oznaczeniu wartości "nieaktywne" konto użytkownika nie jest już zwracane jako element członkowski kolekcji użytkowników (na przykład przy użyciu opcji [Pobierz listę wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="f4f70-124">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="f4f70-125">Aby uzyskać listę usuniętych użytkowników, którzy nie zostali jeszcze przeczyszczeniu, należy wykonać zapytanie o konta użytkowników, które zostały ustawione jako nieaktywne.</span><span class="sxs-lookup"><span data-stu-id="f4f70-125">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="f4f70-126">C\#</span><span class="sxs-lookup"><span data-stu-id="f4f70-126">C\#</span></span>

<span data-ttu-id="f4f70-127">Aby pobrać listę usuniętych użytkowników, należy utworzyć zapytanie filtrujące dla użytkowników klienta, których stan jest ustawiony jako nieaktywny.</span><span class="sxs-lookup"><span data-stu-id="f4f70-127">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="f4f70-128">Najpierw utwórz filtr, tworząc wystąpienie obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) z parametrami, jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="f4f70-128">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="f4f70-129">Następnie utwórz zapytanie przy użyciu metody [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) .</span><span class="sxs-lookup"><span data-stu-id="f4f70-129">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="f4f70-130">Jeśli nie chcesz, aby wyniki były stronicowane, zamiast tego możesz użyć metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) .</span><span class="sxs-lookup"><span data-stu-id="f4f70-130">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="f4f70-131">Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="f4f70-131">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="f4f70-132">Na koniec Wywołaj metodę [**zapytania**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) , aby wysłać żądanie.</span><span class="sxs-lookup"><span data-stu-id="f4f70-132">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

<span data-ttu-id="f4f70-133">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f4f70-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f4f70-134">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="f4f70-134">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f4f70-135">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f4f70-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f4f70-136">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f4f70-136">Request syntax</span></span>

| <span data-ttu-id="f4f70-137">Metoda</span><span class="sxs-lookup"><span data-stu-id="f4f70-137">Method</span></span>  | <span data-ttu-id="f4f70-138">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f4f70-138">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f4f70-139">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f4f70-139">**GET**</span></span> | <span data-ttu-id="f4f70-140">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users? size = {size} &Filter = {Filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f4f70-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f4f70-141">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f4f70-141">URI parameter</span></span>

<span data-ttu-id="f4f70-142">Podczas tworzenia żądania Użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="f4f70-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="f4f70-143">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4f70-143">Name</span></span>        | <span data-ttu-id="f4f70-144">Typ</span><span class="sxs-lookup"><span data-stu-id="f4f70-144">Type</span></span>   | <span data-ttu-id="f4f70-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4f70-145">Required</span></span> | <span data-ttu-id="f4f70-146">Opis</span><span class="sxs-lookup"><span data-stu-id="f4f70-146">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f4f70-147">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="f4f70-147">customer-id</span></span> | <span data-ttu-id="f4f70-148">guid</span><span class="sxs-lookup"><span data-stu-id="f4f70-148">guid</span></span>   | <span data-ttu-id="f4f70-149">Tak</span><span class="sxs-lookup"><span data-stu-id="f4f70-149">Yes</span></span>      | <span data-ttu-id="f4f70-150">Wartość jest identyfikatorem GUID sformatowanym przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="f4f70-150">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="f4f70-151">size</span><span class="sxs-lookup"><span data-stu-id="f4f70-151">size</span></span>        | <span data-ttu-id="f4f70-152">int</span><span class="sxs-lookup"><span data-stu-id="f4f70-152">int</span></span>    | <span data-ttu-id="f4f70-153">Nie</span><span class="sxs-lookup"><span data-stu-id="f4f70-153">No</span></span>       | <span data-ttu-id="f4f70-154">Liczba wyników do wyświetlenia w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="f4f70-154">The number of results to be displayed at one time.</span></span> <span data-ttu-id="f4f70-155">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f4f70-155">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="f4f70-156">filter</span><span class="sxs-lookup"><span data-stu-id="f4f70-156">filter</span></span>      | <span data-ttu-id="f4f70-157">filter</span><span class="sxs-lookup"><span data-stu-id="f4f70-157">filter</span></span> | <span data-ttu-id="f4f70-158">Tak</span><span class="sxs-lookup"><span data-stu-id="f4f70-158">Yes</span></span>      | <span data-ttu-id="f4f70-159">Zapytanie filtrujące wyszukiwanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f4f70-159">The query that filters the user search.</span></span> <span data-ttu-id="f4f70-160">Aby można było pobrać usuniętych użytkowników, należy uwzględnić i zakodować następujący ciąg: {"Field": "UserState", "value": "Inactive", "operator": "Equals"}.</span><span class="sxs-lookup"><span data-stu-id="f4f70-160">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f4f70-161">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f4f70-161">Request headers</span></span>

<span data-ttu-id="f4f70-162">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f4f70-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f4f70-163">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f4f70-163">Request body</span></span>

<span data-ttu-id="f4f70-164">Brak.</span><span class="sxs-lookup"><span data-stu-id="f4f70-164">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f4f70-165">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f4f70-165">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f4f70-166">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f4f70-166">REST response</span></span>

<span data-ttu-id="f4f70-167">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [CustomerUser](user-resources.md#customeruser) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f4f70-167">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f4f70-168">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f4f70-168">Response success and error codes</span></span>

<span data-ttu-id="f4f70-169">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="f4f70-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f4f70-170">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f4f70-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f4f70-171">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f4f70-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f4f70-172">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f4f70-172">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
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
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
