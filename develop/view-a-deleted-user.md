---
title: Wyświetlanie użytkowników usuniętych dla klienta
description: Pobiera listę usuniętych zasobów CustomerUser dla klienta według identyfikatora klienta. Opcjonalnie możesz ustawić rozmiar strony. Musisz podać filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445310"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="31f73-105">Wyświetlanie użytkowników usuniętych dla klienta</span><span class="sxs-lookup"><span data-stu-id="31f73-105">View deleted users for a customer</span></span>

<span data-ttu-id="31f73-106">Pobiera listę usuniętych zasobów CustomerUser dla klienta według identyfikatora klienta.</span><span class="sxs-lookup"><span data-stu-id="31f73-106">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="31f73-107">Opcjonalnie możesz ustawić rozmiar strony.</span><span class="sxs-lookup"><span data-stu-id="31f73-107">You can optionally set a page size.</span></span> <span data-ttu-id="31f73-108">Musisz podać filtr.</span><span class="sxs-lookup"><span data-stu-id="31f73-108">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31f73-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="31f73-109">Prerequisites</span></span>

- <span data-ttu-id="31f73-110">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="31f73-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="31f73-111">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31f73-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="31f73-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="31f73-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="31f73-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="31f73-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="31f73-114">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="31f73-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="31f73-115">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="31f73-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="31f73-116">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="31f73-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="31f73-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="31f73-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="31f73-118">Co się stanie po usunięciu konta użytkownika?</span><span class="sxs-lookup"><span data-stu-id="31f73-118">What happens when you delete a user account?</span></span>

<span data-ttu-id="31f73-119">Stan użytkownika jest ustawiany na "nieaktywny" podczas usuwania konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31f73-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="31f73-120">Pozostanie w ten sposób przez 30 dni, po czym konto użytkownika i skojarzone z nim dane są przeczyszczania i nie można ich uzyskać.</span><span class="sxs-lookup"><span data-stu-id="31f73-120">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="31f73-121">Jeśli chcesz przywrócić usunięte konto użytkownika w oknie 30-dniowym, zobacz Przywracanie usuniętego użytkownika [dla klienta.](restore-a-user-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="31f73-121">If you want to restore a deleted user account within the 30-day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="31f73-122">Gdy konto użytkownika zostanie usunięte i oznaczone jako "nieaktywne", nie będzie już zwracane jako członek kolekcji użytkowników (na przykład przy użyciu funkcji Pobierz listę wszystkich kont użytkowników [dla klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="31f73-122">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="31f73-123">Aby uzyskać listę usuniętych użytkowników, których jeszcze nie przeczyszczono, należy wykonać zapytanie dotyczące kont użytkowników, dla których ustawiono nieaktywność.</span><span class="sxs-lookup"><span data-stu-id="31f73-123">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="31f73-124">C\#</span><span class="sxs-lookup"><span data-stu-id="31f73-124">C\#</span></span>

<span data-ttu-id="31f73-125">Aby pobrać listę usuniętych użytkowników, skonstruuj zapytanie, które filtruje użytkowników klientów, których stan jest ustawiony na nieaktywny.</span><span class="sxs-lookup"><span data-stu-id="31f73-125">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="31f73-126">Najpierw utwórz filtr, tworząc wystąpienia obiektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) z parametrami, jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="31f73-126">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="31f73-127">Następnie utwórz zapytanie przy użyciu [**metody BuildIndexedQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery)</span><span class="sxs-lookup"><span data-stu-id="31f73-127">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="31f73-128">Jeśli nie chcesz stronicować wyników, możesz zamiast tego użyć [**metody BuildSimpleQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)</span><span class="sxs-lookup"><span data-stu-id="31f73-128">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="31f73-129">Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="31f73-129">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="31f73-130">Na koniec wywołaj [**metodę Query,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) aby wysłać żądanie.</span><span class="sxs-lookup"><span data-stu-id="31f73-130">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

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

<span data-ttu-id="31f73-131">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="31f73-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="31f73-132">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="31f73-132">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="31f73-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="31f73-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="31f73-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="31f73-134">Request syntax</span></span>

| <span data-ttu-id="31f73-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="31f73-135">Method</span></span>  | <span data-ttu-id="31f73-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="31f73-136">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="31f73-137">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="31f73-137">**GET**</span></span> | <span data-ttu-id="31f73-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="31f73-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="31f73-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="31f73-139">URI parameter</span></span>

<span data-ttu-id="31f73-140">Podczas tworzenia żądania użyj następującej ścieżki i parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="31f73-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="31f73-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="31f73-141">Name</span></span>        | <span data-ttu-id="31f73-142">Typ</span><span class="sxs-lookup"><span data-stu-id="31f73-142">Type</span></span>   | <span data-ttu-id="31f73-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="31f73-143">Required</span></span> | <span data-ttu-id="31f73-144">Opis</span><span class="sxs-lookup"><span data-stu-id="31f73-144">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="31f73-145">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="31f73-145">customer-id</span></span> | <span data-ttu-id="31f73-146">guid</span><span class="sxs-lookup"><span data-stu-id="31f73-146">guid</span></span>   | <span data-ttu-id="31f73-147">Tak</span><span class="sxs-lookup"><span data-stu-id="31f73-147">Yes</span></span>      | <span data-ttu-id="31f73-148">Wartość jest identyfikatorem klienta w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="31f73-148">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="31f73-149">size</span><span class="sxs-lookup"><span data-stu-id="31f73-149">size</span></span>        | <span data-ttu-id="31f73-150">int</span><span class="sxs-lookup"><span data-stu-id="31f73-150">int</span></span>    | <span data-ttu-id="31f73-151">Nie</span><span class="sxs-lookup"><span data-stu-id="31f73-151">No</span></span>       | <span data-ttu-id="31f73-152">Liczba wyników, które mają być wyświetlane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="31f73-152">The number of results to be displayed at one time.</span></span> <span data-ttu-id="31f73-153">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="31f73-153">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="31f73-154">filter</span><span class="sxs-lookup"><span data-stu-id="31f73-154">filter</span></span>      | <span data-ttu-id="31f73-155">filter</span><span class="sxs-lookup"><span data-stu-id="31f73-155">filter</span></span> | <span data-ttu-id="31f73-156">Tak</span><span class="sxs-lookup"><span data-stu-id="31f73-156">Yes</span></span>      | <span data-ttu-id="31f73-157">Zapytanie filtruje wyszukiwanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31f73-157">The query that filters the user search.</span></span> <span data-ttu-id="31f73-158">Aby pobrać usuniętych użytkowników, musisz dołączyć i zakodować następujący ciąg: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span><span class="sxs-lookup"><span data-stu-id="31f73-158">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="31f73-159">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="31f73-159">Request headers</span></span>

<span data-ttu-id="31f73-160">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="31f73-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="31f73-161">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="31f73-161">Request body</span></span>

<span data-ttu-id="31f73-162">Brak.</span><span class="sxs-lookup"><span data-stu-id="31f73-162">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="31f73-163">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="31f73-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="31f73-164">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="31f73-164">REST response</span></span>

<span data-ttu-id="31f73-165">W przypadku powodzenia ta metoda zwraca kolekcję [zasobów CustomerUser](user-resources.md#customeruser) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="31f73-165">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="31f73-166">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="31f73-166">Response success and error codes</span></span>

<span data-ttu-id="31f73-167">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="31f73-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="31f73-168">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="31f73-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="31f73-169">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="31f73-169">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="31f73-170">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="31f73-170">Response example</span></span>

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
